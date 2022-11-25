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

deploy k8s:
```
cd k8s
kubectl apply -f .
```

start tunnel to ingress
```
minikube tunnel
```
open `127.0.0.1`

Forward port to 127.0.0.1:8080
```
kubectl port-forward svc/kratos-service 8080:80
```

Email can be viewed at:
```
http://127.0.0.1/mailhog/
```

```sh
curl -X POST -H "Content-Type: application/json" \
    -d '{"grant_types": ["authorization_code", "refresh_token"],
    "response_type": ["code", "id_token"],
    "token_endpoint_auth_method": "none",
    "scope": "openid offline",
    "allowed_cors_origins": ["https://oidcdebugger.com"],
    "redirect_uris": ["https://oidcdebugger.com/debug"]}' \
    http://127.0.0.1/hydra/admin/clients
```

mr#T5T9bXF79qL
mpaowmf@awef.awef