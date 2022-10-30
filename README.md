# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a script that deploys that contract.

Try running some of the following tasks:

```shellscript
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat run scripts/deploy.js
```

## Compile project
```shellscript
yarn hardhat compile
```

### How to use default value if param is not present
```
const GOERLI_RPC_URL =
  process.env.GOERLI_RPC_URL || "https://eth-goerli.g.alchemy.com/v2/_Cl4LBYjPcgxFht50Qo0Fk_zTYe6egzT"
```

## Add default network into modules
```
  defaultNetwork: "hardhat"
```

## Add other network into modules
```json
networks: {
goerli: {
    url: GOERLI_RPC_URL,
    accounts: [PRIVATE_KEY],
    chainId: 5,
},
},
```

## Run with/without network param
```
yarn hardhat run scripts/deploy.js
yarn hardhat run scripts/deploy.js --network hardhat
yarn hardhat run scripts/deploy.js --network goerli
yarn hardhat run scripts/deploy.js --network localhost 
```

if you are using localhost, hardhat local node should be run before in other bash terminal as below. 
## Run node using hardhat in terminal only
```
yarn hardhat node
```

## Add task
- Create a folder named tasks
- Create a task file named block-number.js

```javascript
const { task } = require("hardhat/config")

task("block-number", "Prints the current block number").setAction(      
  // const blockTask =  async function() => {}
  // async function blockTask() {}
  async (taskArgs, hre) => {
    const blockNumber = await hre.ethers.provider.getBlockNumber()
    console.log(`Current block number: ${blockNumber}`)
  }
)
```
- Add into hardhat.config.js
```
require("./tasks/block-number")
```
- Call task with following method
```
yarn hardhat --network hardhat block-number
yarn hardhat --network goerli block-number
```

**Note**Tasks are for plugin, scripts are for local environment!

## Add env package
```
yarn add --dev dotenv
```

## Add plugin to verify contract programmaticaly
```
yarn add --dev @nomiclabs/hardhat-etherscan
```

## Interact with hardhat local node with using console
```
yarn hardhat console --network localhost
> const SimpleStorageFactory = await ethers.getContractFactory("SimpleStorage")
> const simpleStorage = await SimpleStorageFactory.deploy()
> await simpleStorage.retrieve()
> await simpleStorage.store("55")
> await simpleStorage.retrieve()

yarn hardhat console --network hardhat
yarn hardhat console --network goerli
```

## Delete artifact and cache folders
```
yarn hardhat clean
```

## Creating Tests
```javascript
describe("SimpleStorage", () => {})
describe("SimpleStorage", function () {
  beforeEach(async function () {})

  it()
})
```

## Running Tests
```javascript
yarn hardhat test
yarn hardhat test --grep store //run a specific test by searching
```
if you set a test as "it.only("DescriptionA",functionA), it only runs it.


## Attaching Gas Reporter Tool
- Add required package into the project
```shellscript
yarn add --dev hardhat-gas-reporter
```
- Add required config into hardhat.config.js
```javascript
require("hardhat-gas-reporter")
```
```json
  gasReporter: {
    enabled: true,
    outputFile: "gas-report.txt",
    noColors: true,
    currency: "USD",
    coinmarketcap: COINMARKETCAP_API_KEY,
    token: "MATIC",
  },
```

## Attaching Test Coverage Tool
- Add required package into the project
```shellscript
yarn add --dev solidity-coverage
```
- Add required config into hardhat.config.js
```javascript
require("solidity-coverage")
```
- Run for test coverage report
```shellscript
yarn hardhat coverage
```
**Note:** Add coverage.json file and coverage folder into gitignore file

## Links
- JS Test Framework-1 - [Mochajs](https://mochajs.org/)
- JS Test Framework-2 - [Waffle](https://getwaffle.io/)
- CoinMarketCap - [API](https://pro.coinmarketcap.com/login/)
