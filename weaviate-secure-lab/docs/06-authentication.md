# Authentication (API Keys)

In the previous step, you verified that Weaviate enforces authentication by testing access to the `/v1/meta` endpoint.

That test answered a basic question:

> **Is authentication enabled at all?**

In this step, we go one level deeper.

We will verify that authentication is enforced not just for metadata, but for **sensitive, state-affecting endpoints**.

---

## Why we test authentication again

Not all API endpoints carry the same risk.

- `/v1/meta` exposes instance metadata
- `/v1/schema` controls how data is structured and stored

Access to the schema determines:
- what data can be stored
- how it is indexed
- how queries behave

Because schema access is more sensitive, it is important to confirm that:
- unauthenticated users cannot access it
- authenticated users can access it
- authentication is enforced consistently across the API

This ensures there are no “partial security” gaps.

---

## What this test is validating

This step verifies that:

- authentication is **not limited to a single endpoint**
- security controls apply uniformly
- higher-impact operations require valid credentials

A system that protects metadata but exposes schema control would still be insecure.

---

## Test access to the schema without an API key (expected to fail)

Run the following command **without authentication**:

```bash
curl -i http://localhost:8080/v1/schema
```

### What success looks like (failure is expected)

You should see an HTTP response similar to:

```
HTTP/1.1 401 Unauthorized
```

This confirms that:
- schema access is protected
- unauthenticated users cannot inspect or modify structure
- authentication enforcement is consistent

If this request succeeds, the system is misconfigured and should not be used.

---

## Test access to the schema with a valid API key (expected to succeed)

Now repeat the same request using a valid API key.

Run:

```bash
curl -s http://localhost:8080/v1/schema \
  -H "Authorization: Bearer admin-key-123"
```

### What success looks like

You should receive a JSON response.

Even if no schema has been defined yet, the request should:
- return structured JSON
- not return a 401 error
- indicate authenticated access

This confirms that:
- authentication applies to sensitive endpoints
- valid credentials allow controlled access
- the API behaves consistently across endpoints

---

## How this differs from authorization

At this point, Weaviate knows **who** you are.

What it does **not** yet enforce is **what you are allowed to do**.

Right now:
- any authenticated user with a valid key can access the schema
- permissions are not yet restricted by role

The next step introduces **authorization**, which limits actions even among authenticated users.

---

Next: [Authorization (RBAC)](07-authorization-rbac.md)
