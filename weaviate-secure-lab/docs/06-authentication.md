# Authentication (API Keys)

## Test authentication

Without a key:
```bash
curl -i http://localhost:8080/v1/schema
```

With a key:
```bash
curl -s http://localhost:8080/v1/schema \
  -H "Authorization: Bearer admin-key-123"
```

Next: [Authorization (RBAC)](07-authorization-rbac.md)
