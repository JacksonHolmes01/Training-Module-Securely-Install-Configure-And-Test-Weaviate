# Create Test Data

```bash
curl -X POST http://localhost:8080/v1/schema \
  -H "Authorization: Bearer admin-key-123" \
  -H "Content-Type: application/json" \
  -d '{
    "classes": [
      {
        "class": "Note",
        "vectorizer": "none",
        "properties": [
          { "name": "text", "dataType": ["text"] }
        ]
      }
    ]
  }'
```

Next: [Backups](09-backups.md)
