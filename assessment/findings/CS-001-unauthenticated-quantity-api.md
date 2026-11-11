
# CS-001 — Unauthenticated Access to Product Quantity API

## 1. Finding Information

- **Finding ID:** CS-001
- **Title:** Unauthenticated Access to Product Quantity API
- **Target:** OWASP Juice Shop
- **Endpoint:** GET /api/Quantitys/
- **Category:** Broken Access Control — Potential
- **Assessment Date:** 10 November 2026
- **Status:** Open — Requires impact validation
- **Preliminary Severity:** Informational

## 2. Description

During the security assessment, a direct HTTP GET request was sent to the product quantity API without browser cookies or authentication credentials.

The server returned HTTP 200 OK and a JSON response containing 56 product quantity records.

The response included:
- Product identifiers
- Quantity values
- Per-user purchase limits
- Record creation timestamps
- Record update timestamps

## 3. Reproduction Steps

1. Open a Kali Linux terminal.
2. Send the following request:

   `curl -sS -D /tmp/quantity-headers.txt -o /tmp/quantity-body.json -w 'HTTP Status: %{http_code}\nContent Type: %{content_type}\n' http://127.0.0.1:3000/api/Quantitys/`

3. Observe the HTTP status and response content type.
4. Inspect the saved JSON response.

## 4. Observed Results

| Test | Result |
|---|---|
| Authentication credentials supplied | None |
| HTTP status | 200 OK |
| Content type | application/json |
| API status | success |
| Records returned | 56 |
| First record quantity | 70 |
| First record purchase limit | 5 |

## 5. Evidence

Evidence file:

`assessment/evidence/quantity-api-unauthenticated-response.json`

The evidence contains the response received during the unauthenticated request.

## 6. Security Impact Assessment

The endpoint exposes product quantity and purchase-limit information without requiring authentication in the tested request.

Potential concerns include:
- Unintended disclosure of inventory information.
- Exposure of operational or business-related data.
- Information that could assist an attacker in understanding product availability.

The actual business impact has not been established.

Public access may be intentional. Further investigation is required before classifying this behavior as a vulnerability.

## 7. Severity Assessment

**Preliminary severity: Informational**

This classification is based on the currently demonstrated behavior. No sensitive information exposure, unauthorized modification, or exploitation has been established.

Severity should be reassessed if further evidence demonstrates a security impact.

## 8. Recommended Remediation

If the information is not intended to be public:

1. Apply appropriate server-side authentication and authorization.
2. Restrict access to inventory information according to business requirements.
3. Avoid exposing internal inventory details unnecessarily.
4. Validate access controls on related API endpoints.
5. Retest after implementing changes.

If the information is intentionally public, document that requirement and ensure no sensitive internal fields are exposed.

## 9. Conclusion

The assessment confirmed that the product quantity API returned 56 records without authentication credentials in the tested request.

This behavior has been documented as a preliminary access-control observation. Further validation is necessary to determine whether it represents a security weakness.
