# Transaction

This documentation explains how to perform a basic transaction. For example, if you want to send some ADA to another address from the wallet address generated earlier (refer to this [documentation](https://github.com/ValdryanIvandito/cardano-cli-simplified/blob/main/1-generate-wallet-address.md)), follow the steps below:

## Generate Wallet Address (Optional)

If you haven't generated a wallet address, you should follow this [documentation](https://github.com/ValdryanIvandito/cardano-cli-simplified/blob/main/1-generate-wallet-address.md) first.

## Initiate Blockchain Network

```bash
network="testnet-magic 1"
```

_or_

```bash
network="testnet-magic 2"
```

_or_

```bash
network="mainnet"
```

**The following is a table regarding the network on Cardano**
| cli Parameter | Network Name |
|---------|---------|
| testnet-magic 1 | Preprod |
| testnet-magic 2 | Preview |
| mainnet | Mainnet |

## Test Querying The Blockchain

```bash
cardano-cli query tip \
--$network
```

**Note:** Use the following command to ensure that the ledger in the database has been synchronized 100%



## Determine the Recipient Address and Amount to Send (Output)

```bash
recipientAddress="RECIPIENT ADDRESS"
amount="AMOUNT IN LOVELACE"
```

**Note:** 1₳ = 1,000,000 Lovelace

## Build Transaction

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $txHash#$txIx \
--tx-out $walletAddress+$sendAmountWallet \
--tx-out $paymentAddress+$sendAmountPayment \
--change-address $txAddress \
--out-file myTransaction/tx.draft
```
