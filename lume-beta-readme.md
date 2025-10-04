# LumeGallery NFT Collection Creator - User Guide

Welcome to LumeGallery, your comprehensive platform for creating and deploying NFT collections on multiple blockchain networks. This guide will walk you through creating both **Generative** and **Deterministic** NFT collections.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Collection Types Overview](#collection-types-overview)
3. [Generative Collections Guide](#generative-collections-guide)
4. [Deterministic Collections Guide](#deterministic-collections-guide)
5. [Deployment Process](#deployment-process)
6. [Best Practices](#best-practices)
7. [Troubleshooting](#troubleshooting)

---

## Getting Started

### Prerequisites

- **Web3 Wallet**: MetaMask, WalletConnect, or compatible wallet
- **Lume NFT**: You need to own a Lume NFT to access the platform
- **Supported Networks**: HyperEVM, Abstract, Monad, or Base

### First Steps

1. **Connect Your Wallet**: Click "Connect Wallet" and authorize the connection
2. **Verify Access**: Ensure you own a Lume NFT for platform access

---

## Collection Types Overview

### Generative Collections

**Best for**: Traditional PFP projects, character collections, art with multiple layers

- **Technology**: Layered trait system with rarity weights
- **Art Format**: SVG, PNG, or GIF files
- **Deployment**: DIY deployment with full control
- **Randomization**: Based on collection seed and keccak hashing along with trait weights to create a deterministic output,

### Deterministic Collections

**Best for**: Algorithmic art, generative art, unique mathematical patterns

- **Technology**: P5.js code-based generation
- **Art Format**: Generated programmatically
- **Deployment**: Guided deployment with code review
- **Randomization**: ArtBlocks-style deterministic generation

---

## Generative Collections Guide

### Step 1: Project Setup

1. Navigate to **"Create Project"**
2. Select your blockchain network (HyperEVM, Abstract, Monad, or Base)
3. Choose **"Generative"** as your collection type
4. Configure basic collection details:
   - **Collection Name**: Your project's display name
   - **Token Name**: Individual token naming (e.g., "MyAwesomeNFT #1")
   - **Token Symbol**: Short identifier (max 5 characters)
   - **Description**: Detailed project description
   - **Total Supply**: Number of NFTs to generate
   - **Mint Price**: Cost per mint (in network currency)
   - **Max Per Wallet**: Purchase limit per address
   - **Royalties**: Creator royalties percentage

### Step 2: Trait Configuration

The trait system is the core of generative collections:

#### Layer Management

- **Maximum Layers**: 15 layers per collection
- **Layer Order**: Drag and drop to reorder layers (bottom layers render first)
- **Layer Naming**: Use descriptive names (e.g., "Background", "Eyes", "Accessories")

#### Trait Upload Process Prior to Contract Deploment.

1. **Add Layer**: Click "Add Layer" to create a new trait category
2. **Upload Assets**:
   - Supported formats: SVG, PNG, GIF
   - Recommended size: native pixel art size ifx1000px for optimal quality
   - File size limit: The maximum file size for each trait is 2 KB - you can have up to 15 layers and each layer can have up to 100 KB worth of traits.
3. **Set Rarities**: Each trait must have a rarity count that adds up to your total supply
4. **Trait Naming**: Use clear, descriptive names for each variation

#### Trait Upload Process After Contract Deploment.
1. You will be directed to the contract setting page where you will need to complete a transaction for every layer of your project to be uploaded to the contract.
2. This must be done prior to any tokens being minted.


### Step 3: Preview and Validation

1. **Generate Preview**: Use the preview system to see your collection
2. **Check Duplicates**: The preview page will warn you of any duplicates and how many.
3. **Trait Filtering**: Use the sidebar to filter by specific traits
4. **Rarity Verification**: Ensure your rarity distribution matches expectations

### Step 4: Seed Management

- **Generate Seed**: Create a random seed for trait distribution
- **Lock Seed**: Lock the seed before deployment (required)
- **New Output**: Generate new seed if you want different trait distribution

---

## Deterministic Collections Guide

### Step 1: Project Setup

1. Navigate to **"Create Project"**
2. Select your blockchain network
3. Choose **"Deterministic"** as your collection type
4. Configure basic collection details (same as generative)

### Step 2: Code Development

Deterministic collections use P5.js for art generation:

#### Code Editor Features

- **Live Preview**: Real-time preview of your code
- **Resizable Panels**: Adjust editor and preview panel sizes
- **Error Handling**: Built-in error detection and reporting
- **Seed Management**: Deterministic seed for consistent outputs

#### Available Functions

The platform automatically provides:

```javascript
// Random number generation (0-1)
R.random_dec();

// Random number between min and max
R.random_num(min, max);

// Random integer between min and max (inclusive)
R.random_int(min, max);

// Random boolean with probability
R.random_bool(probability);

// Random choice from array
R.random_choice(array);
```

#### Code Requirements

- **Canvas Size**: Use 2:3 ratio (e.g., 600x900px)
- **Deterministic**: All randomness must use the provided `R` functions
- **No External APIs**: Code runs in sandboxed environment
- **Performance**: Optimize for rendering speed

#### Starter Template

```javascript
function setup() {
  createCanvas(600, 900); // 2:3 ratio
  colorMode(HSB, 360, 100, 100);
  noLoop();
}

function draw() {
  background(0, 0, 96);

  // Use R.random_* functions for all randomness
  const circleCount = R.random_int(5, 12);
  for (let i = 0; i < circleCount; i++) {
    const hue = R.random_num(0, 360);
    const size = R.random_num(80, 240);
    const x = R.random_num(size / 2, width - size / 2);
    const y = R.random_num(size / 2, height - size / 2);

    fill(hue, 80, 90);
    ellipse(x, y, size);
  }
}
```

### Step 3: Code Review Process

1. **Submit for Review**: Click "Submit for Code Review"
2. **Review Period**: Code will be reviewed by the team
3. **Feedback**: Receive feedback and make necessary changes
4. **Approval**: Once approved, proceed to deployment

### Step 4: Testing and Validation

- **Seed Testing**: Test with different seeds to ensure variety
- **Performance Check**: Verify code runs efficiently
- **Output Quality**: Ensure consistent, high-quality outputs

---

## Deployment Process

### Pre-Deployment Checklist

- [ ] **Generative**: Seed is locked and traits are configured
- [ ] **Deterministic**: Code is reviewed and approved
- [ ] **Wallet Connected**: Ensure wallet is connected to correct network
- [ ] **Network Gas**: Sufficient funds for deployment transactions

### Deployment Steps

1. **Testnet Deployment**: Deploy to testnet first (recommended)
2. **Testing**: Thoroughly test all contract functions
3. **Mainnet Deployment**: Deploy to mainnet after testnet validation
4. **Verification**: Contract verification on block explorer

### Deployment Types

- **Testnet**: For testing and validation (free)
- **Mainnet**: For live collection (requires gas fees)

---

### General Guidelines

- **Backup Your Work**: Save projects regularly
- **Test Thoroughly**: Always test on testnet first
- Report any bug or feature requests here: https://forms.gle/W8V5YjG7QFZsHMNi7

---

## Troubleshooting

### Common Issues

#### Generative Collections

**Problem**: Trait rarities don't add up to total supply
**Solution**: Ensure each layer's rarity counts sum to your total supply

**Problem**: Duplicate NFTs in preview
**Solution**: Adjust trait weighting across all layers, reduce total supply, include more traits.

**Problem**: Upload failures
**Solution**: Check file format, size, and internet connection

#### Deterministic Collections

**Problem**: Code not running in preview
**Solution**: Check for syntax errors and use only provided functions

**Problem**: Inconsistent outputs
**Solution**: Ensure all randomness uses the `R` functions

**Problem**: Performance issues
**Solution**: Optimize code complexity and reduce computational load

#### General Issues

**Problem**: Wallet connection issues
**Solution**: Refresh page, reconnect wallet, check network

**Problem**: Deployment failures
**Solution**: Check gas fees, network connection, and contract parameters

### Getting Help

- **Documentation**: Refer to this guide and platform documentation
- **Community**: Join the LumeGallery community for support
- **Technical Support**: Contact support for technical issues

---

## Platform Features

### Navigation

- **Dashboard**: Overview of your projects and activity
- **Create Project**: Start new collection creation
- **My Projects**: Manage existing projects
- **Preview**: Test and validate and deploy your collection from this page.

### Supported Networks

- **HyperEVM**: High-performance EVM-compatible chain
- **Abstract**: Modular blockchain platform
- **Monad**: Parallel execution blockchain
- **Base**: Coinbase's Layer 2 solution


---

Happy creating! 🎨
