# OAuth 2.0

## OAuth Flows

* **Authorization Code Flow** - Code is the key to generate access token to access resource.

* **Client Credentials Flow** - Application authenticate with client id and client secret then generate access token to
  access
  resource.
* **Resource Owner Password Flow** - Directly user enter username and password after successfully authentication access
  token
  will generate.

## What is PKCE - Proof Key for Code Exchange

PKCE generate's two information

* **_Code Verifier_** - App generate Random string called `Code Verifier`.

* **_Code Challenge_** - Hashing `Code Verifier` with `SHA-256` called `Code Challenge`.

> **Code Challenge** is `base64url(sha256(code_verifier))`

## How PKCE Works ?

![img.png](images/pkce1.png)
![img.png](images/pkce2.png)

# Resource

https://youtu.be/DdhJvxztALI?si=R7G7nHmXolLsNSTT

## Authorization Code Flow + PKCE

```mermaid
sequenceDiagram
    autonumber
    participant u as User
    participant c as Client APP <br> (Web or Mobile)
    participant a as Authorization <br> Server
    participant r as Resource Server
    u -->> c: Click Login Button
    c ->> c: <br>
    Note over c: Client generates <br> code_verifier and code_challenge
    c -->> a: make /authorize call for code
    a ->> a: <br>
    Note over a: It will store <br> code_challenge, <br> code_challenge_method,<br> state
    a ->> u: Redirect to login page for user_name and passwd authentication prompt.
    u -->> a: Authenticate and consent completed by User.
    a ->> c: authorization code
    c -->> a: authorization code + code_challenge
    a ->> a: <br>
    Note over a: Validate code_challenge with code_verifier
    a ->> c: ID token and Access Token
    c -->> a: /token request
    c -->> r: Request user data with access_token
    r ->> c: Response.
```

```mermaid
sequenceDiagram
    autonumber
    participant u as User
    participant c as Client App (Web / Mobile)
    participant a as Authorization Server
    participant r as Resource Server
    u -->> c: Click Login
    c ->> c: <br>
    Note over c: Client generates <br> code_verifier and code_challenge<br>Note: Client will store `code_verifier`
    c -->> a: /authorize <br> (code_challenge, code_challenge_method, state)
    a ->> u: Redirect to Login & Consent
    u -->> a: Authenticate & Approve
    a ->> a: Store auth_code + code_challenge
    a -->> c: Redirect with authorization_code
    c -->> a: /token<br> (authorization_code + code_verifier)
    a ->> a: Hash code_verifier<br> Compare with stored code_challenge
    a -->> c: Access Token (+ ID Token if OIDC)
    c -->> r: API request with access_token
    r -->> c: Protected Resource
```

```mermaid
sequenceDiagram
    autonumber
    participant u as User
    participant c as Client App (Web / Mobile)
    participant a as Authorization Server
    participant r as Resource Server
    u -->> c: Click Login
    Note over c: Client generates a high-entropy <br> code_verifier and derives <br> code_challenge using S256
    c ->> c: Generate code_verifier & code_challenge
    c -->> a: /authorize <br> (code_challenge, code_challenge_method, state)
    Note over a: Authorization Server stores <br> code_challenge, method, and state
    a ->> u: Redirect to Login & Consent
    u -->> a: Authenticate & Approve
    Note over a: Authorization code is bound <br> to the original code_challenge
    a ->> a: Store auth_code + code_challenge
    a -->> c: Redirect with authorization_code
    Note over c, a: Client proves possession of <br> code_verifier during token exchange
    c -->> a: /token <br> (authorization_code + code_verifier)
    Note over a: Server hashes code_verifier <br> and compares it with stored <br> code_challenge
    a ->> a: Hash code_verifier <br> Compare with stored code_challenge
    a -->> c: Access Token (+ ID Token if OIDC)
    Note over r: Resource Server validates <br> the access token
    c -->> r: API request with access_token
    r -->> c: Protected Resource
```

## How PKCE is working ? (LLD)

1. User click **Login Button**.
2. Client generate **'code_verifier'** and **'code_challenge'** and store **'code_verifier'** for later use.

**Example: -**

|                    |                                                  |
|--------------------|--------------------------------------------------|
| **Code Verifier**  | 2hevbzj0-ErqW45HhecGzMbQ5RCPyw7xv2h04txtmsFMTBGD |
| **Code Challenge** | aRTFQY9QWPm-8q7VLThoyAoDItONVXXI22SAiPOcQbQ      |

3. Client again **generate random string** for **'state'** parameter, and needs to store for next step.

```url
https://authorization-server.com/authorize?
  response_type=code
  &client_id=h9wqrtqkmq7631p15v-siAwa
  &redirect_uri=https://www.oauth.com/playground/authorization-code-with-pkce.html
  &scope=photo+offline_access
  &state=B3X7B85DxEamQV_L
  &code_challenge=aRTFQY9QWPm-8q7VLThoyAoDItONVXXI22SAiPOcQbQ
  &code_challenge_method=S256
```

The client includes the **'code_challenge'** parameter in this request, which the **authorization server will store and
compare later** during the code exchange step.

### 4️⃣ Verify the state parameter

The user was redirected back to the client with a few additional query parameters in the URL:

  ```url
?state=B3X7B85DxEamQV_L&code=RiIKa-WTQYKgya_esmeuKvUxHbv830Ktdjkoa4e754gHNIl2 
```

The state value isn't strictly necessary here since the PKCE parameters provide CSRF protection themselves. In practice,
if you're sure the OAuth server supports PKCE, you can use the state parameter for application state instead of using it
for CSRF protection.

### 5. Exchange the Authorization Code

Now you're ready to exchange the authorization code for an access token.

The client will build a POST request to the token endpoint with the following parameters:

```curl
POST https://authorization-server.com/token

grant_type=authorization_code
&client_id=h9wqrtqkmq7631p15v-siAwa
&client_secret=bafPE8aCuZsXjw1ZZngwJl9C-uDS93lwVIoyBT4nlh5QP3Gl
&redirect_uri=https://www.oauth.com/playground/authorization-code-with-pkce.html
&code=RiIKa-WTQYKgya_esmeuKvUxHbv830Ktdjkoa4e754gHNIl2
&code_verifier=2hevbzj0-ErqW45HhecGzMbQ5RCPyw7xv2h04txtmsFMTBGD
```

Remember the **'code_verifier'**? You'll need to send that along with the token request. The authorization server will
check whether the verifier matches the challenge that was used in the authorization request. This ensures that a
malicious party that intercepted the authorization code will not be able to use it.

### 6. Token Endpoint Response

Here's the response from the token endpoint! The response includes the access token and refresh token.

```json
{
  "token_type": "Bearer",
  "expires_in": 86400,
  "access_token": "mHAhfrWiJzo5KQ90l1ODvLiTgcpK4XPCTYHBtp5TGlq1efS3wRdNN6EOOByPL_TLobNZkO27",
  "scope": "photo offline_access",
  "refresh_token": "-kGqhwMRBrcaoGrBGCOCY2MI"
}
```

Great! Now your application has an access token, and can use it to make API requests on behalf of the user.

---

## Grant Types

In OAuth 2.0, the term **'grant type'** refers to the way an application gets an access token.

* Authorization Code
* PKCE
* Client Credentials
* Device Token
* Refresh Token

### Authorization Code

The Authorization Code grant type is used by confidential and **public clients to exchange an authorization code** for
an
access token.
