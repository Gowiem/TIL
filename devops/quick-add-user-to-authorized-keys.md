# Quickly Add User's Pub Key to Server's Authorized Users

This was taken from a DigitalOcean tutorial and I like the simplicity. For future use!

```bash
cat ~/.ssh/$USERS_PUB_KEY | ssh root@$SERVER_IP_ADDRESS "cat >> ~/.ssh/authorized_keys"
```
