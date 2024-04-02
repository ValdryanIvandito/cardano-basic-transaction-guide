# Introduction

This documentation explains how to generate Cardano wallet address using the cardano-cli, follow the steps below.

# Step by Step

## Step-1 Initiate Cardano Network

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

## Step-2 Test Querying The Blockchain (Optional)

```bash
cardano-cli query tip \
--$network
```

**_Note: Use the following command to ensure that the ledger in the database has been synchronized 100%_**

## Step-3 Make Directory

```bash
mkdir myWallet
cd myWallet
```

## Step-4 Create Payment Verification (Public) and Signing (Private) Key

```bash
cardano-cli address key-gen \
--verification-key-file payment.vkey \
--signing-key-file payment.skey
```

## Step-5 Create Stake Verification and Signing Key

```bash
cardano-cli stake-address key-gen \
--verification-key-file stake.vkey \
--signing-key-file stake.skey
```

## Step-6 Create Wallet Address

```bash
cardano-cli address build \
--payment-verification-key-file payment.vkey \
--stake-verification-key-file stake.vkey \
--out-file payment.addr \
--$network
```

## Step-7 Display The Wallet Address

```bash
myAddress=$(cat payment.addr)
echo $myAddress
```

**Example Address:**

```bash
addr_test1vzws4fmc9rds6cvc7fcah8lsc3axquaqn2r0ulxrzxze0ccmx4x5l
```

**_Note: After successfully generating a wallet address, you can top up your balance using the Cardano Faucet at the following Official Cardano Faucet [link](https://docs.cardano.org/cardano-testnet/tools/faucet/)_**

## Step-8 Display Information About the Wallet Address UTxO (Check Balance)

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

# Demo

The following is a video recorded by the Indonesian Cardano Developers Community where I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, here is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ).

# References

[Gimbalabs PPBL2023 Module 102.2: Build an Address](https://plutuspbl.io/modules/102/1022)

[Cardano Developer Portal: Generating Wallet Keys](https://developers.cardano.org/docs/operate-a-stake-pool/generating-wallet-keys/)

[CIP-0019: Cardano Addresses](https://developers.cardano.org/docs/operate-a-stake-pool/generating-wallet-keys/)
