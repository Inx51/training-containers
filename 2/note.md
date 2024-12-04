```bash
#starta en container med rabbitmq och öppna port 15672
podman run -d --name my-rabbit-mq -p 15672:15672 rabbitmq:3-management
```

```bash
#visa alla loggar (STDOUT,STDERR) för vår container samt följ loggarna (skriv inte bara ut dom)
podman logs --follow=true my-rabbit-mq
```

```bash
#Exekvera bash på vår container
podman exec -it my-rabbit-mq bash
```

```bash
#lista filer/mappar i vår container
ls
```

```bash
#byt workingdir
cd opt/rabbitmq/sbin
```

* **Visa att shovel inte är installerat**

```bash
#installera shovel på vår rabbitmq container
rabbitmq-plugins enable rabbitmq_shovel rabbitmq_shovel_management
```

```bash
#lämna kontextet av vår container
exit
```

* **Stoppa container via UI**

* **Stoppa via CLI**

* **starta via CLI**

* **Ta bort container via CLI (-f)**