# Generate Wallet Address

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

The following is a table regarding the network on Cardano
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

## Make Directory

```bash
mkdir myWallet
cd myWallet
```

## Create Payment Verification (Public) and Signing (Private) Key

```bash
cardano-cli address key-gen \
--verification-key-file payment.vkey \
--signing-key-file payment.skey
```

## Create Stake Verification and Signing Key

```bash
cardano-cli stake-address key-gen \
--verification-key-file stake.vkey \
--signing-key-file stake.skey
```

## Create Address

```bash
cardano-cli address build \
--payment-verification-key-file payment.vkey \
--stake-verification-key-file stake.vkey \
--out-file payment.addr \
--$network
```

## Display The Address

```bash
myAddress=$(cat payment.addr)
echo $myAddress
```

- **Note:** After successfully generating a wallet address, you can top up your balance using the Cardano Faucet at the following link [Official Cardano Faucet](https://docs.cardano.org/cardano-testnet/tools/faucet/)

## Display The Balance

```bash
cardano-cli query utxo \
--address $myAddress \
--$network
```

## Demo

The following is a video recorded by the Indonesian Cardano Developers Community where I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, here is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ)

## References

[Official Documentation](https://docs.cardano.org/development-guidelines/use-cli/)  
[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
