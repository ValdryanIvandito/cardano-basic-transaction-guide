# Pendahuluan

Dokumentasi ini menjelaskan cara membuat transaksi di Cardano, ikuti langkah-langkah dibawah ini.

# Langkah-Langkah

## Langkah-1 Membuat Alamat Dompet

Jika Anda belum membuat Alamat Dompet, ikuti [dokumentasi](https://github.com/ValdryanIvandito/cardano-basic-transaction-guides/blob/main/generate-wallet-address-id.md) berikut.

## Langkah-2 Inisiasi Jaringan Cardano (Opsional)

**_Petunjuk: Jika Anda sudah memilih jaringan, Anda dapat melewati langkah ini_**

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

## Langkah-3 Inisiasi Parameter Input: Hash Transaksi (TxHash) dan Indeks Transaksi (TxIx) dari Alamat Dompet (Pengirim)

**_Petunjuk: Asumsi Anda telah memiliki Alamat Dompet_**

### Menampilkan Informasi Mengenai UTxO Alamat Dompet

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

### Inisiasi TxHash dan TxIx

**_Catatan: Setiap transaksi dapat memiliki satu atau beberapa input, dan satu atau beberapa output_**

**Satu Input:**

```bash
utxo="COPY TX-HASH DISINI#COPY TX-IX DISINI"
```

**Beberapa Input:**

```bash
utxo1="COPY TX-HASH1 DISINI#COPY TX-IX1 DISINI"
utxo2="COPY TX-HASH2 DISINI#COPY TX-IX2 DISINI"
```

**_Catatan: TxHash dan TxIx dibatasi antara '#'_**

## Langkah-4 Inisiasi Parameter Output: Alamat Penerima dan Jumlah ADA yang Akan Dikirim

**Satu Output:**

```bash
recipientAddress="COPY ALAMAT PENERIMA DISINI"
amount="JUMLAH DALAM LOVELACE"
```

**Beberapa Output:**

```bash
recipientAddress1="COPY THE RECIPIENT1 ADDRESS DISINI"
recipientAddress2="COPY THE RECIPIENT2 ADDRESS DISINI"
amount1="AMOUNT1 IN LOVELACE"
amount2="AMOUNT2 IN LOVELACE"
```

**_Catatan: 1₳ = 1,000,000 Lovelace_**

## Langkah-5 Membuat Transaksi

**Satu Transaksi:**

```bash
cardano-cli transaction build \
--babbage-era \
--$network \
--tx-in $utxo \
--tx-out $recipientAddress+$amount \
--change-address $myAddress \
--out-file transaction.raw
```

**Beberapa Transaksi:**

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

## Langkah-6 Menandatangani Transaksi

```bash
cardano-cli transaction sign \
--$network \
--tx-body-file transaction.raw \
--signing-key-file payment.skey \
--out-file transaction.signed
```

## Langkah-7 Mengirim Transaksi

```bash
cardano-cli transaction submit \
--$network \
--tx-file transaction.signed
```

**_Petunjuk: Anda dapat melacak transaksi menggunakan penjelajah blockchain, seperti Cardano Explorer atau CardanoScan. Salin tautan di bawah ini._**

Preprod:

```bash
https://preprod.cardanoscan.io/transaction/COPY-THE-TX-HASH-DISINI
```

Preview:

```bash
https://preview.cardanoscan.io/transaction/COPY-THE-TX-HASH-DISINI
```

Mainnet:

```bash
https://cardanoscan.io/transaction/COPY-THE-TX-HASH-DISINI
```

# Demo

The following is a video recorded by the Indonesian Cardano Developers Community wDISINI I demonstrated the steps above. Watch the recorded video at timestamp **_1:27:27_**, DISINI is the [link](https://youtu.be/03hXLZ_07N0?list=PLUj8499OocHiL8gXPv8wMlLW-zIcyYdrQ).

# Referensi

[Official Documentation](https://docs.cardano.org/development-guidelines/use-cli/)

[Gimbalabs PlutusPBL](https://plutuspbl.io/modules/102/slts)
