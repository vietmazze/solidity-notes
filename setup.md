1)Create your REACT APP frontend:
- npx create-react-app react-token-faucet

2)Install hardhat,ethers,chai
- npm install ethers hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers

3)Install openzeppelin contracts if needed
- npm install @openzeppelin/contracts

4)Initialize hardhat project
- npx hardhat run

These files should be present:
hardhat.config.js - project configuration
.gitignore - github should not push
/scripts/sample-script.js - our deployer script
/test/sample-test.js - tests

Add a .env if needed
- touch .env

5) Configure .gitignore to remove production env, add to .gitignore
# misc
.env
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local






