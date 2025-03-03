---
id: xrc721-token-remix
title: XRC721 using Remix IDE
keywords:
  - docs
  - apothem
  - token
  - XRC721
  - remix
description: Use Remix IDE to deploy an XRC721 Token.
---

# How to Create and Deploy an XRC721 NFT Using Remix

## 🧭 Table of contents

* [🧭 Table of contents](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-table-of-contents)
* [📰 Overview](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-overview)
  * [What you will learn](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#what-you-will-learn)
  * [What you will do](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#what-you-will-do)
  * [📰 About XRC721 Tokens](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-about-xrc721-tokens)
* [🚀 Setting up the development environment](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-setting-up-the-development-environment)
  * [⚒️ Creating XDCPay Wallet for signing transactions](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#️-creating-xdcpay-wallet-for-signing-transactions)
  * [⚒ Adding Testnet XDC to Development Wallet](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-adding-testnet-xdc-to-development-wallet)
* [💵 Writing our first XRC721 Token](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-writing-our-first-xrc721-token)
  * [💵 OpenZeppelin](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-openzeppelin)
  * [💵 Events and Functions](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-events-and-functions)
  * [💵 Methods](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-methods)
  * [💵 Compiling and Deploying](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-compiling-and-deploying)
* [🔍 Verifying Contracts on the Block Explorer](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-verifying-contracts-on-the-block-explorer)
  * [🔍 Interacting with your contract on the Block Explorer](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-interacting-with-your-contract-on-the-block-explorer)

## 📰 Overview

[Remix IDE](https://remix.xinfin.network/#optimize=false\&runs=200\&evmVersion=null\&version=soljson-v0.8.7+commit.e28d00a7.js) is a blockchain development environment, which you can use to create and test smart contracts by levering an Ethereum Virtual Machine.

#### What you will learn

In this tutorial, you will learn how to set up Remix IDE and use it to build, test and deploy a XRC721 Token on both the XDC Network mainnet and XDC Apothem testnet.

#### What you will do

* Setup Remix IDE
* Create an XRC721 token
* Compile the XRC721 token
* Deploy the XRC721 token
* Interact with the XRC721 token
* Check the deployment status on [xinfin.network](https://xinfin.network/#stats)

### 📰 About XRC721 Tokens

XRC721 is a set of rules to standardize assets on the XinFin network. Every XRC721 Token must be able to execute the following methods:

* `safeTransferFrom(address from, address to, uint256 tokenId)`
* `transferFrom(address from, address to, uint256 tokenId)`
* `approve(address to, uint256 tokenId)`
* `getApproved(uint256 tokenId)`
* `setApprovalForAll(address operator, bool _approved)`
* `isApprovedForAll(address owner, address operator)`

These are the minimum required methods that allow an asset on the XinFin network to be called an XRC721 token. Also, a XRC721 token must be able to emit the following `Events` on the blockchain:

* `Approval(address indexed owner, address indexed approved, uint256 indexed tokenId)`
* `Transfer(address indexed from, address indexed to, uint256 indexed tokenId)`
* `ApprovalForAll(address indexed owner, address indexed operator, bool approved)`

Events are helpers that come in handy in the exhaustive labor of indexing state changes, and they are essential to off-chain applications to find relevant data on the blockchain. By mapping all `Transfer` events, for example, we can fetch all the historic data on token transfers more easily.

Last but not least, a few contract constants that are public that are also very important to have are:

* `name`
* `symbol`

Without these public constants, it would be impossible to label tokens on block explorers, for example. In this tutorial we will deploy a XRC721 token that have all the `Methods`, `Events` and `Constants` mentioned above.

## 🚀 Setting up the development environment

[Remix](https://remix.xinfin.network/#optimize=false\&runs=200\&evmVersion=null\&version=soljson-v0.8.7+commit.e28d00a7) is an online solidity IDE for compiling and deploying solidity code to EVM compatible blockchains. To begin working on a new smart contract, we must first create a new file in the contracts folder on the left side of the view pane.

![](https://user-images.githubusercontent.com/60708843/190065372-1e43e443-f13b-463a-abb6-7497ae7c8b8c.png)

### ⚒️ Creating XDCPay Wallet for signing transactions

In order to get started deploying new contracts on XDC Mainnet and/or Apothem, we need to have XDCPay wallet to sign our transactions and store XDC tokens.

* First we have to install the chrome extension of [XDCPay](https://chrome.google.com/webstore/detail/xdcpay/bocpokimicclpaiekenaeelehdjllofo).

![](https://user-images.githubusercontent.com/60708843/190068514-7beac72f-ea99-49c9-ada7-7e88dc8cbf3e.png)

* Open the Chrome extension after it has been successfully installed.
* Agree to the Terms of Service.

![](https://user-images.githubusercontent.com/60708843/190069353-3214410d-0526-41c9-9c1c-1170a10840c6.png)

* Create a new XDCPay wallet by setting up a strong password or use an existing Seed Phrase **`12 or 24-Word Mnemonic Phrase`** to recover your existing wallet here.

![](https://user-images.githubusercontent.com/60708843/190121441-7b972e85-8ec0-47c2-adae-4e6c3fb01528.png)

* Keep the seed phrase safe. 🚨 **Do not share the seed phrase with anyone or you can risk losing your assets and/or the ownership of your smart contracts!** 🚨

![](https://user-images.githubusercontent.com/60708843/190071788-c134a5bc-599a-4a6d-a481-e7cf62e75a51.png)

* Verify recovery phrase
* Your XDCPay wallet has been successfully created.

### ⚒ Adding Testnet XDC to Development Wallet

Initially, our account would be empty, and we would require some XDC tokens to initiate blockchain transactions. We would use a faucet to fill our wallet with test XDC tokens for this. These tokens are worthless in and of themselves. They are simply used to test your contracts on the testnet in order to avoid losing your real money.

* First, make a copy of your wallet address. Your wallet address would look like **`xdc057ac7de8ad6f21c7bb0dcc6a389ff9161b3b943`**. These account address are interchangeable with Ethereum network. We can access these accounts on Ethereum network by simply changing the initial `xdc` with `0x`.

![](https://user-images.githubusercontent.com/60708843/190072656-cf4a819b-92e1-4eb3-948b-7c6dbc8bafc1.png)

* After that, navigate to the [XDC faucet](https://faucet.apothem.network/).
* Enter your XDC account address and request for Test XDC here.

![](https://user-images.githubusercontent.com/60708843/190073022-1d893bce-5f21-494d-8e28-20cdb9b91299.png)

* If your request is approved, you will be credited with the XDC in your wallet.
* If you can't see the XDC in your wallet, make sure you're connected to the XDC Apothem Testnet or the XDC Mainnet.

![](https://user-images.githubusercontent.com/60708843/190086617-07b3e4a8-4b4e-4e08-affa-97cce7b1f192.png)

* If you are currently connected to the XDC Mainnet, switch to the XDC Apothem Testnet.

## 💵 Writing our first XRC721 Token

The source code for the XRC721 Token used in this tutorial is available here: [XRC721 Contract Folder](XRC721/contracts/XRC721.sol). But we will address all `Events`, `Methods` and `Constants` mentioned in the section [📰 About XRC721 Tokens](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-about-xrc721-tokens).

Lets start by creating the `XRC721.sol` file.

![](https://user-images.githubusercontent.com/60708843/192205208-9d4cba9b-0bd8-4313-94ee-fabe376362c6.png)

And write the shell of our smart contract by writing:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract XRC721 {
    
}
```

### 💵 OpenZeppelin

Inside our contract, we would be importing the scripts from **`OpenZeppelin`** Github repository. These form the foundation for our contract which is having all the code of different functions which needs to be implemented in our contract. We are also importing the **`Counters`** from **`OpenZeppelin`** Github repository which is used to keep account of the counter of the current tokenId.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Counters.sol";

contract XRC721 is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;
    
}
```

### 💵 Events and Functions

As mentioned in [📰 About XRC721 Tokens](how-to-create-and-deploy-an-xrc721-nft-using-remix.md#-about-xrc721-tokens). Events are very important part of a Smart Contract logic. Events have `indexed` variables that are variables that can be filtered by off-chain interfaces. We might be tempted to index all the variables that are tied to an on-chain event, however we can't go crazy about it since Solidity has a _maximum of 3 indexed variable_ limitation for Events. Lets see how `Transfer`, `Approval` and `ApprovalForAll` are written in OpenZeppelin in a simpler form.

```solidity
contract IXRC721 {
  event Transfer(address indexed from, address indexed to, uint256 indexed tokenId);
  
  event Approval(address indexed owner, address indexed approved, uint256 indexed tokenId);
  
  event ApprovalForAll(address indexed owner, address indexed operator, bool approved);
  
  // Mapping from token ID to owner
  mapping(uint256 => address) private _tokenOwner;

  // Mapping from owner to number of owned token
  mapping(address => Counters.Counter) private _ownedTokensCount;
  
  // Mapping from token ID to approved address
  mapping(uint256 => address) private _tokenApprovals;
  
  // Mapping from owner to operator approvals
  mapping(address => mapping(address => bool)) private _operatorApprovals;
  
  /* @dev Returns the number of NFTs in `owner`'s account. */
  function balanceOf(address owner) public view returns (uint256) {
      require(owner != address(0), "XRC721: balance query for the zero address");
      return _ownedTokensCount[owner].current();
  }
  
  /* @dev Returns the owner of the NFT specified by `tokenId`.*/
  function ownerOf(uint256 tokenId) public view virtual returns (address) {
      address owner = _owners[tokenId];
      require(owner != address(0), "ERC721: owner query for nonexistent token");
      return owner;
  }
  
  * - If the caller is not `from`, it must be have been allowed to move this
  * NFT by either {approve} or {setApprovalForAll}.
  */
  function safeTransferFrom(address from, address to, uint256 tokenId, bytes memory _data) public {
      require(_isApprovedOrOwner(_msgSender(), tokenId), "XRC721: transfer caller is not owner nor approved");
      _safeTransferFrom(from, to, tokenId, _data);
  }
  
  function transferFrom(address from, address to, uint256 tokenId) public {
      //solhint-disable-next-line max-line-length
      require(_isApprovedOrOwner(_msgSender(), tokenId), "XRC721: transfer caller is not owner nor approved");
      _transferFrom(from, to, tokenId);
  }
  
  function _approve(address to, uint256 tokenId) internal virtual {
      _tokenApprovals[tokenId] = to;
      emit Approval(ownerOf(tokenId), to, tokenId);
  }
  
  function getApproved(uint256 tokenId) public view returns (address operator) {
      require(_exists(tokenId), "ERC721: approved query for nonexistent token");

      return _tokenApprovals[tokenId];
  }
  
  function setApprovalForAll(address to, bool approved) public {
      require(to != _msgSender(), "XRC721: approve to caller");
      _operatorApprovals[_msgSender()][to] = approved;
      emit ApprovalForAll(_msgSender(), to, approved);
  }
  
  function isApprovedForAll(address owner, address operator) public view virtual returns (bool) {
      return _operatorApprovals[owner][operator];
  }
}
```

We do not need to write this code in our contract. It is already implemented with the OpenZeppelin github repository.

### 💵 Methods

We need to create the `constructor` that is a function called only once when the contract is deployed, where we can parse as arguments information such as the token name and symbol. We would also create another function `createToken` which will take an address and `mint` our created `XRC721 NFT Token` to that address:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// import "@openzeppelin/contracts/token/ERC721/ERC721Full.sol";
// import "@openzeppelin/contracts/drafts/Counters.sol";

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Counters.sol";

contract XRC721 is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    constructor(string memory name, string memory symbol) ERC721(name, symbol) {
    }

    function createToken(address tokenOwner) public returns (uint256) {
        _tokenIds.increment();
        uint256 newItemId = _tokenIds.current();
        _mint(tokenOwner, newItemId);
        return newItemId;
    }
}
```

And here we have implemented everything we needed to make our token compliant with the XRC721 Standard. Of course there are more features we can implement to this contract, such as the [SafeMath](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/SafeMath.sol) library that replace naive mathematical operations for methods that will avoid `underflows` and `overflows`, and supply management methods such as `mint` and `burn`.

### 💵 Compiling and Deploying

Lets try compiling the `XRC721.sol` contract:

* Open the Solidity Compiler in the left side navigation pane ![](https://user-images.githubusercontent.com/60708843/190066438-b1816a19-3051-4d04-87d2-a2b1ade198f4.png).
* From the compiler option, select the compiler version **`v0.8.16`**.
* Choose Language as **`Solidity`**.
* Set the EVM version as the **`compiler default`**.
* Next, select **`Compile XRC721.sol`**.

![](https://user-images.githubusercontent.com/60708843/192210162-5894a8df-e00b-4eaa-b095-5fe91d284eab.png)

* After Successful Compilation, it will show ![alt](https://user-images.githubusercontent.com/60708843/190067983-4451282c-348c-4872-a57d-b2e698b59cad.png)
* Once our contract has been compiled, we can deploy it to the Apothem Test Network.

For deployment on the XDC Apothem Testnet. In either case, you need to have enough funds to pay for gas fees on the address that is being used for development.

* Navigate to Deploy and Transactions ![alt](https://user-images.githubusercontent.com/60708843/190074569-0f6cccdb-08d6-41e9-8c54-9ac9c648a283.png).

![](https://user-images.githubusercontent.com/60708843/190075329-676cc9e6-170d-46f3-92eb-8d023c24d608.png)

* Choose Injected Web3 as the Environment.

![](https://user-images.githubusercontent.com/60708843/190122488-9f142cda-4f48-4cb0-a8b5-888695c12e18.png)

* Confirm the popup to add the account to Remix IDE now.
* Next, choose the account to which you want to deploy the contract.

![](https://user-images.githubusercontent.com/60708843/190123093-c5979b6a-6026-491b-ab8f-1ae7c34b84ec.png)

* Choose the contract you want to use.

![](https://user-images.githubusercontent.com/60708843/192210725-51f3a49d-9b29-4a6b-af47-9dc3c39daebb.png)

* Add Initial values regarding your token.

![](https://user-images.githubusercontent.com/60708843/192211053-2daa9e0b-0e05-4752-8405-b33904cdadf1.png)

* Press the "transact" button and a popup will appear, which we must confirm in order to create the transaction for contract deployment.

![](https://user-images.githubusercontent.com/60708843/190075747-c7d1f7a6-2737-49ac-bd72-681a84bd95b0.png)

* After that we need to `flatten` out our smart contract so that it can be easily verified on our Block Explorer.
* For that we would right click on our smart contract file and here we would see an option to `flatten` our smart contracts on the bottom of menu pane.

![](https://user-images.githubusercontent.com/60708843/192693257-87ad3508-e0e1-4bd9-b32c-0ca06faacdea.jpg)

* Clicking on the flatten button will open a dialog box which we need to accept and a new icon for flatter is added to our left navigation pane.

![](https://user-images.githubusercontent.com/60708843/192693831-673d676a-fddc-4da6-b39d-e4f7cfe91f6d.jpg)

* After that we move to the flattener tab and will see the option to select our smart contract which we need to flatten. Here we will select our XRC721.sol smart contract and it will give an option to save the flattened smart contract.

![](https://user-images.githubusercontent.com/60708843/192696049-cb6ced5e-3f9e-415a-8ed1-09b8d0a25a91.jpg)

* After flattening, we will be having the flattened file.

This flattened code would be used further when we are verifying our token.

## 🔍 Verifying Contracts on the Block Explorer

Once you have successfully deployed your smart contract to the blockchain, it might be interesting to verify you contract on [XinFin Block Explorer](https://explorer.xinfin.network/).

First lets check the address our contract is deployed. Go to your wallet and get the most recent transaction details, then copy the transaction address.

![](https://user-images.githubusercontent.com/60708843/190076901-179e4fac-d4e8-43c7-a657-ea525a4e3883.png)

Next, navigate to the [XDC Block explorer](https://explorer.apothem.network/) and paste the transaction hash there. Note that if you deployed your token to Apothem testnet then you will need to navigate to the [Apothem Explorer](https://explorer.apothem.network/), and if you deployed your token to XDC mainnet then you will need to navigate to the [mainnet explorer](https://explorer.xinfin.network/).

![](https://user-images.githubusercontent.com/60708843/190076901-179e4fac-d4e8-43c7-a657-ea525a4e3883.png)

From there, we need to get the transaction details as well as the **`To Address`** where the contract is deployed.

![](https://user-images.githubusercontent.com/60708843/192211779-45553699-312f-4e62-8ddf-c2e211943e39.png)

Here we have a `XRC721` contract deployed on XDC Mainnet at the `0x53bA8Cb12EaF09E6B0b671F39ac4798A6DA7d660`. This address is in the Ethereum standard but we can simply swap the `0x` prefix for `xdc` and search for our newly deployed contract on [XinFin Block Explorer](https://explorer.xinfin.network/):

![Verify 01](https://user-images.githubusercontent.com/78161484/190875518-828c0061-71de-42c2-b222-0b8427852d01.png)

And click in the `Verify And Publish` Option.

We will be redirected to the Contract verification page where we need to fill out:

* Contract Name: _XRC721_
* Compiler: _Check your_ `Remix IDE` _for Compiler Version_
* Contract Code: _Just paste everything from your_ `flattened contract` _file._

Once everything is filled out, press Submit!

![Verify 02](https://user-images.githubusercontent.com/60708843/192740081-78eebba6-f1c1-456a-8978-9fa64e4619f8.jpg)

If everything is correctly filled out, your contract page on the block explorer should display a new tab called `Contract`:

![Verify 03](https://user-images.githubusercontent.com/78161484/190875780-6223b4b0-fecc-4e79-83bc-c810c5b0351c.png)

### 🔍 Interacting with your contract on the Block Explorer

With your XDCPay wallet, it is possible to interact with verified Smart Contracts on the [XinFin Network Block Explorer](https://explorer.xinfin.network/). You can read from, write to, or simply read the information tied to your Smart Contract on the blockchain.

For that, we would first copy the address where our contract is deployed on the network.

After that we would need to go back to the Remix IDE and paste that deployed contract address in the `At Address` button text box and click on that button.

![](https://user-images.githubusercontent.com/60708843/192214035-726e991c-785c-4c72-bbeb-02cae0be0faa.png)

This would fetch the contract and all the functions related to our deployed contract and we can easily play around with those functions.

![](https://user-images.githubusercontent.com/60708843/192214710-f4f49983-e315-472a-be7c-5d91f7c71011.png)

Now here we would be minting a new NFT token to our wallet.

Here we would be passing on our `wallet address` and then we click on the `createToken` button.

![](https://user-images.githubusercontent.com/60708843/192254561-f6de5540-8801-4f10-87fa-fbda5a525918.png)

After clicking in `createToken`, we need to confirm the transaction on the XDCPay wallet:

![Verify 05](https://user-images.githubusercontent.com/78161484/190876653-eb8e558b-2b09-4c0f-ad5f-a3d17a54bf30.png)

We can check for the minted token by going to our XDCPay Wallet and clicking on the `Tokens` tab and click on the `Add Token` button.

![Verify 05](https://user-images.githubusercontent.com/60708843/192256810-4ee5dad6-f4f5-4067-ba76-a5bb9b589c81.png)

Then we have to add the deployed contract address on the `Token Address` text field. This will automatically fetch the token symbol. Then click on the `Add Token` button.

![Verify 05](https://user-images.githubusercontent.com/60708843/192257221-be4f834f-ab55-471d-857e-d0e11836623f.png)

Add our newly minted token is available in our wallet.

![Verify 05](https://user-images.githubusercontent.com/60708843/192257728-188f6ec3-bf3a-40ce-bcf7-a57bef1482a9.png)

And we can check our successful transaction on the [Block Explorer!](https://explorer.apothem.network/txs/0xa95719657bee4d87068d3407e2c53acd9e955ad6eebe6f81d6cfcc59a42d7bb5#overview)

***

For more information about Remix IDE, Please Visit [Remix IDE Documentation](https://remix-ide.readthedocs.io/en/latest/).\
For more information about XinFin Network, Please Visit [XDC Network Documentation on GitBook](https://docs.xdc.org/).\
