
```yaml
tunnel: 997809ba-c344-43fb-a349-3d4fd90f6afc
credentials-file: /root/.cloudflared/997809ba-c344-43fb-a349-3d4fd90f6afc.json

ingress:
  # Rules map traffic from a hostname to a local service:
- hostname: example.com
  service: https://localhost:8000
  # Rules can match the request's path to a regular expression:
- hostname: static.example.com
  path: \.(jpg|png|css|js)$
  service: https://localhost:8001
  # Rules can match the request's hostname to a wildcard character:
- hostname: '*.example.com'
  service: https://localhost:8002
  # Example of a request mapping to the Hello World test server:
- hostname: test.apihut.net
  service: hello_world
  # An example of a catch-all rule:
- service: https://localhost:8003
- service: http_status:404
```