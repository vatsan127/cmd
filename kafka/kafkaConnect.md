## _REST API_

List all connectors

```bash
curl -s localhost:8083/connectors | jq
```

Get connector status

```bash
curl -s localhost:8083/connectors/<connector-name>/status | jq
```

Create a connector

```bash
curl -X POST -H "Content-Type: application/json" --data '{
  "name": "<connector-name>",
  "config": {
    "connector.class": "<connector-class>",
    "tasks.max": "1",
    "topics": "<topic-name>"
  }
}' localhost:8083/connectors
```

Pause a connector

```bash
curl -X PUT localhost:8083/connectors/<connector-name>/pause
```

Resume a connector

```bash
curl -X PUT localhost:8083/connectors/<connector-name>/resume
```

Restart a connector

```bash
curl -X POST localhost:8083/connectors/<connector-name>/restart
```

Delete a connector

```bash
curl -X DELETE localhost:8083/connectors/<connector-name>
```

Get connector config

```bash
curl -s localhost:8083/connectors/<connector-name>/config | jq
```

Update connector config

```bash
curl -X PUT -H "Content-Type: application/json" --data '{
  "connector.class": "<connector-class>",
  "tasks.max": "1",
  "topics": "<topic-name>"
}' localhost:8083/connectors/<connector-name>/config
```

Get connector tasks

```bash
curl -s localhost:8083/connectors/<connector-name>/tasks | jq
```

Restart a specific task

```bash
curl -X POST localhost:8083/connectors/<connector-name>/tasks/<task-id>/restart
```

List installed connector plugins

```bash
curl -s localhost:8083/connector-plugins | jq
```

Check Connect worker status

```bash
curl -s localhost:8083/ | jq
```
