# software-dev-course-spy-team-encryption

## GETTING STARTED

1. Each member of your group should generate a public/private key pair using the `ssh-keygen` command in the terminal:
   - Navigate to your root directory using `cd ~`.
   - Enter the following command (update to reflect your name and email): `ssh-keygen -t rsa -b 2048 -m pkcs8 -f yourName_key -C "your_email"`
   - Skip entering a passphrase by pressing `Enter` twice.
   - **NOTE:** The `.pub` file generated is not a Publisher file, it is a public key. You can open it with IntelliJ, Notepad, or another text editor to see the contents.
2. Fork and clone the asymmetric encryption application, open in IntelliJ, and run it.
3. **Test the encryption and decryption processes with your own keys first.** You'll need to use the paths to where they are stored on your hard drive (i.e. `/Users/{user}/mykey.pub` for Mac; `\Users\{user}\mykey.pub` for Windows).
4. Once you've verified your private key is correctly decrypting messages that were encrypted with your public key, it's time to send secret messages to other members of your spy team.

## SHARING SECRET MESSAGES

1. Each member should share their *public* key with the other members of the group so that everyone has everyone else's public key.
2. Make sure you keep your *private* key secret!
3. Save your teammates' public keys in the same place as your own on your local machine and, if needed, change the name of the files to have their name included so you know whose is whose.
4. Come up with a secret spy message (e.g., "The crow flies at midnight." or "The eagle has landed.").
5. With your program running, choose a team member and use *their* public key to encrypt the message. Send them the encrypted text.
6. The recipient should run the program and decrypt it using their private key.
7. Make sure everyone has received at least one message from another team member and successfully decrypted it.

## TESTING THE SECURITY OF ENCRYPTED MESSAGES

1. Send an encrypted message to a member of the spy team whose public key is *different* from the one you used to encrypt it, and ask them to decrypt it. They should be unable to decipher the message because it was encrypted with someone else's public key.
2. Make sure everyone on your team has:
   - Sent an encrypted message
   - Received and successfully decrypted a message
   - Tried (and failed) to decrypt a message intended for someone else


## NOTES AND TROUBLESHOOTING

### GETTING ERRORS

- `Error decrypting message: Padding error in decryption` : you've tried to decrypt a message meant for someone else!   
- `Error encrypting message: \{user}\{fileName}` : ensure you are using the *public* key to encrypt your message  
- `Error decrypting message: 86045F926... {encodedMessage}` : enter the private key file path first, then the message   
- `Error decrypting message: Illegal base64 character 2d` : ensure you are using the *private* key to decrypt your message. If you are using the private key and still seeing this error, see the following instructions to convert your private key to the correct format.

### FORMAT PRIVATE KEYS

**Use this section if you have a previously generated key pair with a `.pub` public key and OpenSSH private key**.  Attempting to use a private key in this format will result in program errors such as `Illegal base64 character`. If you are unsure what format your file is, see *[here](#pempub-file-structures)* for file structure examples.

If you have an existing key pair, you can delete them and generate a new key pair with the private key in PKCS8 format as shown in the first instruction, or enter the command below to convert it:

`ssh-keygen -p -m pkcs8 -f fileName`

### ***NOTES ON OPTIONS USED***

`-t`: key-type (rsa, dsa, ecdsa, ed25519, etc.)  
`-b`: bits (4096 is most common for RSA; higher bits = more security)  
`-f`: specifies filename for generated key. If not specified, generally saved in ~/.ssh/id_rsa for RSA type  
`-C`: add a comment. If not specified, will be user@computer. Using your email is very useful, since this SSH key could then be used for authentication in GitHub.  
`-m`: format  
`-p`: requests changing a passphrase of a private key instead of creating a new one (allows us to convert the private key without generating a new one)

### ***PEM/PUB FILE STRUCTURES***

#### PEM File Format

###### Public Key

`-----BEGIN PUBLIC KEY-----`  
`{KEY}`  
`-----END PUBLIC KEY-----`

###### Private Key

`-----BEGIN PRIVATE KEY-----`  
`{KEY}`  
`-----END PRIVATE KEY-----`

---

### PUB/OpenSSH File Format

##### Public Key

`ssh-rsa`  
`{KEY} `  
`{COMMENT/EMAIL}`

##### Private Key

`-----BEGIN OPENSSH PRIVATE KEY-----`  
`{KEY}`  
`-----END OPENSSH PRIVATE KEY-----`
