
* **Visa image i ./HelloWorld/Dockerfile**

* **Vad är en base-image?**

* **Visa Docker instructions** https://docs.docker.com/reference/dockerfile/
    * **Förklara "tags"**

* **Bygg med Dockerfile**
```bash
podman build -t img-helloworld ./HelloWorld
```

```bash
#Kör vår image, och följ STDOUT (loggen)
podman run --name my-hello-world -a STDOUT img-helloworld
```

```dockerfile
#Ändra i Dockerfile till
FROM alphine:latest

CMD echo "Not you again!"
```

```bash
#Bygg med Dockerfile med tag!
podman build -t img-helloworld:again ./HelloWorld
```

```bash
#Kör vår image med tag, och följ STDOUT (loggen)
podman run --name my-hello-world-again -a STDOUT img-helloworld:again
```

```bash
#Visa alla images (finns i UI också)
podman images -a
```
