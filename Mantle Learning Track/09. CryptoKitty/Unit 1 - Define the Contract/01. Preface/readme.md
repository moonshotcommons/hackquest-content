# Content/Intro

In this section, we will build the overall framework of the ***CryptoKitty*** contract.

First, it's important to note that our ***CryptoKitty*** follows the ERC721 *standard*. 

> **CryptoKitties** was launched in Nov 2017, before the ERC721 standard was proposed in Jan 2018. Therefore, there was no such thing as ERC721 when **CryptoKitties** was launch. 
We only use ERC721 framework for education purpose, so it’s easier to capture the key idea in **CryptoKitties**.
> 

Here, we will add our own functionalities on top of the ERC721 *standard*, such as breed kitties related to the token.

In this unit, we will need to 

1. setup our *contract* using ERC721.
2. define a token counter to align the kitties created in our *contract* and the tokens created in the ERC721 framework. 