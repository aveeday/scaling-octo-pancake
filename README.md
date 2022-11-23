# scaling-octo-pancake

Run dev compose:
```
docker compose up --build
```

Create client:
```
docker compose exec hydra \
    hydra create client \
    --endpoint http://127.0.0.1:4445 \
    --grant-type authorization_code,refresh_token \
    --response-type code,id_token \
    --token-endpoint-auth-method none \
    --format json \
    --scope openid --scope offline \
    --allowed-cors-origin https://oidcdebugger.com \
    --redirect-uri https://oidcdebugger.com/debug
```

Go to `https://oidcdebugger.com/` and change next values:
```
Authorize URI: http://127.0.0.1:4444/oauth2/auth
Client ID: from then previous step
Response type: code
Use PKCE?: true
Token URI: http://127.0.0.1:4444/oauth2/auth
Response mode: query
```