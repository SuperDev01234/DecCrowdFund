## Decentralized Crowdfunding App

This is a simple crowdfunding dapp intended to show off what I've learned from the B9 Lab Ethereum course. The contracts are written in Solidity and the app is utilizing the Truffle framework. The frontend of the app is built with React and Webpack. 

### Contracts

**FundingHub.sol**
The first contract is the Funding Hub. This contract is responsible for creating and maintaining a list of all Project contracts. FundingHub also offers a contribute method which can be used to contribute directly to a Project. To demonstrate a potential business model use-case Projects have been locked to only allow receiving of funds from their managing Funding Hub. You can imagine a scenario in which the FundingHub takes a small fee for managing each project.

**Project.sol**
This contract contains all of the logic around how a crowfunding project should operate. 



### App
The frontend app for this project is built on React and forks off of the [truffle-webpack-demo project](https://github.com/ConsenSys/truffle-webpack-demo) by Consensys. The cool thing about this is that it combines the latest in regular frontend javscript development with Ethereum. In order to manage the state of the dapp, Redux was chosen. 

One of my goals of this project was to see if there was a way I could abstract the asynchronous web3 and contract calls into a simple API that I could then integrate into a standard React+Redux Action/Reducer flow. This was achieved with the web3Api.js file. This approach works well with the asynchronous nature of interacting with the blockchain as things like contract properties, and account balances can seemlessly notify the app when they have updated and the UI will reflect those changes instantly.

Here is an example of how this flow works:
0. Upon initial load the app dispatchs ```fetchProjectsAndDetails()```
0. fetchProjectsAndDetails dispatchs the ```requestProjects``` Action and makes async request to web3Api's ```getProjects()``` function
0. When the ```getProjects()``` request resolves it returns the result to the ```fetchProjectAndDetails()``` function and dispatchs the ```receivedProjects``` Action which notifies the FundingHub Reducer that the state has changed. 
0. When the app sees that the state for FundingHub has changed, the UI re-renders with the new project properties and the projects are displayed in a table on the page

### Known issues/vulnerabilities


### Screenshots
![Funding Hub screen](https://github.com/tyndallm/crowdfund-dapp/blob/master/docs/images/hub_screen.png?raw=true)
![Create project screen](https://github.com/tyndallm/crowdfund-dapp/blob/master/docs/images/create_project.png?raw=true)
![Project screen](https://github.com/tyndallm/crowdfund-dapp/blob/master/docs/images/project_screen.png?raw=true)


### Running

The Web3 RPC location will be picked up from the `truffle.js` file.

0. Clone this repo
0. `npm install`
0. Make sure `testrpc` is running on its default port. Then:
  - `npm run start` - Starts the development server
  - `npm run build` - Generates a build
  - `truffle test` - Run the rest suite
