- This document is all the information needed to test your contract before deploying to the mainnet.

````javascript
const { expect, assert } = require("chai");
const { Wallet } = require("ethers");
const { ethers } = require("hardhat");

````
**MOCHA**
- a JS library for testing

1) describe:  is a Mocha function that allows you to organize your test.
2) beforeEach: is use to do something before testing, usually follow by a it() test.
3) it(): let you create a test and naming it
4) assert: a function that assert if two things are equal, else will log error
5) expect: a function that check to see the expectation is correct, else it will log error


**ETHERS.JS**
- a js library that interact with the ETH blockchain
1) ethers.getContractFactory("Your contract name"): this function through hardhat allows you to connect to your compiled contract
2) ethers.getSigners(): this function let you get a set of randomly created Signers-wallet from ethers.js
3) ethers.connect(Signer wallet): this function let you specify what wallet is doing the SENDING to another wallet

````javascript
describe("Name your category",()=> {
  
  //within describe, you can name your variables
  let MultiSig;
	let MyMultiSig;
	let owner;
	let owners;
	let addr1;
	let addr2;
  
  // beforeEach is use to do something before testing, usually follow by a it() test.
  // use .getContractFactory to grab your compiled contract
  // use .getSigners to get the wallet for testing
  
  beforeEach(async () => {
		MultiSig = await ethers.getContractFactory("MultiSigWallet");
		[owner, addr1, addr2] = await ethers.getSigners();
		owners = await [owner.address, addr1.address, addr2.address];
		MyMultiSig = await MultiSig.deploy(owners, NUM_CONFIRMATIONS_REQUIRED);
	});
  
  it("First owner is the same if deployed", async () => {
		let testOwners = await MyMultiSig.getOwners();
		assert.equal(testOwners[0], owners[0]);
	});

  // another group of test
  // use .connect to specify what Signer you use to send Tx to.
  
  describe("executeTransaction", () => {
		beforeEach(async () => {
			console.log(owners[0]);
			const to = owners[0];
			const value = 0;
			const data =
				"0x6162636400000000000000000000000000000000000000000000000000000000";

			await MyMultiSig.submitTransaction(to, value, data);
			// Use connect(Signer) to specify what address is sending TX,
			//remember it's the Signer class itself, not owner.address
			await MyMultiSig.connect(owner).confirmTransaction(0);
			await MyMultiSig.connect(addr1).confirmTransaction(0);
		});

		it("Should request,confirm,exec by owner", async () => {
			const res = await MyMultiSig.connect(owner).executeTransaction(0);
			const { logs } = res;
			console.log(res);
			// assert.equal(logs[0].event, "ExecuteTransaction");
			// assert.equal(logs[0].args.owner, owners[0]);
			// assert.equal(logs[0].args.txIndex, 0);
			const tx = await MyMultiSig.getTransaction(0);
			assert.equal(tx.to, owners[0]);
		});
	});
}
````
