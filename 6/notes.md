* **Varför volumes?**

```bash
# starta en container med alpine.. gör en "watch" på en fil för att undvika att containern slutförs
podman run -d --name volumedemo alpine watch "date >> /var/log/date.log"
```

```bash
podman exec -it volumedemo sh
```

```sh
# skapa en mapp
mkdir vol1
```

```sh
# gå in i mappen
cd vol1
```

```sh
# skapa en fil med innehållet "hej"
echo hej > hej.txt
```

```sh
# se så att vår fil är skapad
ls
```

```sh
# gå upp ett steg
```

```sh
# se så att vår mapp vol1 är skapad
ls
```

```sh
exit
```

```bash
podman stop volumedemo
```

* **Visa att vår container är stoppad i UI**

* **Starta vår container via UI**

```bash
podman exec -it volumedemo sh
```

```sh
# se så att vår mapp vol1 är kvar
ls
```

* **ctrl + c**

```bash
# ta bort vår container
podman rm volumedemo -f
```

```bash
# kolla så att vår container är borta
podman ps -a
```

```bash
# skapa upp en ny container med samma namn
podman run -d --name volumedemo alpine watch "date >> /var/log/date.log"
```

```bash
podman exec -it volumedemo sh
```

```sh
# vol1 är borta!
ls
```

```sh
exit
```

* **Containers är "stateless" utan volume**

```bash
# skapa vol1 mapp på host
mkdir vol1
```

```bash
# Ta bort existerande volym om en sådan finns
podman rm volumedemo -f
```

```bash
# skapa upp en ny container med samma namn fast nu med en volume -v vol1:/vol1 {relative-host-path}:{container-path}
podman run -d -v vol1:/vol1 --name volumedemo alpine watch "date >> /var/log/date.log"
```

```bash
podman exec -it volumedemo sh
```

```bash
#notera att vol1 finns här
ls
```

```sh
# gå in i mappen
cd vol1
```

```sh
# skapa en fil med innehållet "hej"
echo hej > hej.txt
```

```sh
# se så att vår fil är skapad
ls
```

* **Visa i vol1-mappen i explorer att filen även är där**

* **Skapa fil via explorer i vol1**

```sh
# alla filer visas
ls
```

```sh
exit
```

```sh
# ta bort vår container
podman rm volumedemo -f
```

* **Visa att containern är borta**

* **Visa att vol1 finns kvar i explorer**

```bash
# skapa upp samma container med samma volume
podman run -d -v vol1:/vol1 --name volumedemo alpine watch "date >> /var/log/date.log"
```

```bash
podman exec -it volumedemo sh
```

```bash
#notera att vol1 finns här
ls
```

```sh
# gå in i mappen
cd vol1
```

```bash
#visa att hej.txt finns kvar
ls
```

```bash
exit
```

```sh
# ta bort vår container
podman rm volumedemo -f
```

* **State/filer behöver alltså sparas på plats utanför containern i sig**

Detta granterar att "state" alltid är lika när en container skapas. 

Så till skillnad från en delad miljö, så vet vi EXAKT vad vi jobbar med då ingen annan har vart och pillat.

Vill vi behålla state så kan det göras genom att skapa en "volume" på en ny mapp eller existerande mapp från vår container.

* **Demo med RabbitMQ och named volume**

```bash
#Skapar en "named volume", notera att detta även syns i UI.. kan delas med flera containers
podman volume create rabbit-mq-data 
#En named-volume skapas på sin "host" i en standard-katalog (/var/lib/containers/storage/volumes/rabbit-mq-data/_data kan delvis ses via \\wsl.localhost\podman-machine-default\var\lib\containers\storage ligger i volumes men har ej access dit)
```

```bash
podman run -d --name my-rabbit-mq -p 15672:15672 -v rabbit-mq-data:/var/lib/rabbitmq/mnesia --hostname my-rabbit-mq rabbitmq:3-management
```

* **Skapa en kö i rabbitmq**
* **Lägg till ett meddelande med delivery mode satt till 2**

```bash
# Ta bort rabbitmq container
podman rm my-rabbit-mq -f
```

```bash
podman run -d --name my-rabbit-mq -p 15672:15672 -v rabbit-mq-data:/var/lib/rabbitmq/mnesia --hostname my-rabbit-mq rabbitmq:3-management
```

* **Kön ska nu va kvar i rabbitmq**

```bash
# Ta bort rabbitmq container
podman rm my-rabbit-mq -f
```

```bash
# Lista våra "named volumes"
podman volume ls
```

```bash
# Ta bort "named volume"
podman volume rm rabbit-mq-data
```