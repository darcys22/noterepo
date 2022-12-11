It will be named key_ed25519 in /var/lib/loki, in the default deb installation.

If you have an older (pre-v8) service node there will also be a /var/lib/loki/key but for new (after 8.1.0) service nodes it won't be there and isn't needed.

If you want some help making a backup you can run:

loki-sn-keys show /var/lib/loki/key_ed25519

and then copy and paste the key values it displays in a text file somewhere (you can recreate the file from those entries).

loki-sn-keys restore /var/lib/loki/key_ed25519

which will prompt you for the keys from the text file.
