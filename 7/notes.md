* **Docker nyttjar egna nätverk**
    * https://docs.docker.com/engine/network/
    * typer av nätverk/Drivers
        * bridge - The default network driver.
        * host - Remove network isolation between the container and the Docker host.
        * none - Completely isolate a container from the host and other containers.

* **Exempel**

```bash
# skapa ett nätverk i "bridge-mode" (containers kan nå varandra.. host kan nå om port är publicerad -p XXXX:YYYY)
podman network create -d bridge demo-bridge
```

```bash
#Skapa två containers..
podman run -d --name ncontainer1 --network demo-bridge alpine watch "date >> /var/log/date.log"
podman run -d --name ncontainer2 --network demo-bridge alpine watch "date >> /var/log/date.log"
podman exec -it ncontainer2 sh
# Se om ncontainer2 kan nå nconatiner1
ping ncontainer1
```

```bash
podman network create -d bridge demo-bridge-abc
#Skapa två containers med ett nytt nätverk..
podman run -d --name ncontainer3 --network demo-bridge-abc alpine watch "date >> /var/log/date.log"
podman run -d --name ncontainer4 --network demo-bridge-abc alpine watch "date >> /var/log/date.log"
podman exec -it ncontainer3 sh
# Se om ncontainer3 kan nå nconatiner2
ping ncontainer2
# Isolerade på två nätverk
exit 
podman exec -it ncontainer3 sh
ping ncontainer4
```

```bash
#Skapa en containers som ansluter till båda nätverken
podman run -d --name ncontainer5 --network demo-bridge-abc --network demo-bridge alpine watch "date >> /var/log/date.log"
podman exec -it ncontainer5 sh
# Se om ncontainer5 kan nå nconatiner2 samt ncontainer3
ping ncontainer2
ping ncontainer3
# Vi kunde ansluta en container till flera nätverk
```


```bash
#Skapa två containers.. men sätt network till "none"
podman run -d --name ncontainer5 --network none alpine watch "date >> /var/log/date.log"
podman run -d --name ncontainer6 --network none alpine watch "date >> /var/log/date.log"
podman exec -it ncontainer3 sh
# Se om ncontainer5 kan nå nconatiner6
ping ncontainer4
# none = containern är helt isolerad
```

```bash
#Skapa två containers.. men sätt network till "none"
podman run -d --name sqlserver --network sqlserver-n -e SA_PASSWORD=@someThingComplicated1234 -e ACCEPT_EULA=Y -p 1433:1433 mcr.microsoft.com/mssql/server:2022-latest

#server: 127.0.0\sqlserver,1433
#username:sa
#password:@someThingComplicated1234
```

* **Jag brukar nyttja SQL Server på ovan sätt, då den tar mycket "kraft" från datron så är det skönt att kunna stänga av denna vid behov**
