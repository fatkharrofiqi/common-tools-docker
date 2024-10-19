# Step by Step
1. run *mkcert -install* on windows
2. run docker compose
    ```sh
    docker-compose up
    ```
3. open cmd execute this (do this because we generate mkcert from wsl if we generate from windows we not need run this)
    ```sh
    certutil -addstore -f "ROOT" rootCA.pem
    ```