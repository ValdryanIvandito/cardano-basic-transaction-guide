# Introduction

This documentation explains how to build transaction that include metadata on Cardano, follow the steps below.

# Step by Step

## Step-1 Generate Wallet Address (Optional)

If you haven't generated a wallet address, you should follow this [documentation](https://github.com/ValdryanIvandito/cardano-cli-simplified/blob/main/1-generate-wallet-address.md) first.

## Step-2 Initiate Blockchain Network (Optional)

**_Hint: If you have choosen the network, you can skip this step_**

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

## Step-3 Initiate the Input: Transaction Hash (TxHash) and Transaction Index (TxIx) from Wallet Address (Sender)

**_Hint: Assuming you already have a Wallet Address_**

### Display Information About the Wallet Address UTxO

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

**_Note: TxHash and TxIx are restricted between '#'_**

## Step-4 Initiate the Output: Recipient Address and Amount to Send

```bash
recipientAddress="COPY THE RECIPIENT ADDRESS HERE"
amount="AMOUNT IN LOVELACE"
```

**_Note: 1₳ = 1,000,000 Lovelace_**

## Step-5 Create JSON Metadata

**_Hint: To create JSON metadata, you can choose to use either Vim or Nano._**

### Using Vim

```bash
vim metadata.json
```

**Intructions:**

1. press 'i' to enter insert mode
2. Copy and paste the example metadata provided below:

```JSON
{
  "674": {
    "msg": [
      "Indonesian Cardano Developer Community"
    ]
  }
}
```

3. Press Esc to exit insert mode.
4. Type :wq to save and exit Vim.

### Using Nano

```bash
nano metadata.json
```

**Intructions:**

1. Copy and paste the example metadata provided below:

```JSON
{
  "674": {
    "msg": [
      "Indonesian Cardano Developer Community"
    ]
  }
}
```

2. Press CTRL + X.
3. If prompted with "Save modified buffer?", press Y, then press Enter to confirm saving.

## Step-6 Build Transaction

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $utxo \
--tx-out $recipientAddress+$amount \
--metadata-json-file metadata.json \
--change-address $myAddress \
--out-file transaction.raw
```

## Step-7 Sign Transaction

```bash
cardano-cli transaction sign \
--$network \
--tx-body-file transaction.raw \
--signing-key-file payment.skey \
--out-file transaction.signed
```

## Step-8 Submit Transaction

```bash
cardano-cli transaction submit \
--$network \
--tx-file transaction.signed
```

**_Hint: You can track the transaction using a blockchain explorer, such as Cardano Explorer or CardanoScan. Copy the link below._**

Preprod:

```bash
https://preprod.cardanoscan.io/transaction/COPY-THE-TX-HASH-HERE
```

Preview:

```bash
https://preview.cardanoscan.io/transaction/COPY-THE-TX-HASH-HERE
```

Mainnet:

```bash
https://cardanoscan.io/transaction/COPY-THE-TX-HASH-HERE
```

# Demo

The following is a video recorded by the Indonesian Cardano Developers Community where I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, here is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ)

# References

[Developer Portal: Metadata Transaction Guide](https://developers.cardano.org/docs/transaction-metadata/how-to-create-a-metadata-transaction-cli/)

[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
