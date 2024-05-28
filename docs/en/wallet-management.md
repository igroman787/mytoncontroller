# MyTonCtrl2 wallet management 

## Importing a wallet

MyTonCtrl2 supports various types of wallet-like contracts, including wallet-v1, wallet-v3, [lockup-wallet](https://github.com/ton-blockchain/lockup-wallet-contract/tree/main/universal), and others. Often, it provides a straightforward way to interact with these contracts.

### Importing Using a Private Key

If you have access to a private key, you can easily import a wallet:

```bash
MyTonCtrl> iw <wallet-addr> <wallet-secret-key>
```

Here, `<wallet-secret-key>` is your private key in base64 format.

### Importing Using a Mnemonic Phrase

If you have a mnemonic phrase (a sequence of 24 words like `tattoo during ...`), follow these steps:

1. Install Node.js.
2. Clone and install [mnemonic2key](https://github.com/ton-blockchain/mnemonic2key):
    ```
    git clone https://github.com/ton-blockchain/mnemonic2key.git
    cd mnemonic2key
    npm install
    ```
3. Run the following command, replacing `word1`, `word2`... with your mnemonic phrase and `address` with the address of your wallet contract:
    ```
    node index.js word1 word2 ... word24 [address]
    ```
4. The script will generate `wallet.pk` and `wallet.addr`. Rename them to `imported_wallet.pk` and `imported_wallet.addr`.
5. Copy both files to the `~/.local/share/mytoncore/wallets/` directory.
6. Open the mytonctrl console and list the wallets using the `wl` command.
7. Verify that the wallet has been imported and displays the correct balance.
8. You can now send funds using the `mg` command. Enter `mg` to view the help documentation.
Remember to replace placeholders (words inside `< >`) with your actual values when running commands.

## Show the list of wallets

```bash
MyTonCtrl> wl
```

![](/docs/img/wl.png)


## Create a new local wallet

Also you can create new empty wallet:

```bash
MyTonCtrl> nw <workchain-id> <wallet-name> [<version> <subwallet>]
```

## Activate a local wallet

If you want to use wallet it have to be activated:

```bash
MyTonCtrl> aw <wallet-name>
```

But before activating, send 1 Toncoin to wallet:

```bash
MyTonCtrl> wl 
Name                  Status  Balance           Ver  Wch  Address                                           
validator_wallet_001  active  994.776032511     v1   -1   kf_dctjwS4tqWdeG4GcCLJ53rkgxZOGGrdDzHJ_mxPkm_Xct  
wallet_004            uninit  0.0               v1   0    0QBxnZJq4oHVFs4ban3kJ5qllM1IQo57lIx8QP69Ue9A6Kbs  

MyTonCtrl> mg validator_wallet_001 0QBxnZJq4oHVFs4ban3kJ5qllM1IQo57lIx8QP69Ue9A6Kbs 1
```

Then activate it:

```bash
MyTonCtrl> aw wallet_004
ActivateWallet - OK

MyTonCtrl> wl 
Name                  Status  Balance           Ver  Wch  Address                                           
validator_wallet_001  active  994.776032511     v1   -1   kf_dctjwS4tqWdeG4GcCLJ53rkgxZOGGrdDzHJ_mxPkm_Xct  
wallet_004            active  0.998256399       v1   0    kQBxnZJq4oHVFs4ban3kJ5qllM1IQo57lIx8QP69Ue9A6Psp
```

## Get the sequence number of the wallet

```bash
MyTonCtrl> seqno <wallet-name>
```

![](/docs/img/nw.png)

## Set a wallet version

This command is needed when a modified wallet with interaction methods similar to a regular one is used.

```bash
MyTonCtrl> swv <wallet-addr> <wallet-version>
```

## Export a wallet

It's possible to get a certain wallet address and secret key.

```bash
MyTonCtrl> ew <wallet-name>
```

![](/docs/img/ew.png)

## Delete a local wallet

```bash
MyTonCtrl> dw <wallet-name>
```

![](/docs/img/dw.png)