
## 1. Cookies

- **What it is**  
    Small pieces of data (key–value pairs) that browsers store and automatically send to the server with every HTTP request matching the cookie’s domain/path.
    
- **Key Characteristics**
    
    |Feature|Details|
    |---|---|
    |Size limit|~4 KB per cookie|
    |Lifetime|Either “session” (deleted when browser closes) or persistent (expires at a specified date)|
    |Scope|Domain + path; can be restricted to subdomains|
    |Accessibility|JavaScript (via `document.cookie`) unless marked `HttpOnly` (inaccessible to JS)|
    |Security flags|`Secure` (HTTPS only), `HttpOnly` (no JS access), `SameSite` (controls cross-site sending)|
    |Sent to server?|✔ Automatically on matching requests|
    
- **Typical Use Cases**
    
    - Session authentication (e.g. session IDs)
        
    - CSRF tokens
        
    - Very small user preferences that the server needs (e.g. “dark mode” flag)
        

```js
// Set a 7-day, HttpOnly, Secure cookie
document.cookie = [
  'sessionId=abc123',
  'Path=/',
  'Expires=' + new Date(Date.now()+7*24*60*60e3).toUTCString(),
  'Secure',
  'HttpOnly',
  'SameSite=Strict'
].join('; ');
```

---

## 2. Session Storage

- **What it is**  
    Part of the Web Storage API: stores data (key–value) **per tab (or window)**, cleared when that tab/window closes.
    
- **Key Characteristics**
    
    |Feature|Details|
    |---|---|
    |Size limit|~5 MB per origin|
    |Lifetime|Until the tab/window is closed|
    |Scope|One origin per tab; not shared across tabs|
    |Accessibility|JavaScript only (`window.sessionStorage`)|
    |Sent to server?|✘ Not sent automatically|
    
- **Typical Use Cases**
    
    - Multi-step forms (store progress per session)
        
    - Temporary state that you don’t want to persist (e.g. a draft message)
        
    - Data isolated per tab (e.g. a temporary shopping cart in a pop-up)
        

```js
// Save user’s progress
sessionStorage.setItem('formStep', '2');
// Retrieve it later
let step = sessionStorage.getItem('formStep');
// Remove when done
sessionStorage.removeItem('formStep');
// Or clear entire session storage
sessionStorage.clear();
```

---

## 3. Local Storage

- **What it is**  
    Part of the Web Storage API: stores data (key–value) **indefinitely** (until explicitly cleared) **per origin**.
    
- **Key Characteristics**
    
    |Feature|Details|
    |---|---|
    |Size limit|~5 MB per origin|
    |Lifetime|Persistent across browser restarts|
    |Scope|Shared by all tabs/windows on the same origin|
    |Accessibility|JavaScript only (`window.localStorage`)|
    |Sent to server?|✘ Not sent automatically|
    
- **Typical Use Cases**
    
    - User preferences (theme, language)
        
    - Caching large, non-sensitive data client-side (e.g. lookup tables)
        
    - Feature flags or A/B test assignments
        

```js
// Save user preference
localStorage.setItem('theme', 'dark');
// Later…
const theme = localStorage.getItem('theme');
// Remove it
localStorage.removeItem('theme');
// Or wipe all localStorage
localStorage.clear();
```

---

## 4. At-a-Glance Comparison

|Feature|Cookies|Session Storage|Local Storage|
|---|---|---|---|
|Storage size|~4 KB per cookie|~5 MB per origin|~5 MB per origin|
|Persistence|Session or expires date|Until tab/window close|Until explicitly cleared|
|Scope|Domain + path|Origin + tab/window|Origin (all tabs)|
|Accessibility to JS|✔ unless `HttpOnly`|✔|✔|
|Sent to server automatically|✔|✘|✘|
|Security considerations|Vulnerable to CSRF if mis-used; cookie flags mitigate risks|Vulnerable to XSS – JS only|Vulnerable to XSS – JS only|

---

## 5. When to Use Which

1. **Cookies**
    
    - ✔ You need the data on the **server side** (e.g. authentication).
        
    - ✔ You want automatic inclusion in HTTP requests.
        
    - ⚠️ Keep them small and use flags (`HttpOnly`, `Secure`, `SameSite`) to mitigate security risks.
        
2. **Session Storage**
    
    - ✔ You need **temporary** state per tab (e.g. wizard steps, transient data).
        
    - ✔ You don’t want data to persist beyond the tab session.
        
    - ⚠️ Not suitable if multiple tabs/windows need to share the same state.
        
3. **Local Storage**
    
    - ✔ You need **persistent**, client-only data across sessions (e.g. user settings).
        
    - ✔ You need more than a few kilobytes (up to ~5 MB).
        
    - ⚠️ Not for sensitive data or anything you don’t want exposed to potential XSS attacks.
        

---

### Security Tips

- **Avoid storing secrets** (access tokens, passwords) in Web Storage—use secure, HttpOnly cookies or other secure vaults.
    
- **Always sanitize** any data you place into or read from storage to guard against XSS.
    
- **Use cookie flags** (`HttpOnly`, `Secure`, `SameSite`) whenever you store tokens or session identifiers in cookies.
    
