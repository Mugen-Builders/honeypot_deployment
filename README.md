# Honeypot Deployment on Fly.io

This repository provides sample `fly.toml` files for deploying a Honeypot validator node to [Fly.io](https://fly.io).  
It contains two preconfigured examples for deployment to **Ethereum Mainnet** and **Sepolia testnet**.

> **Note:** The `fly.toml` files rely on the Dockerfile located at `../compose/Dockerfile`.  
> Ensure you place or run these configs from the correct directory.

## 🛠️ Requirements

Before proceeding, ensure you have the following:

- A valid **Fly.io account** ([sign up](https://fly.io/docs/hands-on/sign-up/))
- An **RPC URL** for the target network:
  - ⚠️ *Free Alchemy plans* may hit a 500-block range limit, causing sync issues.
  - ✅ Prefer [Infura](https://infura.io) (even free tier supports limited usage) or upgrade to a paid RPC provider.
- A **private key** funded with ETH for transaction fees on your selected network (Mainnet or Sepolia).

## 🚀 Deployment Steps

### 1. Clone the honeypot repository

Clone the Honeypot V2 repository then, via the command below

```shell
git clone https://github.com/cartesi/honeypot
```

CD into the `honeypot/contrib/compose` folder, then clone this repository using the below command

```shell
cd honeypot/contrib/compose
git clone https://github.com/cartesi/honeypot
```

### 2. Install the Fly.io CLI

Choose the installation method for your OS:

```bash
brew install flyctl                    # macOS (Homebrew)
curl -L https://fly.io/install.sh | sh # Linux/macOS
pwsh -Command "iwr https://fly.io/install.ps1 -useb | iex"  # Windows (PowerShell)
```

### 3. Authenticate with Fly.io

Authenticate your CLI using the below command:

```shell
fly auth login
```

### 4. Choose Your Network Configuration

Rename the fly.toml file appropriately: If you intend to deploy a sepolia or mainnet node then you need to rename the appropriate fly.toml.example file to fly.toml. 

```shell
# For Mainnet
mv fly.toml.mainnet.example fly.toml

# Or for Sepolia
mv fly.toml.sepolia.example fly.toml
```

### 5. Set Your App Name

Next replace the `<Application_name>` in your fly.toml file with your desired application name.

### 6. Create the Fly.io App

Create an application on fly.io using the exact name you used above:

```shell
fly app create <Application_name>
```

### 7. Set Environment Secrets

Setup the necessary environmental variables using the below command:

```shell
fly secrets set -a <Application_name> WEB3_RPC_URL=<SEPOLIA OR MAINNET RPC OF CHOICE>
fly secrets set -a <Application_name> WEB3_PRIVATE_KEY=<PRIVATE_KEY>
```

> **Note:** Ensure to replace `<Application_name>` with the name of your application, `<SEPOLIA OR MAINNET RPC OF CHOICE>` should be the RPC URL for the network of your choice and finally `<PRIVATE_KEY>` should be a private key containing gas fees for your node.

### 8. Deploy the Node

Deploy your node using the command:

```shell
fly deploy 
```
