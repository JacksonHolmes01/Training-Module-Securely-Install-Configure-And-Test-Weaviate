# Export / Download Data

In this section, you will learn how to **export data from Weaviate**.

This is an important operational skill. A secure system is not just about:
- installing correctly
- enforcing authentication
- restricting write access

It must also support:

- auditing
- migration
- compliance review
- backup validation
- incident investigation
- portability between environments

Exporting data proves that:
- objects are actually stored
- authentication protects access
- you can retrieve and preserve records outside the system

---

## Before You Begin

Make sure:

1. Weaviate is running:
   ```bash
   docker ps
   ```

2. The `Note` collection exists:
   ```bash
   curl -s http://localhost:8080/v1/schema \
     -H "Authorization: Bearer admin-key-123"
   ```

3. You have inserted test objects in the previous section.

If these are not true, complete **Create Test Data** first.

---

# Step 1 — Export All Notes to a Local JSON File

This command retrieves objects and saves them to a file on your machine.

```bash
curl -s "http://localhost:8080/v1/objects?class=Note&limit=100" \
  -H "Authorization: Bearer admin-key-123" \
  -o notes_export.json
```

---

## What This Command Does

- `GET /v1/objects` retrieves stored objects
- `class=Note` filters to the Note collection
- `limit=100` caps how many objects are returned
- `-o notes_export.json` writes the result to a file

---

## What Success Looks Like

After running the command, list files:

```bash
ls
```

You should see:

```
notes_export.json
```

Open it:

```bash
cat notes_export.json
```

You should see JSON containing your inserted notes.

This confirms:
- data is retrievable
- API authentication works
- data can be exported locally

---

# Step 2 — Pretty Print the JSON (Optional but Recommended)

Raw JSON can be difficult to read.

If you have `jq` installed:

```bash
cat notes_export.json | jq
```

If you do not have `jq`, you can install it:

### macOS (Homebrew)
```bash
brew install jq
```

### Ubuntu / Debian
```bash
sudo apt install jq
```

Or open the file in:
- VS Code
- Any text editor
- A browser

---

# Step 3 — Test Viewer Export Permissions

Now confirm RBAC behavior.

Viewer should be able to **read** but not **write**.

```bash
curl -s "http://localhost:8080/v1/objects?class=Note&limit=100" \
  -H "Authorization: Bearer viewer-key-123"
```

If RBAC is configured correctly:
- This should return JSON results.

If it fails with `403 Forbidden`, your RBAC role may not include read permissions.

---

# Step 4 — Filtered Export (Selective Retrieval)

Instead of exporting everything, you can filter results.

Example: retrieve only notes containing the word “secure”.

```bash
curl -s "http://localhost:8080/v1/graphql" \
  -H "Authorization: Bearer admin-key-123" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "{ Get { Note(where: { path: [\"text\"], operator: Like, valueText: \"*secure*\" }) { text } } }"
  }'
```

This demonstrates:
- targeted extraction
- controlled querying
- selective retrieval

In real environments, this supports:
- audits
- legal discovery
- compliance filtering
- investigation workflows

---

# Step 5 — Export vs Backup (Important Distinction)

It is critical to understand the difference between **exporting data** and performing a **backup**.

| Export | Backup |
|--------|--------|
| Retrieves JSON via API | Snapshots internal storage |
| Human-readable | Storage-level restore |
| Selective | Entire collection/system |
| Used for audits/migration | Used for disaster recovery |

Export:
- operates at the API level
- respects authentication and RBAC
- is ideal for portability and inspection

Backup:
- operates at the storage layer
- is used for full system recovery
- preserves internal indexes and metadata

Both are required in a secure production system.

---

# Step 6 — Why This Matters for Secure Systems

By completing this section, you have proven:

- Data can be retrieved securely
- API keys protect export access
- RBAC controls who can read
- The system supports portability
- You can generate compliance artifacts

You now understand the **full lifecycle**:

1. Install securely
2. Configure authentication
3. Enforce authorization
4. Insert data
5. Export data
6. Back up data

That is a complete operational security workflow.

---

Next: [Backups](09-backups.md)
