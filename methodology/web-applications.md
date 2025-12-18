---
icon: browser
---

# Web Applications

## CSRF

* Check if the token is present on any form it should be — ONLY Create, Update and Delete forms should have CSRF tokens
* Server checks if the token length is correct - Server checks if parameter is there
* Server accepts empty parameter
* Server accepts responds without CSRF token - Token is not session bound -https://security.love/CSRF-PoC-Genorator/

## JWT

* None-signing algorithm is allowed
* Secret is leaked somewhere
* Server never checks secret
* Secret is easily guessable or brute-forceable -https://jwt.io/
* https://jwt.one/ Open redirect bypass:
* evil.com/expected.com
* Javascript openRedirects
* Hidden link open redirects -?url=evil.com
* Using // to bypass
* https:evil.com (browser might correct this, filter might not catch it)
* /\ to bypass
* %00 to bypass (null byte)
* @ to bypass
* Parameter pollution (adding the same parameter

twice)

## BAC

* Test higher Priv functions should not be able to be executed by lower Priv user —Test ALL user levels — Test with authorise — JS Functions via developer console — Copy and paste of URL IDOR
* Test between ALL tenants (companies hosted on one server/database. Can also be divisions of companies) — Test with authorise — JS Functions via developer console — Copy and paste of URL Captcha bypasses
* Try change request method
* Remove the captcha param from the request - leave param empty
* Fill in random value

## LFI

* Using // to bypass
* /\ to bypass
* \\
* %00 to bypass (null byte)
* @ to bypass
* URL encoding
* double encodings RFI:
* Using // to bypass
* /\ to bypass
* \\
* %00 to bypass (null byte)
* @ to bypass
* URL encoding
* double encodings SQLi:
* ‘“ to trigger — SQLmap '-' ' ' '&' '^' '_' ' or ''-' ' or '' ' ' or ''&' ' or ''^' ' or ''_' "-" " " "&" "^" "_" " or ""-" " or "" " " or ""&" " or ""^" " or ""_" or true-- " or true-- ' or true--

## XXE

* SVG files (images), DOCX/XLSX, SOAP, anything XML that renders
* Blind SSRF, file exfiltration, command exec -

]>

∾

## Template injections (CSTI/SST)

* ${7\*7}
* If resolves, what templating engine
* Try exploit by looking at manuals — URL encode special chars ({}\*) — HTML entities — Double encodings XSS:
* ‘“`><img src=x> into every input field, the moment you register and start using the application "onclick=prompt(8)>"@x.y "onclick=prompt(8)><svg/onload=prompt(8)>"@x.y <image/src/onerror=prompt(8)> <img/src/onerror=prompt(8)> jaVasCript :/*-/*`/_\`/_'/_"/\*\*/(/_ \*/oNcliCk=alert() )//%0D%0A%0d%0a//\</stYle/\</titLe/\</teXtarEa/\</scRipt/--!>\x3csVg/\<sVg/oN loAd=alert()//>\x3e
* Enter a random value into every parameter and look for reflection
* See what context reflection is in
* Craft attack vector based on context — JS — HTML — HTML tag attribute — ... — Url encode — HTML entities — Capital letters — BASE64 encode payload
* CSP might be active — Try bypasses — See what is active and where script can be gotten from — Encode them in base64 — Masquerade script as data

## SSRF

* SSRF against server itself
* SSRF against other servers on the network

## Command injection

* Test every single parameter
* Make a list of commands + command separators for target OS

## Admin panel bypass

* Try referral header
* Easy username/pass
* Directory brute forcing for unprotected pages Deserialization: -Check For Base64 encoded cookies, headers, and payloads. -When decoded, they can look similar to this: O:4:"User":2:{s:8:"username";s:6:"vickie";s:6:"status";s:9:" not admin";}
* Each field is listed with the number of characters that it is, and the data type as one character (ex. s) -Try changing the values in the base64 in burp, then send the request and see if you change things
