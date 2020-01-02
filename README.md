# ledger-eth-lib

WIP

## Usage

### Get Accounts

Fetch the availible accounts (currently only default).

    from ledgereth import get_accounts
    accounts = get_accounts()
    my_account = accounts[0]

### Create and Sign a Transaction

Create a transaction object and sign it.

    from ledgereth import create_transaction
    tx = create_transaction(
        '0xb78f53524ae9d465279e7c3495f71d5db2419e13',  # to
        '0x4dae53ee778a324bd317bd270d6227406b6bd4ec',  # from
        int(1e18),  # value
        int(1e5),  # gas limit
        int(1e9),  # gas price
        1  # nonce
    )
    # TODO: Double check this
    signature = '0x{}{}{}'.format(
        hex(tx.v)[2:],
        hex(tx.r)[2:],
        hex(tx.s)[2:],
    )

### Sign an Existing Transaction Object

Sign a `Transaction` object from pyethereum(or similar RLP serializable):

    from ledgereth import sign_transaction
    tx = sign_transaction(tx)
    # TODO: Double check this
    signature = '0x{}{}{}'.format(
        hex(tx.v)[2:],
        hex(tx.r)[2:],
        hex(tx.s)[2:],
    )

## API

### get_accounts(dongle: Any = None)

Fetch a `List` of accounts.

**NOTE**: This will currently only return the default/primary account from the device.

### sign_transaction(tx: Serializable, dongle: Any = None)

Sign a `rlp.Serializable` transaction.

### create_transaction(to: bytes, sender: bytes, value: int, gas: int, gas_price: int, nonce: int, data: bytes, dongle: Any = None)

Create and sign an `rlp.Serializable` transaction from provided params
