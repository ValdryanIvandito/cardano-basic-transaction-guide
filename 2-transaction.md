# Transaction

This documentation explains how to perform a basic transaction in Cardano. For example, if you want to send some ADA to another address from the wallet address generated earlier. Follow the steps below:

## Generate Wallet Address (Optional)

If you haven't generated a wallet address, you should follow this [documentation](https://github.com/ValdryanIvandito/cardano-cli-simplified/blob/main/1-generate-wallet-address.md) first.

## Initiate Blockchain Network (Optional)

**Note:** If you have choosen the network, you can skip this step

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

## Test Querying The Blockchain (Optional)

```bash
cardano-cli query tip \
--$network
```

**Note:** Use the following command to ensure that the ledger in the database has been synchronized 100%

## Initiate the Input: Sender Address, Transaction Hash (TxHash), Transaction Index (TxIx)

### Display The Address

```bash
myAddress=$(cat payment.addr)
echo $myAddress
```

**Example Address:**

```bash
addr_test1vzws4fmc9rds6cvc7fcah8lsc3axquaqn2r0ulxrzxze0ccmx4x5l
```

### Display Information About the UTxO

```bash
cardano-cli query utxo \
--address $myAddress \
--$network
```

**Example Result:**

```bash
                           TxHash                                 TxIx        Amount
--------------------------------------------------------------------------------------
62c0ce8d6e0b584e9e263e3ba076f53c23095ebd0a9198305819cfa5ecef8e81     0        1000000000 lovelace + TxOutDatumNone
```

### Initiate TxHash and TxIx

```bash
utxo="COPY THE TX-HASH HERE#COPY THE TX-IX NUMBER HERE"
```

**Note:** TxHash and TxIx are restricted between **#**

## Initiate the Output: Recipient Address and Amount to Send

```bash
recipientAddress="COPY THE RECIPIENT ADDRESS HERE"
amount="AMOUNT IN LOVELACE"
```

**Note:** 1₳ = 1,000,000 Lovelace

## Build Transaction

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $utxo \
--tx-out $recipientAddress+$amount \
--change-address $myAddress \
--out-file transaction.raw
```

**Estimated transaction fee:** Lovelace 168361

## Sign Transaction

```bash
cardano-cli transaction sign \
--$network \
--tx-body-file transaction.raw \
--signing-key-file payment.skey \
--out-file transaction.signed
```

## Submit Transaction

```bash
cardano-cli transaction submit \
--$network \
--tx-file transaction.signed
```

**Result:** Transaction successfully submitted

**Note:** You can track the transaction using a blockchain explorer, such as Cardano Explorer or CardanoScan. Copy the link below:

```bash
https://preprod.cardanoscan.io/transaction/COPY-THE-TX-HASH-HERE
```
