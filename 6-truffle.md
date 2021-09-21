1) Setup
````
mkdir learn && cd learn

#create package.json
npm init -y

#setup your version control
git init
git add
git commit -m "message"
git push -u main

#install truffle
npm install --save-dev truffle

#init config truffle
npx truffle init

````

2) Config: need to change to correct solidity version
3) Compile: make sure to add these build/contracts to .gitignore
````
npx truffle compile
````
4) Deploy and interacting with smart contracts:

      a) Install ganache - local blockchain for truffle.
      ````
        npm install --save-dev ganache-cli

        #create the local blockchain
        npx ganache-cli --deterministic
        
        #or use command by truffle
        npx truffle develop
      ````
      b) deploy requires a script inside migration/2_deploy.js
      ````javascript
          // migrations/2_deploy.js
        const Box = artifacts.require('Box');

        module.exports = async function (deployer) {
          await deployer.deploy(Box);
        };
      ````
      c) fix the truffle-config.js to point at local blockchain ganache
      ````javascript
      // truffle-config.js
          module.exports = {
          ...
            networks: {
          ...
              development: {
               host: "127.0.0.1",     // Localhost (default: none)
               port: 8545,            // Standard Ethereum port (default: none)
               network_id: "*",       // Any network (default: none)
              },
              ...
      ````
      d) call the deploy 
      ````
          npx truffle migrate --network development
      ````
      * To re-running the migration command after new functions added, use --reset
            ````truffle migrate --network development --reset   ````
5) Connecting to public networks:
      a)
      ````
      npm install --save-dev @truffle/hdwallet-provider
      ````
      b) setup account and api with Alchemy
      c) setup truffle-config.js to connect to test network such as rinkeby.
      
 
 Additional Commands
````
truffle init
truffle compile
truffle test
truffle debug
truffle migrate
````

