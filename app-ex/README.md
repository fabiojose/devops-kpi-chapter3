# App Example

Requirements:

- node 8.9+

## How To Start

### Without Docker

```bash
npm install && npm start
```

### With Docker

```bash
docker build . -t app-ex && docker run -p 3000:3000 app-ex
```

## The Health Check

```bash
curl http://localhost:3000/healthcheck
```

## Example of Post

```bash
curl -X POST \
     -d'@./data-0.json' \
     -H'Content-Type:application/json' \
     -H'ce-specversion:0.2' \
     -H'ce-type:com.github.pull.create' \
     -H'ce-source:https://github.com/cloudevents/spec/pull/123' \
     -H'ce-id:45c83279-c8a1-4db6-a703-b3768db93887' \
     -H'ce-time:2019-06-21T17:31:00Z' \
     -H'ce-my-extension:extension value' \
     http://localhost:3000/
```
