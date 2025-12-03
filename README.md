# Native Auth HTTP API Examples

This repository demonstrates how to use **Microsoft Entra External ID Native Authentication APIs** directly via HTTP requests, without using the MSAL Native Auth SDK.

## Overview

Native Authentication provides a streamlined authentication experience for mobile and desktop applications. While the MSAL Native Auth SDK simplifies integration, understanding the underlying HTTP API calls is valuable for:

- Custom implementations in languages/platforms without SDK support
- Debugging and troubleshooting authentication flows
- Understanding the authentication process at a protocol level
- Testing and API exploration during development

## What's Included

This repository contains REST Client (`.http`) files demonstrating three core authentication flows:

### 🔐 [Sign-Up Flow](tests/sign-up.http)
- Email + Password registration
- Email OTP (One-Time Passcode) registration
- User attribute collection (built-in and custom extension attributes)
- Multiple flow variations and error scenarios

### 🔑 [Sign-In Flow](tests/sign-in.http)
- Password-based authentication
- Email OTP authentication
- Token refresh mechanism
- Scope management and token handling

### 🔄 [Self-Service Password Reset (SSPR)](tests/sspr.http)
- Complete password reset flow
- OTP verification
- Polling mechanism for reset completion
- Optional immediate sign-in after reset

## Key Concepts Demonstrated

### Continuation Tokens
Each flow uses continuation tokens to maintain state across multiple API calls. These tokens:
- Progress sequentially through authentication steps
- Have limited lifetimes and are typically one-time use
- Maintain session state without requiring client-side storage

### Challenge Types
The API supports multiple authentication methods:
- **`oob`** - Out-of-Band (Email OTP)
- **`password`** - Password authentication
- **`redirect`** - Browser-based fallback (always required)

### Web Fallback (Browser Redirect)
When Entra ID returns `{"challenge_type": "redirect"}`, the app must switch to browser-based authentication using MSAL. This happens when:
- Tenant requires MFA (Multi-Factor Authentication)
- Authentication methods not supported by app (SMS OTP, Authenticator app, FIDO2)
- Conditional Access policies require browser-based auth
- Social identity providers or federated domains
- Enhanced security verification needed

Each flow file includes examples of redirect scenarios and implementation guidance.

### Token Types
- **Access Token** - Short-lived JWT for API authorization
- **Refresh Token** - Long-lived token for obtaining new access tokens
- **ID Token** - JWT containing user identity claims

## Configuration

Before using these examples, update the variables in each `.http` file:

```http
@tenant_subdomain = your-tenant
@tenant_domain = your-tenant.onmicrosoft.com
@client_id = your-app-client-id
@username = test-user@example.com
@password = YourSecurePassword123!
```

## Prerequisites

- **Microsoft Entra External ID tenant** with Native Authentication enabled
- **Application registration** configured for Native Authentication
- **REST Client extension** for VS Code (recommended) or any HTTP client

## Usage

1. Open any `.http` file in VS Code with the REST Client extension
2. Update the variables at the top of the file with your tenant and app details
3. Click "Send Request" above any HTTP request
4. Follow the flow sequentially - each step uses the continuation token from the previous step
5. For OTP flows, manually replace `YOUR_OTP_CODE` with the code received via email

## Flow Examples

### Basic Sign-Up Flow
```
POST /signup/v1.0/start          → continuation_token_1
POST /signup/v1.0/challenge      → continuation_token_2 (OTP sent)
POST /signup/v1.0/continue       → continuation_token_3 (OTP verified)
POST /signup/v1.0/challenge      → continuation_token_4 (password challenge)
POST /signup/v1.0/continue       → continuation_token_5 (password submitted)
POST /oauth2/v2.0/token          → access_token, refresh_token, id_token
```

### Basic Sign-In Flow
```
POST /oauth2/v2.0/initiate       → continuation_token_1
POST /oauth2/v2.0/challenge      → continuation_token_2
POST /oauth2/v2.0/token          → access_token, refresh_token, id_token
```

### SSPR Flow
```
POST /resetpassword/v1.0/start          → continuation_token_1
POST /resetpassword/v1.0/challenge      → continuation_token_2 (OTP sent)
POST /resetpassword/v1.0/continue       → continuation_token_3 (OTP verified)
POST /resetpassword/v1.0/submit         → continuation_token_4 (new password)
POST /resetpassword/v1.0/poll_completion → continuation_token_5 (poll until succeeded)
```

## Error Scenarios

Each file includes common error scenarios:
- Invalid credentials
- Expired tokens
- User not found / already exists
- Password policy violations
- Invalid OTP codes
- Missing required attributes
- **Web fallback redirect** - When browser-based auth is required

## Documentation

For official Microsoft documentation on Native Authentication APIs, see:
- [Microsoft Entra External ID Native Authentication Overview](https://learn.microsoft.com/entra/external-id/customers/concept-native-authentication)
- [Native Authentication API Reference](https://learn.microsoft.com/entra/external-id/customers/reference-native-authentication-api)

## Why Use HTTP APIs Directly?

While the MSAL Native Auth SDK is recommended for production applications, using the HTTP APIs directly offers:

✅ **Educational Value** - Understand authentication protocols at a deeper level  
✅ **Platform Flexibility** - Implement in any language or framework  
✅ **Debugging** - Troubleshoot SDK issues by examining raw HTTP traffic  
✅ **Customization** - Build custom flows not supported by the SDK  
✅ **Testing** - Validate API behavior and test edge cases

## Contributing

Feel free to submit issues or pull requests to improve these examples.

## License

MIT License - See LICENSE file for details

---

**Note**: These examples are for educational and testing purposes. For production applications, consider using the official MSAL Native Auth SDK which handles token management, caching, and security best practices automatically.
