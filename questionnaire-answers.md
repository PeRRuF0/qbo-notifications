# Intuit Developer Portal — Questionnaire Answers

**App Name:** qbo-notification
**Developer:** Mario Suclla Consulting

Use this document as a reference when filling out the Intuit Developer Portal. Copy-paste the answers below into each corresponding field.

---

## URLs Reference Table

| Field | Value |
|---|---|
| **Host Domain** | `perruf0.github.io` |
| **EULA URL** | `https://perruf0.github.io/qbo-notifications/eula.html` |
| **Privacy Policy URL** | `https://perruf0.github.io/qbo-notifications/privacy.html` |
| **Launch URL** | `https://biglakeslawncare.app.n8n.cloud/rest/oauth2-credential/callback` |
| **Disconnect URL** | `https://perruf0.github.io/qbo-notifications/disconnect.html` |

---

## App Details Section

### App Description
> Internal automation tool that connects to QuickBooks Online to monitor suspense account balances and unreviewed bank feed transactions. The app runs daily automated queries and delivers formatted summary notifications to a private Slack channel. This is an internal-only tool operated by Mario Suclla Consulting for bookkeeping and financial oversight purposes. There are no public users.

### Category
> Financial Automation / Accounting / Internal Tool

### App Type
> Web Application

### Is this app publicly available?
> No — this is a private app for internal business use only.

---

## App Information Section

### How was your app built?
> You were asked to create this app to get credentials for another platform that integrates with QuickBooks.

### What platform(s) does your app utilize and make API calls from?
> n8n Cloud — a Node.js-based workflow automation platform hosted on cloud infrastructure (AWS). The app runs on n8n Cloud at https://biglakeslawncare.app.n8n.cloud.

### How does your app interact with Intuit product data?
> Read-only access. The app queries account balances (suspense accounts) and bank feed transaction review status via the QBO Accounting API. It does not create, modify, or delete any data in QuickBooks Online.

### Is your app private or will it be publicly available?
> Private — for internal team/business use only. The app will not be listed on the Intuit Marketplace and has no external end users.

### Which types of QuickBooks Online users can use your app?
> All QuickBooks Online subscription levels (Simple Start, Essentials, Plus, Advanced). However, only 2–3 company files managed by Mario Suclla Consulting will be connected.

### Does your app integrate with platforms beyond Intuit?
> Yes — Slack (for delivering notification messages to a private internal channel).

---

## Authorization & Authentication Section

### Have you tested connect, disconnect, and reconnect in sandbox?
> Yes. The OAuth 2.0 connect, disconnect, and reconnect flows have been tested in the Intuit sandbox environment.

### How frequently does your app refresh access tokens?
> Access tokens are refreshed before expiry (approximately every 55 minutes). Refresh tokens are renewed before their 100-day expiry. Token refresh is handled automatically by n8n Cloud's credential management system.

### Does your app retry failed authorization requests?
> Yes. n8n Cloud provides automatic retry with exponential backoff for failed HTTP requests, including authorization-related failures.

### Does your app request reconnection on authorization errors?
> Yes. When a token refresh fails, the operator is alerted via Slack notification to manually re-authorize the connection through n8n Cloud.

### Does your app use the Intuit discovery document to resolve endpoints?
> Yes. Endpoints are resolved via the OpenID Connect discovery document provided by Intuit.

### How does your app handle these scenarios: token expiry, token revocation, concurrent requests?
> - **Expired access tokens:** Trigger automatic refresh via n8n Cloud's built-in OAuth2 token management.
> - **Expired refresh tokens:** Trigger a Slack alert to the operator for manual re-authorization through the n8n Cloud credential interface.
> - **Revoked tokens:** Handled the same as expired refresh tokens — operator is notified to re-authorize.
> - **Concurrent requests:** Not applicable — the app runs a single-threaded daily execution cycle (one query per company, sequentially). There are no concurrent token requests.

### Does your app rely on the OAuth 2.0 Playground for production tokens?
> No. Production tokens are managed entirely through n8n Cloud's encrypted credential system.

---

## API Usage Section

### Which API categories does your app use?
> Accounting API only.

### What is the API call frequency per customer?
> Approximately 2–3 API calls per company per day (one daily execution cycle). With 2–3 connected companies, the total is approximately 4–9 API calls per day.

---

## Accounting API Section

### Which QuickBooks Online versions is your app compatible with?
> Compatible with all QuickBooks Online subscription levels: Simple Start, Essentials, Plus, and Advanced.

### How does your app handle version-specific feature changes?
> Not applicable. This is an internal-use app where the operator controls which companies are connected. The app queries standard Account and Transaction entities available across all QBO versions.

### Which features does your app use?
> - Query API: Account entity (to retrieve suspense account balances)
> - Query API: Transaction queries (to identify unreviewed bank feed items)
> - Read-only access only — no create, update, or delete operations

### Does your app use webhooks?
> No. The app uses a daily polling pattern, which is sufficient for this use case.

### Does your app use Change Data Capture (CDC)?
> No.

---

## Error Handling Section

### Has your app been tested for error handling?
> Yes. Error handling has been tested in the sandbox environment, including scenarios for invalid tokens, rate limit responses (HTTP 429), and malformed queries.

### Does your app capture the intuit_tid header field?
> Yes. The intuit_tid is captured in n8n Cloud execution logs via HTTP response headers for support and debugging purposes.

### Does your app have an error logging mechanism?
> Yes. n8n Cloud maintains detailed execution logs with full request/response data, including HTTP status codes, response headers, and error messages.

### Is customer support accessible?
> Yes. The sole user/operator can be reached via email at mario@mariosucllaconsulting.com. Since this is an internal-only tool, "customer support" is self-service by the operator.

---

## Security Section

### Has your company experienced any security breaches?
> No.

### Does your company have security breach notification procedures?
> Not applicable — sole operator with no external users or customers. In the event of a credential compromise, affected OAuth tokens would be revoked immediately and connections re-authorized.

### Does your company have a vulnerability assessment process or security team?
> The sole operator performs regular security reviews of credentials, access permissions, and n8n Cloud workflow configurations.

### How are client credentials (Client ID and Client Secret) stored?
> Client ID and Client Secret are stored in n8n Cloud's encrypted credential store. They are never committed to code repositories, stored in plaintext, or exposed in browser console or client-side code.

### Is multi-factor authentication (MFA) enabled?
> Yes. MFA is enabled on both the Intuit Developer account and the n8n Cloud account.

### Does your app use Captcha or bot detection?
> Not applicable. There is no public-facing authentication flow or user interface. The app runs as a server-side automated workflow.

### Does your app use WebSockets?
> No.

### Is customer data shown to anyone beyond the customer?
> No. All data is used internally only. Slack notifications are delivered to a private internal channel accessible only by the operator. No QBO data is shared with, disclosed to, or made accessible by any third party.

---

## Regulated Industries Section

### Does your app serve regulated industries (financial services, insurance, healthcare)?
> The app is used internally by a bookkeeping and fractional CFO consulting practice. It does not process payments, handle lending, provide insurance, or serve as a financial product. It monitors QuickBooks Online account data for operational awareness and client service purposes only.

### Does your app offer insurance products or services?
> No.

---

## Additional Notes for Intuit Review

- This app is functionally identical in purpose to my existing approved app (GreenBizKPI) on the same developer account — both are internal automation tools for QBO data monitoring.
- The app accesses only 2–3 QBO company files, all of which are managed by Mario Suclla Consulting.
- No data is sold, shared, or disclosed to any third party.
- The app has no user interface — it is a server-side workflow running on n8n Cloud that delivers results via Slack.
