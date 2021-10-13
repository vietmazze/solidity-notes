Frontend setup:
a) npx create-react-app [name] or npx create-next-app [name]

b) cd into react app and install: 
 
 npm install ethers hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers @openzeppelin/contracts
````
   npm install ethers hardhat @nomiclabs/hardhat-waffle \
   ethereum-waffle chai @nomiclabs/hardhat-ethers \
   web3modal @openzeppelin/contracts ipfs-http-client@50.1.2 \
   axios
````
 1) @nomiclabs/hardhat-waffle: This is a Hardhat plugin that enables waffle support.
 2) @nomiclabs/hardhat-ethers: This is a Hardhat plugin that enables ethers support.
 3) ethereum-waffle: Waffle is a Solidity testing library. It allows you to write tests for your contracts with JavaScript.
 4) chai: Chai is an assertion library and provides functions like expect.
 5) ethers: This is a popular Ethereum client library. It allows you to interface with blockchains that implement the Ethereum API.
 6) web3modal: Allow users to choose what wallet
 7) @openzeppelin/contracts: audited contracts
 8) ipfs-http-client: Library for IPFS
 9) axios: for React storage

b2) Install tailwind for css
````
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
npm tailwindcss init -p
````
c)setup hardhat by typing
  
  npx hardhat

  npm install --save-dev hardhat
- choose sample project


d) the folder will now contain [scripts],[test],[contracs] and hardhat.config.js

e) activate plugins such as waffle, chai by entering into hardhat.config.js:
 
 -require("@nomiclabs/hardhat-waffle")
 
f) make sure you're using the network you'd want and paths to artifacts


g) need this to remove password related
````
const fs = require('fs')
const privateKey = fs.readFileSync(".secret").toString().trim()

````

Full Command list:
````
npx create-react-app [name]
npm install ethers hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers
npx hardhat
````
** See compile and deploy for further steps.

