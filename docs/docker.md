When setting up docker on Linux, add the current user to the docker group so that you don't have to use sudo with every docker command

```
sudo usermod -aG docker $USER
```
