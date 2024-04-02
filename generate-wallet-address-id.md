# Pendahuluan

Dokumentasi ini menjelaskan cara membuat Alamat Dompet menggunakan cardano-cli, ikuti langkah-langkah dibawah ini.

# Langkah-Langkah

## Langkah-1 Inisiasi Jaringan Cardano

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

**Berikut ini adalah tabel mengenai jaringan Cardano**
| cli Parameter | Network Name |
|---------|---------|
| testnet-magic 1 | Preprod |
| testnet-magic 2 | Preview |
| mainnet | Mainnet |

## Langkah-2 Uji Kueri Blockchain (Opsional)

```bash
cardano-cli query tip \
--$network
```

**_Catatan: Gunakan perintah berikut untuk memastikan bahwa ledger di database telah tersinkronisasi 100%_**

## Langkah-3 Membuat Direktori

```bash
mkdir myWallet
cd myWallet
```

## Langkah-4 Membuat Kunci Verifikasi (Public) dan Tandatangan (Private) untuk Pembayaran

```bash
cardano-cli address key-gen \
--verification-key-file payment.vkey \
--signing-key-file payment.skey
```

## Langkah-5 Membuat Kunci Verifikasi dan Tandatangan untuk Staking

```bash
cardano-cli stake-address key-gen \
--verification-key-file stake.vkey \
--signing-key-file stake.skey
```

## Langkah-6 Membuat Alamat Dompet

```bash
cardano-cli address build \
--payment-verification-key-file payment.vkey \
--stake-verification-key-file stake.vkey \
--out-file payment.addr \
--$network
```

## Langkah-7 Menampilkan Alamat Dompet

```bash
myAddress=$(cat payment.addr)
echo $myAddress
```

**Contoh Alamat:**

```bash
addr_test1vzws4fmc9rds6cvc7fcah8lsc3axquaqn2r0ulxrzxze0ccmx4x5l
```

**_Catatan: Setelah berhasil membuat alamat dompet, Anda dapat mengisi saldo menggunakan Faucet Cardano di [link](https://docs.cardano.org/cardano-testnet/tools/faucet/) berikut._**

## Langkah-8 Menampilkan Informasi Mengenai UTxO Alamat Dompet (Cek Saldo)

```bash
cardano-cli query utxo \
--address $myAddress \
--$network
```

**Contoh Hasil:**

```bash
                           TxHash                                 TxIx        Amount
--------------------------------------------------------------------------------------
62c0ce8d6e0b584e9e263e3ba076f53c23095ebd0a9198305819cfa5ecef8e81     0        1000000000 lovelace + TxOutDatumNone
```

# Demo

The following is a video recorded by the Indonesian Cardano Developers Community where I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, here is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ)

# Referensi

[Official Documentation](https://docs.cardano.org/development-guidelines/use-cli/)

[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
