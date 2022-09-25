---
title: generate publickey again with rsa private key
created: '2022-09-25T03:09:54.074Z'
modified: '2022-09-25T04:04:42.850Z'
---

# generate publickey again with rsa private key

cause the deploy public key does not allow duplicate public key, causing trouble for us to use the git repo sync tool.

```bash
PRIVATE_KEY_PATH=/Users/jamesbrown/.notable/id_rsa_original_backup
PUBKEY_PATH=/Users/jamesbrown/.notable/id_rsa.pub2
ssh-keygen -y -f $PRIVATE_KEY_PATH > $PUBKEY_PATH
```
