# Identity & Access Management Protocols

This repository contains comprehensive documentation and resources explaining the core authentication and authorization protocols: **SAML**, **OAuth 2.0**, and **OpenID Connect (OIDC)**.

---

## 🎯 Overview

Three main protocols dominate modern identity and access management:

| Protocol | Primary Purpose | Key Use Case | Core Concept |
|----------|----------------|--------------|-------------|
| **SAML 2.0** | **Authentication (AuthN)** | Enterprise SSO | XML-based identity assertions |
| **OAuth 2.0** | **Authorization (AuthZ)** | API Access Delegation | Token-based resource access |
| **OpenID Connect (OIDC)** | **Authentication (AuthN)** | Consumer/Modern SSO | Identity layer on OAuth 2.0 |

---

## 🔐 What's the Difference?

### The Core Distinction

**Authentication vs. Authorization:**
- **Authentication (AuthN)**: "Who are you?" - Verifying user identity
- **Authorization (AuthZ)**: "What are you allowed to do?" - Granting permissions to resources

---

## 📋 Protocol Deep Dive

### 1. SAML (Security Assertion Markup Language)

**What It Is:**
SAML is a widely applicable authentication protocol used primarily in enterprise environments for Single Sign-On (SSO).

**Purpose:**
- Enterprise Single Sign-On
- Prove user identity across multiple corporate applications

**Key Characteristics:**
- **Format**: XML-based protocol
- **Binding**: SOAP/HTTP redirect binding
- **Signature**: X.509 certificate validation
- **Token**: SAML Assertion containing authentication statements
- **Flow Types**: SP-initiated and IdP-initiated flows

**How It Works (Simple Example):**
```
Employee → Company Portal → Click Salesforce
    ↓
Salesforce redirects to Company Identity Provider (IdP)
    ↓
Employee logs in at company IdP
    ↓
Company IdP creates & signs SAML Assertion (XML)
    ↓
SAML Assertion sent back to Salesforce
    ↓
Salesforce verifies signature & logs employee in
```

**Use Cases:**
- Accessing company HR systems (Workday)
- Enterprise CRM platforms (Salesforce)
- Cloud applications for employees
- Legacy system integration

**Analogy:**
Think of SAML like your **Company ID Card**. It proves you work there and grants you access to internal systems without needing a separate password for each one.

---

### 2. OAuth 2.0 (Open Authorization)

**What It Is:**
OAuth 2.0 is an authorization framework (not authentication) designed to provide secure delegated access to resources without sharing passwords.

**Purpose:**
- Allow apps to access user resources without password sharing
- Enable secure service-to-service communication
- Provide scope-based, limited-time access

**Key Characteristics:**
- **Format**: RESTful/JSON-based
- **Token Types**: Access Token (for resource access), Refresh Token (for renewing access)
- **Grant Types**: Authorization Code, Client Credentials, Device Code, Implicit, Password
- **Scope-Based**: Granular permission control
- **Separation**: Authorization Server vs Resource Server

**How It Works (Photo App Example):**
```
User → Photo Printing App → "Access your Google Photos"
    ↓
User redirected to Google (Authorization Server)
    ↓
Google shows consent screen: "Allow access to your photos?"
    ↓
User clicks "Allow"
    ↓
Google returns Authorization Code to Photo App
    ↓
Photo App exchanges code for Access Token (server-to-server)
    ↓
Photo App uses Access Token to retrieve photos from Google
    ↓
Photo App prints photos (without ever knowing user's Google password)
```

**Use Cases:**
- Mobile app authorization
- Third-party API access
- Service-to-service authentication
- Delegated access to resources

**Analogy:**
Think of OAuth 2.0 like a **Valet Key**. You give the valet a special key that only starts your car—nothing more. The valet cannot open the glove box or trunk, just drive the car.

---

### 3. OpenID Connect (OIDC)

**What It Is:**
OIDC is an authentication protocol built on top of OAuth 2.0 that adds a standardized identity layer, using JSON Web Tokens (JWTs).

**Purpose:**
- Modern Single Sign-On for consumer and web applications
- Securely verify user identity
- Simplify "Login with..." social login buttons

**Key Characteristics:**
- **Format**: JWT-based (JSON Web Tokens)
- **Built On**: OAuth 2.0
- **ID Token**: Contains user identity claims (name, email, etc.)
- **UserInfo Endpoint**: Additional user profile data
- **Signature**: Cryptographically signed for verification
- **Flow Types**: Authorization Code Flow, Hybrid Flow, Implicit Flow

**How It Works (Sign in with Google Example):**

**Step 1:** User clicks "Sign in with Google"
```
User → News Website → Click "Sign in with Google"
```

**Step 2:** Redirect to Google
```
News Website redirects user to Google's authentication server
```

**Step 3:** Google Authentication
```
Google shows login prompt
User enters credentials
Google verifies credentials
```

**Step 4:** Google Creates & Signs ID Token (JWT)
```json
{
  "iss": "https://accounts.google.com",
  "sub": "1234567890",
  "aud": "news_website_client_id",
  "name": "John Doe",
  "email": "john@example.com",
  "iat": 1516239022,
  "exp": 1516242622
}
```
Google signs this payload with its private key.

**Step 5:** Authorization Code Exchange
```
Google returns Authorization Code to News Website
News Website's server exchanges code for tokens (server-to-server)
Google returns:
  - ID Token (signed JWT with user info)
  - Access Token (for accessing APIs)
```

**Step 6:** Verification
```
News Website verifies ID Token signature using Google's public keys
If valid: Extract user info (name, email)
Create session & log user in
```

**Step 7:** User Logged In
```
User sees: "Welcome, John Doe!"
User is now logged into News Website with Google account
```

**Use Cases:**
- Consumer-facing applications
- Social login functionality ("Login with Google/Facebook")
- Modern web applications
- Mobile app authentication
- API identity verification

**Analogy:**
Think of OIDC like your **Driver's License**. It not only proves who you are (like a valet key proves who can drive), but it also contains verified information about you (name, address, photo). This is perfect for everyday use.

---

## 🔄 SAML vs OAuth 2.0 vs OIDC

### The Official Distinction

**SAML:** A widely applicable authentication protocol
- Handles the function of **granting access**
- Grants to whom? To the authenticated user
- Used in enterprise environments

**OAuth 2.0:** An authorization standard designed for specific applications
- Handles the function of **determining what can/cannot be accessed**
- Determines scope of access
- Used for API and resource delegation

**OIDC:** An authentication protocol built on OAuth 2.0
- Adds a **layer of security to OAuth 2.0**
- Uses JSON Web Tokens (JWTs) to verify user identity
- Enables users to log in with one set of credentials across multiple sites

### Quick Decision Matrix

| Scenario | Use This | Reason |
|----------|----------|--------|
| Employee accessing company Salesforce | **SAML** | Enterprise SSO, internal systems |
| App accessing Google Photos API | **OAuth 2.0** | Authorization & delegation, not identity |
| Website with "Login with Google" button | **OIDC** | Consumer SSO, user identity needed |
| Mobile app syncing with company API | **OIDC** | Modern auth + user verification |
| Third-party service accessing customer data | **OAuth 2.0** | Scope-based delegation |
| Legacy system integration | **SAML** | Enterprise standard, XML support |

---

## 🚀 Real-World Usage Scenarios

### Scenario 1: Enterprise Employee (SAML)

```
Morning routine at TechCorp:

1. Employee boots laptop
2. Logs into company portal with credentials
3. Portal is their Identity Provider (IdP) - e.g., Okta, Azure Entra ID
4. Employee clicks "Salesforce" icon
5. Behind the scenes: SAML assertion is created by IdP
6. Salesforce (Service Provider) receives & verifies SAML assertion
7. Employee is automatically logged into Salesforce ✓

Benefits:
- Single login, access to all corporate apps
- No password reuse across services
- Company controls access policies centrally
- High security with XML signatures
```

### Scenario 2: API Access (OAuth 2.0)

```
Photo App Workflow:

1. User launches Photo Printing App
2. User clicks "Upload from Google Photos"
3. App redirects to Google with specific scopes:
   - Scope: "View your photos"
   - Scope: "Access your drive"
4. User logs into Google (if not already)
5. Google shows: "Photo App wants to access your photos"
6. User clicks "Allow"
7. Google returns Authorization Code
8. Photo App exchanges code for Access Token
9. Photo App uses Access Token to fetch photos
10. Photos uploaded to printing service ✓

Benefits:
- User never shares Google password with Photo App
- Photo App gets limited, time-restricted access
- User can revoke access anytime
- Google can monitor which apps access what data
```

### Scenario 3: Consumer Application (OIDC)

```
Shopping Website Login:

1. User visits NewShoppingStore.com
2. User clicks "Sign in with Google"
3. Redirected to Google's authentication
4. User logs in at Google
5. Google asks: "Allow NewShoppingStore to see your profile?"
6. User clicks "Allow"
7. Google creates ID Token (JWT):
   {
     "name": "Jane Smith",
     "email": "jane@gmail.com",
     "picture": "..."
   }
8. ID Token sent to NewShoppingStore
9. NewShoppingStore verifies signature
10. NewShoppingStore extracts user info
11. User logged in as "Jane Smith" ✓

Benefits:
- No new password to remember
- Automatic account creation
- Trusted identity verification (Google verified the user)
- Basic profile information available
- Simple "Login with..." experience
```

---

## 🛡️ Security Deep Dive

### SAML Security

- **XML Signatures**: Uses X.509 certificates to sign SAML assertions
- **Encryption**: Assertions can be encrypted with certificates
- **Signature Verification**: Service provider verifies signature before trusting assertion
- **Complexity**: Security through comprehensive schema and binding protocols

**Example SAML Assertion:**
```xml
<saml:Assertion>
  <saml:Issuer>https://company-idp.com</saml:Issuer>
  <saml:Subject>
    <saml:NameID>john.doe@company.com</saml:NameID>
  </saml:Subject>
  <saml:AuthnStatement AuthnInstant="2024-01-15T10:00:00Z">
    <saml:AuthnContext>
      <saml:AuthnContextClassRef>
        urn:oasis:names:tc:SAML:2.0:ac:classes:Password
      </saml:AuthnContextClassRef>
    </saml:AuthnContext>
  </saml:AuthnStatement>
  <ds:Signature><!-- Cryptographic Signature --></ds:Signature>
</saml:Assertion>
```

### OAuth 2.0 Security

- **PKCE (Proof Key for Code Exchange)**: Prevents authorization code interception
- **Token Refresh**: Short-lived access tokens, refreshable tokens for long-term access
- **Scope Limitation**: Each access token limited to specific scopes
- **Secure Transport**: Requires HTTPS/TLS
- **No Password Sharing**: Never exposes user credentials to third-party apps

### OIDC Security

- **ID Token Signature**: JWT signed by identity provider, cryptographically verifiable
- **ID Token Claims**: `iss` (issuer), `sub` (subject), `aud` (audience), `iat` (issued at), `exp` (expiration)
- **Nonce Parameter**: Prevents token replay attacks
- **UserInfo Endpoint**: Provides additional user claims with access token
- **Combines OAuth 2.0 + JWT**: Gets both authorization and verified identity

**Example ID Token (JWT):**
```json
Header: {
  "alg": "RS256",
  "kid": "rsa1"
}

Payload: {
  "iss": "https://accounts.google.com",
  "sub": "110169547453986905554",
  "aud": "your-app-client-id.apps.googleusercontent.com",
  "email": "john@example.com",
  "email_verified": true,
  "iat": 1516239022,
  "exp": 1516242622,
  "nonce": "n-0S6_WzA2Mj"
}

Signature: [Cryptographically signed with Google's private key]
```

---

## 🔗 Key Concepts Explained

### JWT (JSON Web Token)

A compact, URL-safe means of representing claims to be transferred between two parties.

**Structure:** `Header.Payload.Signature`

**Example:**
```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9
.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIn0
.signature_here
```

**Why JWTs?**
- Self-contained: No need to store session on server
- Verifiable: Cryptographic signature proves authenticity
- Compact: Easy to transmit via HTTP headers or URL parameters
- Stateless: No database lookup needed to validate

### ID Token vs Access Token (OIDC)

| ID Token | Access Token |
|----------|--------------|
| Contains user identity claims | Contains permissions/scopes |
| Used by app to know who user is | Used by app to access resources |
| For authentication | For authorization |
| Expires quickly (1 hour typical) | May be longer-lived or refreshable |
| Client-focused | Resource server-focused |

### Flows and Grant Types

**SAML Flow:**
- Browser-based redirect flow
- SOAP binding or HTTP binding
- Stateful (session-based)

**OAuth 2.0 Grant Types:**
1. **Authorization Code**: Secure server-to-server exchange (most common)
2. **Implicit**: Browser-only, tokens in URL fragment (deprecated)
3. **Client Credentials**: Service-to-service, no user involved
4. **Device Code**: For devices without browsers
5. **Password**: Legacy, not recommended

**OIDC Flows:**
- **Authorization Code Flow**: Secure, recommended for web/mobile
- **Implicit Flow**: Browser-only, less secure
- **Hybrid Flow**: Combines features of both

---

## 🎯 When to Use Which?

### Use SAML When:

✅ Building enterprise applications  
✅ Integrating with corporate identity providers (Okta, Azure AD, Ping)  
✅ High-security environments requiring XML signatures  
✅ Compliance requirements (HIPAA, SOC 2)  
✅ Internal employee-facing applications  
✅ Legacy system integration  

### Use OAuth 2.0 When:

✅ Need API-level authorization  
✅ Third-party app integration  
✅ Mobile app accessing backend APIs  
✅ Don't need user identity, just resource access  
✅ Service-to-service communication  
✅ Microservices architecture  

### Use OIDC When:

✅ Consumer-facing applications  
✅ Want "Login with Google/Facebook/GitHub"  
✅ Modern web or mobile apps  
✅ Need both authentication and basic user info  
✅ Building new applications from scratch  
✅ Want simplicity with security  

---

## 📚 Architecture Patterns

### Enterprise Pattern (SAML)

```
┌─────────────────────────────────────────┐
│         Employee Workstation            │
└────────────────────┬────────────────────┘
                     │
                     ▼
         ┌───────────────────────┐
         │  Company Portal/IdP    │
         │   (Okta, Azure AD)    │
         └────────────┬──────────┘
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
    Salesforce   Workday      Slack
     (SP)         (SP)         (SP)
     
SAML: One login → Access all corporate apps
```

### API Pattern (OAuth 2.0)

```
┌──────────────────┐
│   Mobile App     │
└────────┬─────────┘
         │
         ▼
┌──────────────────────┐
│  Authorization       │
│  Server (Google)     │
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Resource Server     │
│  (Google APIs)       │
└──────────────────────┘

OAuth: App gets limited, scoped access to resources
```

### Consumer Pattern (OIDC)

```
┌──────────────────┐
│   Web Browser    │
└────────┬─────────┘
         │
         ▼
┌──────────────────────┐
│   Consumer App       │
│  (News Website)      │
└────────┬─────────────┘
         │
         ▼
┌──────────────────────┐
│  Identity Provider   │
│  (Google, Facebook)  │
└──────────────────────┘

OIDC: User login + identity verification + access
```

---

## 📊 Feature Comparison Table

| Feature | SAML | OAuth 2.0 | OIDC |
|---------|------|----------|------|
| **Primary Use** | Authentication | Authorization | Authentication |
| **Token Format** | XML Assertion | Access Token | JWT (ID Token) |
| **Signature Type** | XML Signature (X.509) | Bearer Token | JWT Signature (RS256, HS256) |
| **Transport** | HTTP Redirect, SOAP | HTTP/REST | HTTP/REST |
| **Session Management** | Server-side sessions | Stateless tokens | Stateless tokens |
| **User Identity** | Yes (SAML Assertion) | No (just access) | Yes (ID Token + UserInfo) |
| **Complexity** | High (XML) | Medium | Medium |
| **Learning Curve** | Steep | Moderate | Moderate |
| **Mobile Friendly** | No | Yes | Yes |
| **Modern Apps** | No | Yes | Yes |
| **Enterprise Ready** | Excellent | Good | Good |
| **Standards Body** | OASIS | IETF | OpenID Foundation |
| **Adoption** | Enterprise | Enterprise + Consumer | Consumer + Modern |

---

## 🔄 Common Integration Patterns

### Pattern 1: SAML + OAuth 2.0 + OIDC

A modern organization doesn't choose just one protocol. They support multiple for different use cases:

```
┌────────────────────────────────────────────────┐
│   Central Identity Platform (Okta, Azure AD)   │
└──────────────────┬─────────────────────────────┘
                   │
      ┌────────────┼────────────┐
      │            │            │
      ▼            ▼            ▼
   SAML         OAuth 2.0      OIDC
   (Salesforce) (Mobile API)   (Web App)
   (Workday)    (Third-party)  (Consumer)
   (Slack)      (Microservices) (Social Login)
```

### Pattern 2: Internal + External Identity

```
┌──────────────────────────────────────┐
│   Internal Employees                  │
│   (Corporate IdP - SAML)              │
└─────────────┬────────────────────────┘
              │
    ┌─────────┴─────────┐
    ▼                   ▼
Corporate Apps      Partner Apps
(Salesforce)        (OAuth 2.0)


┌──────────────────────────────────────┐
│   External Users / Customers          │
│   (Public IdP - OIDC)                 │
└─────────────┬────────────────────────┘
              │
    ┌─────────┴─────────┐
    ▼                   ▼
Web Portal        Mobile App
(Login with...)   (Social Login)
```

---

## 💡 Best Practices

### For SAML Implementation:
- Use IdP-initiated or SP-initiated flow consistently
- Implement certificate rotation
- Monitor and audit all authentication attempts
- Use HTTPS for all SAML assertions
- Store certificates securely

### For OAuth 2.0 Implementation:
- Always use authorization code flow (never implicit)
- Implement PKCE for mobile/SPA apps
- Use short-lived access tokens
- Implement refresh token rotation
- Validate scopes carefully

### For OIDC Implementation:
- Verify ID token signature before trusting claims
- Check token expiration (exp claim)
- Implement nonce to prevent replay attacks
- Use secure storage for tokens
- Implement proper logout/token revocation

---

## 📖 Key Takeaways

| Concept | Definition | Example |
|---------|-----------|---------|
| **Authentication** | Verifying who someone is | Logging in with username/password |
| **Authorization** | Granting permission to do something | Allowing app access to your photos |
| **SAML** | XML-based enterprise SSO | Employee accessing Salesforce via company login |
| **OAuth 2.0** | Token-based authorization framework | App requesting access to Google Photos |
| **OIDC** | JWT-based modern authentication | Signing into website with Google account |
| **ID Token** | Verified package of user identity | JWT containing name, email, profile pic |
| **Access Token** | Permission to access resources | Bearer token for API calls |
| **Scope** | Limited permissions for access | "read:photos", "write:profile" |

---

## 📚 Additional Resources

- [SAML 2.0 Specifications](http://saml.xml.org/saml-specifications)
- [OAuth 2.0 RFC 6749](https://tools.ietf.org/html/rfc6749)
- [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html)
- [JWT.io - JWT Debugger](https://jwt.io)
- [OAuth 2.0 Security Best Practices](https://tools.ietf.org/html/draft-ietf-oauth-security-topics)

---

## 🤝 Contributing

This documentation is a living resource. Please contribute corrections, clarifications, or additional examples!

---

**Last Updated**: November 2025  
**Protocol Versions**: SAML 2.0, OAuth 2.0, OpenID Connect 1.0
