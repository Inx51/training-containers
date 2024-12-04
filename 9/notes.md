
* **Flera filer av compose för att kunna kombinera**
    * default är docker-compose.yaml samt docker-compose.override.yaml
    * men fler kan specificeras 
    ```bash
    docker compose -f docker-compose.yaml -f docker-compose.utv.yaml
    ```

https://docs.docker.com/compose/how-tos/multiple-compose-files/merge/