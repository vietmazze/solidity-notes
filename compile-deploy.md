**1) COMPILE**
  To compile your contracts use: 
    - hardhat compile

  Once compile, the artifacts folder will be created.


**2) TEST YOUR CONTRACTS:**
    - Waffle and chai are used for verify contracts.
    - Using the describe/it structure through Mocha JS test.
  
  ````javascript
    const {expect} = require("chai");
    describe("MyContract", () => {
    it("should return its name", async () => {
    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy("My Contract");

    await myContract.deployed();
    expect(await myContract.getName()).to.equal("My Contract");
  });
 ````
  
  - describe: logical block of the test
  - it: tell us the name of the testing block for us to recognize later
  - const MyContract: uses ethers to look up the contract name (MyContract) and create a factory that you can instantiate
  - const myContract: use the instantiate contract and deploy all functionality
  - await myContract: Do some testing and wait for result
  - expect: the success/fail expectation once await is finish.

  To Execute the tests:
  
    - hardhat test

**3) DEPLOY CONTRACT:**

  - Deploying is nothing else than a JS file that execute on demand
  - Deploy script need to be placed inside scripts/deployMyContract.js
    
    ````javascript
        async function main() {
        const MyContract = await ethers.getContractFactory("MyContract");
        const myContract = await MyContract.deploy("My Contract");

        console.log("My Contract deployed to:", myContract.address);
      }

        main()
          .then(() => process.exit(0))
          .catch(error => {
            console.error(error);
            process.exit(1);
        });
    ````
    - Before running deploy script, we need to deploy a test network (hardhat comes with local testnet)
      - hardhat node
    - This should connect to hardhat testnet and create bunch of addresses.
    - Then to run the script use - or create a script in package.json
    
    ````
      "hardhat run --network localhost scripts/deployMyContract.js"
    ````
    -The command uses Hardhat to execute your script and defines the target network as localhost.
    
    Complete Command list:
    ````
    hardhat compile
    hardhat node
    hardhat run --network localhost scripts/deployMyContract.js
    ````
