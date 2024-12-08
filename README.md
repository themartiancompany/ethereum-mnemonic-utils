Ethereum Mnemonic Key Utils
================================

Python module/program to convert Ethereum mnemonic keys into regular private keys that
can be consumed by regular wallets.
Default parameters work for Ledger ETH wallets,
but it *should* be able to support any wallet that uses BIP32 HD and BIP39 seed standards.

Logic adapted from
https://github.com/satoshilabs/slips/blob/master/slip-0010/testvectors.py
and
https://github.com/trezor/python-mnemonic.
Work modularized and cythonized from
https://github.com/vergl4s/ethereum-mnemonic-utils/tree/master.

### Install

```bash
python \
  setup.py \
    install
```

### Examples

#### Mnemonic key > private key

```bash
echo \
  "legal winner thank year wave sausage worth useful legal winner thank yellow" > \
    myfile
ethereum-mnemonic-utils \
  myfile
```

#### Mnemonic key > private key #2

```python
from ethereum_mnemonic_utils.mnemonic_utils import mnemonic_to_private_key
private_key = mnemonic_to_private_key(
  "legal winner thank year wave sausage worth useful legal winner thank yellow")
```

#### Private key > Mist keystore using eth-keyfile module

```python
import binascii
import eth_keyfile
json_keyfile = eth_keyfile.create_keyfile_json(
  binascii.unhexlify(
    private_key),
    b"any password")
```

#### Private key > Mist keystore using web3.py module

```python
import binascii
from web3.auto import w3
json_keyfile = w3.eth.account.privateKeyToAccount(
  binascii.unhexlify(
    private_key)).encrypt(
      b"any password")
```

### License

Work relicensed from MIT license to
GNU Affero General Public License version 3
or later version
by Pellegrino Prevete.
