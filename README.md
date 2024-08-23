# MoodNFT

MoodNFT is an ERC721 smart contract that allows users to mint NFTs that reflect their mood. Each NFT can flip between two moods: Happy and Sad. The contract is built using Solidity and leverages OpenZeppelin's ERC721 implementation.

## Table of Contents

- [MoodNFT](#moodnft)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Installation](#installation)
    - [Steps](#steps)
  - [Usage](#usage)
    - [Deploying the Contract](#deploying-the-contract)
    - [Interacting with the Contract](#interacting-with-the-contract)
  - [Contract Overview](#contract-overview)
    - [Minting NFTs](#minting-nfts)
    - [Flipping Mood](#flipping-mood)
    - [Token URI](#token-uri)
  - [Error Handling](#error-handling)
  - [License](#license)

## Features

- **Mint MoodNFT:** Users can mint an NFT that starts with a "Happy" mood.
- **Flip Mood:** The owner of the NFT can flip its mood between "Happy" and "Sad".
- **Dynamic Metadata:** The NFT's metadata updates dynamically based on its mood.

## Installation

To use this contract, you need to have the following tools installed:

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [Foundry](https://getfoundry.sh/) for Solidity development

### Steps

1. Clone the repository:
   ```bash
   git clone https://github.com/TheOnma/mood-nft-project.git
   cd mood-nft
   ```

2. Install dependencies:
   ```bash
   forge install
   ```

3. Compile the smart contract:
   ```bash
   forge build
   ```

## Usage

### Deploying the Contract

To deploy the MoodNFT contract, you will need to pass in the SVG image URIs for both the "Happy" and "Sad" states:

```solidity
string memory sadSvgImageUri = "data:image/svg+xml;base64,...";
string memory happySvgImageUri = "data:image/svg+xml;base64,...";

MoodNft moodNft = new MoodNft(sadSvgImageUri, happySvgImageUri);
```

### Interacting with the Contract

1. **Minting an NFT:**
   ```solidity
   moodNft.mintNft();
   ```

   This mints a new NFT with an initial mood set to "Happy".

2. **Flipping the Mood:**
   ```solidity
   moodNft.flipMood(tokenId);
   ```

   Only the owner of the NFT can flip its mood between "Happy" and "Sad".

3. **Getting the Token URI:**
   ```solidity
   string memory tokenUri = moodNft.tokenURI(tokenId);
   ```

   This returns the metadata of the NFT, including its mood-specific image.

## Contract Overview

### Minting NFTs

The `mintNft` function allows any user to mint a new MoodNFT. The newly minted NFT will start with the "Happy" mood.

### Flipping Mood

The `flipMood` function allows the owner of the NFT to toggle its mood between "Happy" and "Sad". This operation is restricted to the NFT's owner.

### Token URI

The `tokenURI` function generates the metadata URI for the NFT. The metadata includes the name, description, attributes, and mood-specific image URI of the NFT.

```json
{
  "name": "Mood NFT",
  "description": "An NFT that reflects the owners mood.",
  "attributes": [
    {
      "trait_type": "moodiness",
      "value": 100
    }
  ],
  "image": "<imageURI>"
}
```

## Error Handling

The contract includes custom error handling to ensure that only the owner of an NFT can flip its mood:

- **`MoodNft__CantFlipMoodIfNotOwner`:** This error is thrown if a user who is not the owner of the NFT attempts to flip its mood.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```