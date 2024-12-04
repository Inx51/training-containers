* **vad är ett registry?**

* **Visa docker hub och quay**
    * https://hub.docker.com/
    * https://quay.io/

* **Slå upp RabbitMQ på docker hub**

* **Gör en publish till public repo på docker hub**

```bash 
podman login docker.io
#se credentials i 1Password
```

```bash
podman push helloworld:latest docker://docker.io/51inx/helloworld
#podman push {vår image ed tag} {repo}
```

```bash
#ta bort image som precis pushades lokalt
podman rmi helloworld:latest
```

```bash
podman run --name helloworldagain -a STDOUT 51inx/helloworld:latest
```

* **Hur lägger jag till ett registry? (***Inget man behöver bry sig om i vanliga fall***)**