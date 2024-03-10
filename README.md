## A JWT mock server for local development

### Run in local

```shell
npm install
npm run start
## OR
npm run start -- --claims '{"username": "test@test.com", "userId": 1, "authorities": ["AUTH_1"]}'
```

### Run with npx

Default port 9000

```shell
npx --package jwt-mock-server start
```

To run in a different port 3000

```shell
PORT=3000 npx --package jwt-mock-server start
```

### endpoints

Retrieve the server's public keys (JWKS):

```shell
curl --location --request GET 'localhost:9000/jwt/.well-known/jwks.json'
```

Get a jwt token and pass claims in post body

```shell
curl --location --request POST 'localhost:9000/jwt/token' \
--header 'Content-Type: application/json' \
--data-raw '{"username": "user1@test.com"}'
```

Get a jwt using get and pass claims in query params:

```shell
curl --location --request GET 'localhost:9000/jwt/token?username=abc@test.com.au&authorities=AUTH_WP&authorities=AUTH_WP2' \
--header 'Content-Type: application/json'
```

or you can get the default claims, the default claims needs to be passed when you start the server

```shell
npx --package github:ruiyang/jwt-mock-server start --claims '{"username": "test-user@test.com"}'

curl --location --request GET 'localhost:9000/jwt/token' \
--header 'Content-Type: application/json'
```

Shutdown the server gracefully

```shell
curl --location --request GET 'localhost:9000/shutdown'
```
