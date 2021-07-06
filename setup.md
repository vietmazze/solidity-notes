Frontend setup:
a) npx create-react-app [name]

b) cd into react app and install: 
 
 npm install ethers hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers
 
 1) @nomiclabs/hardhat-waffle: This is a Hardhat plugin that enables waffle support.
 2) @nomiclabs/hardhat-ethers: This is a Hardhat plugin that enables ethers support.
 3) ethereum-waffle: Waffle is a Solidity testing library. It allows you to write tests for your contracts with JavaScript.
 4) chai: Chai is an assertion library and provides functions like expect.
 5) ethers: This is a popular Ethereum client library. It allows you to interface with blockchains that implement the Ethereum API.
 6) solidity-coverage: This library gives you coverage reports on unit tests with the help of Istanbul.


c)setup hardhat by typing
  
  npx hardhat
- choose sample project
- 
d) the folder will now contain [scripts],[test],[contracs] and hardhat.config.js

e) activate plugins such as waffle, chai by entering into hardhat.config.js:
 -require("@nomiclabs/hardhat-waffle")
f) make sure you're using the network you'd want and paths to artifacts

g) after this setup, we can start working on our contract

h) compiling your contract:
   npx hardhat compile 
 - this will create the artifacts in the src directory
 - artifacts/contracts/Greeter.json file contains ABI and can be use to intereact with EVM

