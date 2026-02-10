# Verify Weaviate is Running

## Test without authentication (should fail)

```bash
curl -i http://localhost:8080/v1/meta
```

## Test with admin API key (should succeed)

```bash
curl -s http://localhost:8080/v1/meta \
  -H "Authorization: Bearer admin-key-123"
```

Next: [Authentication (API Keys)](06-authentication.md)
