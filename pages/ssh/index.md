### Adding public key to server ``authorized_keys``

```bash
cat ~/.ssh/id_rsa.pub | ssh USER@HOST "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
