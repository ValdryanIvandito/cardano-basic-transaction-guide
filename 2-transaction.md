# Transaction

This documentation explains how to perform a basic transaction in Cardano. For example, if you want to send some ADA to another address from the wallet address generated earlier. Follow the steps below:

# Step by Step

## Step-1 Generate Wallet Address

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

**_Note: Each transaction can have one or multiple inputs, and one or multiple outputs_**

**Single Input:**

```bash
utxo="COPY THE TX-HASH HERE#COPY THE TX-IX NUMBER HERE"
```

**Multiple Input:**

```bash
utxo1="COPY THE TX-HASH1 HERE#COPY THE TX-IX1 NUMBER HERE"
utxo2="COPY THE TX-HASH2 HERE#COPY THE TX-IX2 NUMBER HERE"
```

**_Note: TxHash and TxIx are restricted between '#'_**

## Step-4 Initiate the Output: Recipient Address and Amount to Send

**Single Output:**

```bash
recipientAddress="COPY THE RECIPIENT ADDRESS HERE"
amount="AMOUNT IN LOVELACE"
```

**Multiple Output:**

```bash
recipientAddress1="COPY THE RECIPIENT1 ADDRESS HERE"
recipientAddress2="COPY THE RECIPIENT2 ADDRESS HERE"
amount1="AMOUNT1 IN LOVELACE"
amount2="AMOUNT2 IN LOVELACE"
```

**_Note: 1₳ = 1,000,000 Lovelace_**

## Step-5 Build Transaction

**Single Transaction:**

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $utxo \
--tx-out $recipientAddress+$amount \
--change-address $myAddress \
--out-file transaction.raw
```

**Multiple Transaction:**

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $utxo1 \
--tx-in $utxo2 \
--tx-out $recipientAddress1+$amount1 \
--tx-out $recipientAddress2+$amount2 \
--change-address $myAddress \
--out-file transaction.raw
```

## Step-6 Sign Transaction

```bash
cardano-cli transaction sign \
--$network \
--tx-body-file transaction.raw \
--signing-key-file payment.skey \
--out-file transaction.signed
```

## Step-7 Submit Transaction

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

[Official Documentation](https://docs.cardano.org/development-guidelines/use-cli/)

[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
