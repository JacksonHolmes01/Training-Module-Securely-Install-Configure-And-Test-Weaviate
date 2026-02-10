# Authorization (RBAC)

## Admin vs Viewer test

Viewer attempting schema write (should fail):

```bash
curl -i -X POST http://localhost:8080/v1/schema \
  -H "Authorization: Bearer viewer-key-123" \
  -H "Content-Type: application/json" \
  -d '{"classes":[{"class":"FailTest","vectorizer":"none"}]}'
```

Admin attempting schema write (should succeed):

```bash
curl -i -X POST http://localhost:8080/v1/schema \
  -H "Authorization: Bearer admin-key-123" \
  -H "Content-Type: application/json" \
  -d '{"classes":[{"class":"Note","vectorizer":"none"}]}'
```

Next: [Create Test Data](08-create-test-data.md)
