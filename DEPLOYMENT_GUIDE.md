# 🚀 SpinBase Smart Contract Deployment Guide

Complete guide to deploy the SpinBase smart contract ecosystem on Celo blockchain.

## 📋 Prerequisites

- Node.js >= 18.0.0
- npm or pnpm package manager
- A Celo wallet with CELO tokens for gas fees
- Celo extension or similar Web3 wallet

## 🔑 Step 1: Setup Wallet & Get Testnet CELO

### Create/Import Celo Wallet
1. Install [Celo Extension Wallet](https://chrome.google.com/webstore/detail/celo-extension-wallet/kkilomkmpmkbupvmffavfdeconfirmDialog) or use MetaMask
2. Create a new account or import existing one
3. Save your private key securely

### Get Testnet CELO (Celo Sepolia)
1. Visit [Celo Faucet](https://faucet.celo-sepolia.celo-testnet.org/)
2. Enter your wallet address
3. Claim 5 testnet CELO (free)

### Get Mainnet CELO (Optional, requires purchase)
- Buy CELO from exchanges (Coinbase, Kraken, etc.)
- Bridge from other chains using [Celer cBridge](https://cbridge.celer.network/)

---

## ⚙️ Step 2: Environment Setup

### Navigate to Hardhat Contracts Directory
```bash
cd templates/contracts/hardhat
```

### Install Dependencies
```bash
npm install
# or
pnpm install
```

### Create .env File
```bash
cp .env.example .env.local
```

### Edit `.env.local` with Your Values
```env
# Get your private key from Celo wallet
PRIVATE_KEY=0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef

# Get API key from Celoscan.io (optional, for verification)
ETHERSCAN_API_KEY=your_celoscan_api_key

# Enable gas reporting (optional)
REPORT_GAS=true
```

⚠️ **IMPORTANT: Never commit your .env file or share your private key!**

---

## 🧪 Step 3: Test Contracts (Optional but Recommended)

Run the test suite to ensure contracts are working:
```bash
npm run test
```

Expected output:
```
✓ SpinBaseToken tests (7 tests)
✓ SpinWheel tests (8 tests)
✓ StakingVault tests (6 tests)
```

---

## 🔗 Step 4: Deploy to Celo Sepolia Testnet

### Compile Contracts First
```bash
npm run build
```

### Deploy to Testnet
```bash
npm run deploy:celo-sepolia
```

**Output Example:**
```
SpinBaseToken deployed to: 0x1234567890abcdef1234567890abcdef12345678
SpinNFT deployed to: 0xabcdefabcdefabcdefabcdefabcdefabcdefabcd
SpinWheel deployed to: 0x5678901234567890123456789012345678901234
StakingVault deployed to: 0xdeadbeefdeadbeefdeadbeefdeadbeefdeadbeef
SpinBaseVotes deployed to: 0xcafebabecafebabecafebabecafebabecafebabe
SpinBaseGovernor deployed to: 0xfacefacefacefacefacefacefacefacefaceface
```

**Copy these addresses!** You'll need them for the next step.

### View Deployment Details
```bash
# Check deployment artifacts
cat ./ignition/deployments/chain-11142220/deployed_addresses.json
```

---

## ✅ Step 5: Verify Contracts (Optional)

Verify contracts on Celoscan for transparency and debugging:

```bash
npm run verify -- <CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

Example:
```bash
npm run verify -- 0x1234567890abcdef1234567890abcdef12345678 1000000000000000000000000
```

---

## 🌐 Step 6: Add Contracts to GitHub Project

1. Go to your SpinBase-Celo repository
2. Click on your profile → Settings → Data sources (or navigate to the Add Smart Contracts page)
3. Click "Add smart contracts"
4. Enter each contract address and select "Celo" chain:

| Contract | Address |
|----------|---------|
| SpinBaseToken (SPIN) | 0x... |
| SpinNFT | 0x... |
| SpinWheel | 0x... |
| StakingVault | 0x... |
| SpinBaseVotes (SPINGOV) | 0x... |
| SpinBaseGovernor (DAO) | 0x... |

5. Click "Verify" for each contract

---

## 📊 Step 7: Monitor Deployments

### Verify on Block Explorer

**Celo Sepolia Testnet:**
- Explorer: https://sepolia.celoscan.io/
- Enter your contract address to view transactions

**Celo Mainnet:**
- Explorer: https://celoscan.io/
- Enter your contract address to view transactions

### Check Contract Events
Visit the contract on Celoscan → Events tab to see all transactions

---

## 🚀 Step 8: Deploy to Mainnet (Optional)

**IMPORTANT:** Only do this after thorough testing on testnet!

### Get Mainnet CELO
- Ensure you have CELO tokens in your wallet for gas fees
- Gas costs typically: 0.1-1 CELO per transaction

### Deploy to Mainnet
```bash
npm run deploy:celo
```

### Monitor Gas Prices
Visit [Celo Gas Station](https://docs.celo.org/learn/platform/celo-for-mobile) for current gas prices

---

## 🔧 Troubleshooting

### Error: "Invalid Private Key"
- Ensure private key is in correct format (0x prefix + 64 hex characters)
- Check there are no extra spaces or newlines in .env file

### Error: "Insufficient Funds"
- Make sure your wallet has enough CELO for gas fees
- Request testnet CELO from faucet: https://faucet.celo-sepolia.celo-testnet.org/

### Error: "Contract Already Deployed"
- Each deployment creates new instances
- Use the addresses from the latest deployment
- Delete `ignition/deployments` folder to reset

### Error: "Network Not Found"
- Verify hardhat.config.ts has correct network configuration
- Check internet connection to RPC endpoint

### Slow Deployment
- Celo network can take 30-60 seconds per transaction
- Be patient and don't interrupt the process
- Monitor on block explorer

---

## 📝 Contract Addresses (Sepolia Testnet Example)

After successful deployment, save these addresses:

```json
{
  "network": "celo-sepolia",
  "chainId": 11142220,
  "contracts": {
    "spinToken": "0x...",
    "spinNFT": "0x...",
    "spinWheel": "0x...",
    "stakingVault": "0x...",
    "spingov": "0x...",
    "governor": "0x..."
  }
}
```

---

## 📚 Additional Resources

- [Celo Documentation](https://docs.celo.org)
- [Hardhat Documentation](https://hardhat.org/docs)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)
- [Celoscan Block Explorer](https://celoscan.io)
- [Celo Faucet](https://faucet.celo-sepolia.celo-testnet.org/)

---

## ⚠️ Security Best Practices

1. **Never share your private key**
2. **Use testnet for testing**, mainnet for production
3. **Always verify contracts** on block explorer
4. **Test thoroughly** before mainnet deployment
5. **Keep .env files private** - add to .gitignore
6. **Audit contracts** before large deployments
7. **Use hardware wallet** for mainnet (Ledger, Trezor)

---

## 🎉 Next Steps

After deployment:

1. ✅ Add contract addresses to GitHub project
2. ✅ Update frontend to use contract addresses
3. ✅ Create interaction guide for users
4. ✅ Set up monitoring and analytics
5. ✅ Plan governance token distribution

---

**Need Help?**
- Check contract comments in source files
- Review test files for usage examples
- Join [Celo Discord](https://discord.com/invite/celo)

**Happy deploying! 🚀**
