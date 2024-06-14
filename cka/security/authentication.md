# Authentication

## Accounts
- User [Admins & Users]
- Service Accounts [Bots]
  - Create service accounts and manage them
  - ```bash
    kubectl create serviceaccount my-service-account
    ```
  - ```bash
    kubectl list serviceaccount
    ```

## Users (Authentication)

- Authentication echaniss or users are
  1. Static Password File
  2. Static Token File
  3. Certificates
  4. Identity Services