{
"title": "Verify Downloads",
  "linkTitle": "VerifyDownloads",
  "weight": "1",
  "date": "2021-03-02",
  "description": "Verify installers and updates using PGP (Pretty Good Privacy)."
}

## Signed deliverables

API Gateway installers and updates are signed using PGP to prove authenticity and ensure integrity. This document explains how to verify the signature using Axways public PGP key. Signatures are detached and are provided in a file with the same name as the original file but with .asc appended to the filename.

## Prerequisites

* You have downloaded the required file and it's related .asc signature file from [Axway Support](https://support.axway.com).
* You have downloaded the public PGP key file (axwaypgp.asc) from [Axway Support](https://support.axway.com).
* A tool to verify PGP signature is installed.

## Import PGP Key

Use the PGP tool to import Axways public code signing PGP key axwaypgp.asc. The examples below use GNU Privacy Guard (gpg). Optionally use the gpg --edit-key option to assign a trust level to the key.

```
gpg --import axwaypgp.asc
// to enforce trustability of the key
gpg --edit-key product.security.group@axway.com trust
```

## Verify a detached signature

Use the gpg tool to verify the signature of a downloaded file.

```
gpg --verify installer.tar.gz.asc installer.tar.gz

gpg: Signature made Mon 22 Feb 2021 13:40:22 GMT
gpg:                using RSA key 1B433523955D3C69
gpg: Good signature from "AXWAY PGP KEY (Code Signing) <product.security.group@axway.com>" [ultimate]
gpg:                 aka "product.security.group@axway.com" [ultimate]
```

If the key has not been explicitly trusted the result will contain a warning, but the signature will still be shown as valid.

```
gpg --verify installer.tar.gz.asc installer.tar.gz
 
gpg: Signature made Thu Jan 28 23:25:41 2021 UTC
gpg:                using RSA key 1B433523955D3C69
gpg: Good signature from "AXWAY PGP KEY (Code Signing) <product.security.group@axway.com>" [unknown]
gpg:                 aka "product.security.group@axway.com" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 6800 AEEC B8DE 55EC 5A17  47F9 1B43 3523 955D 3C69
```
