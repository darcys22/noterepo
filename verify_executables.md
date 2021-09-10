# Eh?

So a [FOSS](https://itsfoss.com/what-is-foss/) project might have signed releases with a GPG sig. How do you verify it on a Linux machine?

Example sigp/lighthouse, but same idea for any project.

Install gpg: `sudo apt install gpg`

Grab their PGP key ID from their download page and
`gpg --keyserver pgp.mit.edu --recv THEIRKEYID` and wait

Grab both the binary and the pgp signature from their download page and
`gpg --verify SIGFILE BINFILE`

For example:
```
yorick@ethlinux:~$ gpg --verify lighthouse-v1.2.0-x86_64-apple-darwin.tar.gz.asc lighthouse-v1.2.0-x86_64-apple-darwin.tar.gz
gpg: Signature made Tue 09 Mar 2021 10:26:18 PM EST
gpg:                using RSA key 15E66D941F697E28F49381F426416DC3F30674B0
gpg: Good signature from "Sigma Prime <security@sigmaprime.io>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 15E6 6D94 1F69 7E28 F493  81F4 2641 6DC3 F306 74B0
```

Now it tells you you don't trust their key, which is exactly true. If you want to change that:
```
gpg --edit-key THEIRKEYID
gpg> trust
```

and select the level of trust to be "ultimate", and you won't be seeing those warnings any more.
```
yorick@ethlinux:~$ gpg --verify lighthouse-v1.2.0-x86_64-apple-darwin.tar.gz.asc lighthouse-v1.2.0-x86_64-apple-darwin.tar.gz
gpg: Signature made Tue 09 Mar 2021 10:26:18 PM EST
gpg:                using RSA key 15E66D941F697E28F49381F426416DC3F30674B0
gpg: Good signature from "Sigma Prime <security@sigmaprime.io>" [ultimate]
```

# Failure case

What does this look like when the signature or the file has been tampered with?

## Changed file, signature unchanged

```
yorick:~$ gpg --verify electrum-4.0.9-setup.exe.asc electrum-4.0.9-setup.exe
gpg: Signature made Fri Dec 18 14:07:22 2020 EST
gpg:                using RSA key 6694D8DE7BE8EE5631BED9502BD5824B7F9470E6
gpg: BAD signature from "Thomas Voegtlin (https://electrum.org) <thomasv@electrum.org>" [ultimate]
```

"BAD signature" ... the key is right, but the contents of the file don't match what's been signed! This file has been tampered with.

## Changed file, signed by the attacker

```
yorick:~$ gpg --verify electrum-4.0.9-setup.exe.asc electrum-4.0.9-setup.exe
gpg: Signature made Thu Mar 11 08:47:26 2021 EST
gpg:                using DSA key 52F684EE55A8FCA12FA571C67AC217EAFA29C820
gpg: Can't check signature: No public key
```

"No public key" - this wasn't signed by anybody I trust and have the public key for. This file has been tampered with, and the signature file was replaced as well.
