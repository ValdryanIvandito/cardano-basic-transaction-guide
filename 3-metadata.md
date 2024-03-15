# Metadata

This documentation explains how to perform a transaction with metadata in Cardano. Follow the steps below:

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

## Create JSON Metadata

```bash
vim metadata.json
```

**Hint:**

1. press i
2. Following is example metadata in form a message with code 674

```JSON
{
  "674": {
    "msg": [
      "Indonesian Cardano Developer Community"
    ]
  }
}
```

3. press esc
4. :wq

## Build Transaction

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

**Estimated transaction fee:** Lovelace 168669

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

## Demo

The following is a video recorded by the Indonesian Cardano Developers Community where I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, here is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ)

## References

[Official Documentation](https://docs.cardano.org/development-guidelines/use-cli/)

[Developer Portal: Metadata Transaction Guide](https://developers.cardano.org/docs/transaction-metadata/how-to-create-a-metadata-transaction-cli/)

[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
