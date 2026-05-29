# Issue: No enforcement of trusted hosts on incoming requests

## Observed behaviour

The application has no built-in mechanism to validate the `Host` header on incoming HTTP requests against a configured allowlist. A request with a spoofed or attacker-controlled `Host` header is accepted and processed without any warning or rejection.

This means that if the application uses the `Host` header to construct URLs — for example, in redirects, password reset links, or any call to `url_for` with `_external=True` — those URLs will reflect the attacker-supplied hostname rather than the legitimate one.

**Example of the problem:**

```
GET /reset-password HTTP/1.1
Host: evil.attacker.com
```

If the application generates a password reset link using the request's host, the resulting email could contain:

```
https://evil.attacker.com/reset-password?token=abc123
```

...which directs the user to an attacker-controlled site.

## Expected behaviour

The application should provide a configuration option — for example, `TRUSTED_HOSTS` — that accepts a list of valid hostnames (and optional ports). When set:

- Any incoming request whose `Host` header does not match the allowlist should be rejected with an appropriate HTTP error response (e.g., 400 Bad Request).
- Requests with a matching `Host` header should pass through unchanged.
- If `TRUSTED_HOSTS` is not configured (empty or unset), all requests should be accepted as before (backwards-compatible default).

## Notes

- The `Host` header check should happen early in request processing, before routing or any view logic runs.
- Subdomains and ports should be handled carefully — consider whether `example.com` should also match `www.example.com`.
- The Werkzeug library (which this framework builds on) may already provide relevant utilities for host validation.
- Existing tests should continue to pass; new tests should cover the rejection case and the passthrough case.
