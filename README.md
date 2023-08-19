## Setup: How to install the needed libraries

First, we need to install PyCryptodome. Open the terminal (Command Prompt on Windows, Terminal on macOS) and run the following command:

```bash
pip install pycryptodome
```

### How to generate a public and private key

You can create the public and private keys using the following code:

```python
import os
from Crypto.PublicKey import RSA

private_key_path = "private.pem"
public_key_path = "public.pem"

# Check if the private and public key files already exist
if os.path.exists(private_key_path) or os.path.exists(public_key_path):
    print("Public or private key files already exist. Aborting key generation.")
else:
    key = RSA.generate(2048)
    private_key = key.export_key()
    public_key = key.publickey().export_key()

    with open(private_key_path, "wb") as private_file:
        private_file.write(private_key)
    
    with open(public_key_path, "wb") as public_file:
        public_file.write(public_key)

    print("Public and private keys generated successfully.")

```

The above code will generate two files: `private.pem`, containing the private key, and `public.pem`, containing the public key.

## Encryption: How to encrypt a message

Assuming you have the public key and the message you want to encrypt is in a text file named `message.txt`, you can encrypt the message with the following code:

```python
import os
from Crypto.PublicKey import RSA

private_key_path = "private.pem"
public_key_path = "public.pem"

# Check if the private and public key files already exist
if os.path.exists(private_key_path) or os.path.exists(public_key_path):
    print("Public or private key files already exist. Aborting key generation.")
else:
    key = RSA.generate(2048)
    private_key = key.export_key()
    public_key = key.publickey().export_key()

    with open(private_key_path, "wb") as private_file:
        private_file.write(private_key)
    
    with open(public_key_path, "wb") as public_file:
        public_file.write(public_key)

    print("Public and private keys generated successfully.")

```

This code will create a file named `encrypted_message.bin`, containing the encrypted message.

## Decryption: How to decrypt the message

Assuming you have the private key, you can decrypt the message with the following code:

```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

private_key = RSA.import_key(open("private.pem").read())
cipher = PKCS1_OAEP.new(private_key)

with open("encrypted_message.bin", "rb") as encrypted_file:
    encrypted_message = encrypted_file.read()

decrypted_message = cipher.decrypt(encrypted_message)

with open("decrypted_message.txt", "wb") as decrypted_file:
    decrypted_file.write(decrypted_message)
```

This code will create a file named `decrypted_message.txt`, containing the original decrypted message.