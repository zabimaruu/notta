[Go Back](https://rmelendez.net)

Great online document [Source](https://betterstack.com/community/questions/how-to-fix-permission-denied-error-when-connecting-to-docker/)
Some applications such as `dockge` faces *permission* issues, such as unable to *restart* and *deploy* `docker-compose`
Add user to `docker` group
```bash
sudo usermod -aG docker your-user
# or
sudo usermod -aG docker $USER
```
Restart server/computer or
```bash
newgrp docker
```

**Debian 12** - In order to create docker containers using `docker compose plugin` 
	*Note: it is essential to run `docker compose` instead of `docker-compose`*
