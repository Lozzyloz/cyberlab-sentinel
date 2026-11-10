
# CyberLab Sentinel — API Reconnaissance Inventory

## 1. Assessment Information

- **Project:** CyberLab Sentinel
- **Target:** OWASP Juice Shop
- **Target URL:** http://127.0.0.1:3000
- **Assessment Type:** API Reconnaissance
- **Date:** 10 November 2026
- **Environment:** Kali Linux, Firefox Developer Tools and Docker
- **Authorization:** Locally hosted application owned and controlled by this project.

## 2. Assessment Objective

The objective was to identify an application API endpoint, examine its HTTP request and response, and document the information returned by the endpoint.

## 3. Identified API Endpoint

| Property | Observation |
|---|---|
| Endpoint | `/api/Quantitys/` |
| HTTP Method | GET |
| Host | 127.0.0.1:3000 |
| Expected Response Format | JSON |
| Browser Status Code | 304 Not Modified |
| Records Returned | 56 |
| Request Type | Fetch/XHR |

## 4. Response Structure

The API response contained:

- `status`: success
- `data`: An array containing 56 records.

Each inspected record contained the following fields:

| Field | Description |
|---|---|
| ProductId | Associated product identifier |
| id | Quantity record identifier |
| quantity | Recorded product quantity |
| limitPerUser | Per-user purchase limit value |
| createdAt | Record creation timestamp |
| updatedAt | Last update timestamp |

## 5. Sample Response Observations

### Record 1

| Field | Value |
|---|---|
| ProductId | 1 |
| id | 1 |
| quantity | 70 |
| limitPerUser | 5 |

### Record 2

| Field | Value |
|---|---|
| ProductId | 2 |
| id | 2 |
| quantity | 40 |
| limitPerUser | null |

Both records contained creation and update timestamps.

## 6. Preliminary Security Observations

### 6.1 Inventory Information Exposure

The observed response contains product identifiers and quantity information.

Further investigation is required to determine whether this information is intended to be publicly accessible and whether it presents a business or security risk.

### 6.2 Purchase Limit Handling

The `limitPerUser` field contains different values across the two inspected records.

The second record contains a null value. Its meaning and impact require examination of the application's server-side purchase-limit logic.

### 6.3 Request Headers

The browser request included a custom `X-User-Email` header.

Its purpose and handling require further investigation. Its value has been excluded from this report.

## 7. Evidence and Limitations

The endpoint was examined using Firefox Developer Tools.


The browser displayed a 304 Not Modified response while showing the response data. This indicates that cached response content was available.

Only two of the 56 records were inspected in detail.

Authentication requirements, authorization controls, and server-side enforcement have not yet been verified.

No confirmed vulnerabilities are claimed.

## 8. Recommended Next Steps

1. Inspect additional API endpoints.
2. Determine whether the quantity endpoint requires authentication.
3. Investigate the purpose of the custom request header.
4. Review purchase-limit enforcement.
5. Compare API behavior under different application states.
6. Document and validate any potential security weaknesses.

## 9. Conclusion

The reconnaissance identified an API endpoint that returns product quantity records and related purchase-limit information.

The findings establish an initial understanding of the application's API structure and provide a foundation for further controlled security testing.
