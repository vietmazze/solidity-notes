**Array:** 
1) Deleting element creates a gap in the array, replace the last elem into the index of delete and pop the last one.

    function delete (uint index) public 
    {
    arr[index] = arr[arr.length-1]
    arr.pop()
    }


````
function <function name>(<parameters>)
    [internal | external | public | private]
    [pure | constant | view | payable]
    [modifiers]
    [return(<return types>)]
    {
        <body>
    }
````

**Accessiblity: **
1. Public - no restrictions
2. External - only from outside the contract (unless you use this)
3. Private - only from this contract
4. Internal - only from this contract and all derived contracts

**Data Locations:**
1) storage- State variables are always in storage
    Local variables of struct, array or mapping type reference storage by default
    Todos storage todo = todos[index]
2) memory - Function arguments are always in memory, function call
    function g(uint memory _arr) public returns (uint memory) 
3) calldata stack -(local variable) special data location that contains function arguments, only avail for external functions
    Local variables of value type (i.e. neither array, nor struct nor mapping) are stored in the stack
    function h(uint calldata _arr) external
    Bugs arrive because devs don't know how to store data
Notes on the usage of memory:
There are defaults for the storage location depending on which type of variable it concerns:

- State variables are always in storage

- Function arguments are always in memory

- Local variables of struct, array or mapping type reference storage by default

- Local variables of value type (i.e. neither array, nor struct nor mapping) are stored in the stack


    
**Function input/output:**
1) cannot use mapping for input/output in function
2) cannot use multidimensional array/

**View and Pure Functions:**
1) View function declares that no state will be changed
2) Pure function declares that no state variable will be changed or read.

**Throwing Exceptions:**

1) require(condition) - Ensure valid conditions/state, validate return values
   ```` 
    Validation of inputs, external call returns and variables before state changes
    Refunds remaining gas when fail
    Should be used more often and towards the beginning of functions
    ````
2)assert() - Test internal errors and check for invariants
    
    ````
    Validation of invariants, situations that should never happen and variables after state changes
    Consumes all gas when fail
    Should be used less often and towards the end of functions
    ````
3)revert() - always throw an exception
    ````
        Reverts the current transaction
        Refunds remaining gas when fail
        Used within if-else statements
    ````

**Function Modifier:**
1) They are use before/after a function call to do:
    a) restrict write access to specific msg.sender of the contract
    b) validate inputs b4 running another function
    c) guard against the reentrancy hack (where 2 contracts call each other recursively?)
  
**Inheritance:** 
Within a contract:
1) Virtual: A parent function that is going to be overriden by child, must declare virtual
    ````
    function foo() public virtual returns (string memory) {}
    ````
2) Override: Contract that override a parent function must contain override
Contract to Contract
3) All contract inheritance of another must use "is" to inherit another
    ````
    contract A {}
    contract B is A {}
    ````
4) Contracts order of inheritance is important, and it is from RIGHT to LEFT order but most-based like first.
    ````
    contract A
    contract B
    C will inherit functions in B before A since B is first come
    contract C is A,B {}
    ````
5) If you have:
    ````contract A
    contract B is A
    contract C is A,B
    ````
   We will run into error because B is based on A, and A is most based first.
   
**Sending Ether:**
3 ways to send ETHER from contract to contract:
1) Transfer: this method forwards 2300gas, but will throw error if tx fail for cases such as (not enough gas),(nonpayable contract)
    a. Good to guard against re-entrancy hack but 2300gas limit is issue
2) Send: this method forwards 2300 gas, and returns bool.
    a. 2300 gas limit
3) Call: forwards set amount/max gas, and returns bool.
    a. Good for future tx since we can limit/set gas amount.
    b. Becareful of re-entrancy hack using this method.

**Receiving Ether:**
-When receiving ETHER, either fallback() or receive() must exist within the contract.
1) Receive() is called if msg.data is empty
2) fallback() is called if msg.data is not empty

**Keccak256 Hash Function:**
- In order to create a hash in Solidity, we use keccak256
1) The parameter for keccak can be anything such as string _text, uint _num, address _addr
    bytes32 hash = keccak256(abi.encodePacked(_text,_num,_addr));
2) Collision Resistant - keccak256 is collision resistant BUT abi.encodePacked can mess up on dynamic variables
    bytes32 hash = keccak256(abi.encodePacked(_text1,_text2));
    This will run into issue if 
    text1 = AA
    text2 = BB
    encodePacked will combine before hashing.
    The best way to avoid is use abi.encode
