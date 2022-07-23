## Thoughts - decentralized Twitter-like app (web3.0)

# Thoughts - Decentralized twitter-like app (Block-chain Project) 
live at: https://dthoughts.vercel.app/

## **Overview**

This is a very basic blockchain project, which is a short message(thought) sharing app. This is basically a decentralized twitter-like app, which takes users and allows them to share a short message which is publicly viewable.
The source code for this is available on GitHub at the following 
link: https://github.com/om2137/Thoughts

## **Components used**

**Ethereum:** project is based on Ethereum as a smart contract platform. <br>
**Solidity:** The programming language used in this project for smart contracts. <br>
**Hardhat:** Hardhat development environment used in the project, used to compile contracts, set up the local blockchain, etc. <br>
**Waffle:** waffle is used to test the contracts in the project. <br>
**Ethers.js:** library used to connect with the Ethereum network to perform the operation. <br>
**Metamask: **Metamask is the wallet used in this project for the transaction. <br>
**Next.js: **Next.js is the framework used in the project to build the web app or decentralized app. <br>
**Tailwind.css:  **For styling the application Tailwind.css is used. <br>

## **Working on project**

This project is divided into two parts one is a contract, where the smart contract resides and the other is a decentralized app(Dapp). <br>
In the first part, there is a smart contract written in solidity which has two main components user and thought. Users have their address, name, unique username, bio, and avatar. Address and username are unique to each user. This contract has the basic features used by the user like signup and posting messages. <br>
In the second part, there is a next.js app that has the components which we will see and use to interact with the application. It has the index.tsx in pages which is the main page where all other components are assembled like the signup page, the home page, etc. It also contains a hook useThoughts.ts which is used to connect the application with the contract. It has all the functions like connect, createuser(signup), post message, etc. used in the application. <br>
In very basic form, a smart contract is first compiled and tested on hardhat, then a node or a local Ethereum network which have multiple accounts. The smart contract is then deployed on the local network and we get the address. This address is used in Dapp to connect with the contract and the local network. Dapp is ready to run, when first started you will have to connect it with the metamask, and then one of the accounts on the local network which we ran with hardhat. After connecting Metamask signup with the relevant information and then the user is ready to tweet.


![working archi.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654684234662/2SiCQAuOs.png align="left")
 
## **Future Article of the series**

This article is just an overview of the project. What components does it use and what is the basic structure and working of the project. 
**In future articles, we will see each component in-depth and how the project is made from scratch.** <br>


follow on Twitter: https://twitter.com/omtwts





