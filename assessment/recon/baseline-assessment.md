# CyberLab Sentinel — Baseline Reconnaissance Report

## 1. Assessment Information

- **Project:** CyberLab Sentinel
- **Target:** OWASP Juice Shop
- **Target URL:** http://127.0.0.1:3000
- **Assessment Type:** Initial Web Application Reconnaissance
- **Date:** 7 November 2026
- **Environment:** Kali Linux with Docker
- **Authorization:** Locally hosted application owned and controlled by this project.

## 2. Assessment Objective

The objective of this initial assessment was to examine the application's HTTP response, identify observable security-related headers, and establish a baseline for further security testing.

## 3. Methodology

The following command was used:

`curl -sS -D assessment/recon/homepage-headers.txt -o /dev/null http://127.0.0.1:3000/`

The command retrieved the HTTP response headers and saved them as evidence.

## 4. Observations

| Observation | Result |
|---|---|
| HTTP response status | 200 OK |
| CORS policy | Access-Control-Allow-Origin: * |
| MIME sniffing protection | X-Content-Type-Options: nosniff |
| Clickjacking protection | X-Frame-Options: SAMEORIGIN |
| Content Security Policy | Not observed |
| HSTS | Not observed |
| Content type | text/html; charset=UTF-8 |
| Application-specific header | X-Recruiting: /#/jobs |

## 5. Preliminary Security Analysis

### 5.1 Cross-Origin Resource Sharing

The application returned `Access-Control-Allow-Origin: *`.

This indicates that the response permits cross-origin access under the browser's CORS rules. Further investigation is required to determine whether sensitive resources are exposed.

### 5.2 Security Headers

The response included X-Content-Type-Options and X-Frame-Options, which provide useful browser-side protections.

A Content-Security-Policy header was not observed in the homepage response. This should be investigated further.

### 5.3 HTTP Strict Transport Security

An HSTS header was not observed. However, the application is currently accessed through local HTTP rather than HTTPS. This observation is not classified as a confirmed vulnerability.

## 6. Evidence

Raw HTTP response headers:

`assessment/recon/homepage-headers.txt`

## 7. Limitations

This assessment examined the homepage's HTTP response headers only.

It did not establish whether the application contains exploitable vulnerabilities, whether all API endpoints use the same policies, or whether sensitive information can be accessed.

## 8. Next Steps

1. Map the application's accessible routes and functionality.
2. Examine application API endpoints.
3. Investigate the CORS configuration.
4. Review additional security headers and browser protections.
5. Begin controlled vulnerability assessment.

## 9. Conclusion

The initial reconnaissance successfully established a baseline of the OWASP Juice Shop homepage's HTTP response behavior.

The observations provide a foundation for deeper security testing. No confirmed vulnerabilities are claimed at this stage.
