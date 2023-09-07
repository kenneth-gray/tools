# Using GPG

## Generate public/private key pair

```sh
gpg --full-generate-key
```

- Select default key kind: RSA and RSA
- Type largest key size (currently 4096)
- Give a reasonable expiry (1y as a default)
- Fill out the other personal details
- Enter suitable password that will encrypt/decrypt the private key

## List public keys

```sh
gpg --list-keys --quiet
```

## Export public key

```sh
gpg --output [output-file-public-key.gpg] --export [public-key-id]
```

## Import public key

```sh
gpg --import [public-key.gpg]
```

### Trust key (once you're certain key is legitimate)

```sh
gpg --edit-key [user@example.com]
sign
save
```

## Encrypting a file using a public key

```sh
gpg --encrypt --output [output-file.gpg] --recipient [user@example.com] [input-file]
```

- output-file.gpg: Name of the output file, usually the same as the input file, but with a .gpg postfix
- user@example.com: Email of the public key to use
- input-file: File to encrypt

## Decrypt file using private key

```sh
gpg --decrypt --output [ouput-file] [input-file.gpg]
```

- output-file: Name of the output file, usually the same as the input file minus the .gpg postfix
- input-file.gpg: File to decrypt
