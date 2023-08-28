```
curl --location --request PUT 'http://127.0.0.1:9180/apisix/admin/routes/1' \
--header 'X-API-KEY: edd1c9f034335f136f87ad84b625c8f1' \
--header 'Content-Type: application/json' \
--data '{
    "uri": "/testresty/*",
    "name": "testresty",
    "status": 1,
    "methods": ["GET"],
    "plugins": {
        "proxy-rewrite": {
            "regex_uri": ["/testresty/(.*)", "/$1"]
        },
        
        
        
        "ext-plugin-pre-req": {
            "conf": [
                {
                    "name": "say",
                    "value": "{\"body\":\"naja\"}"
                }
            ]
        }
    },
    "upstream": {
        "type": "roundrobin",
        "nodes": {
            "testresty:80": 1
        },
        "scheme": "http"
    }
}'
```