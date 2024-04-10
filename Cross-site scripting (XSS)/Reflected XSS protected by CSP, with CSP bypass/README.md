## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5dddf7ac-d374-4abe-9dd6-e52bdaf84fbc)

## Solution :

Enter the following Payload the search box:

```html
<img src=1 onerror=alert()>
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/84faef2c-5ae2-4ae2-840c-8a2119f01e73)

Observe that the payload is reflected, but the CSP prevents the script from executing.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ed8fa7d7-7356-4bb1-a1d3-f5302c95a36f)

In Burp Proxy, observe that the response contains a Content-Security-Policy header, and the report-uri directive contains a parameter called token. Because you can control the token parameter, you can inject your own CSP directives into the policy.

Payload will be-

```html
https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cscript%3Ealert%281%29%3C%2Fscript%3E&token=;script-src-elem%20%27unsafe-inline%27
```

>The injection uses the script-src-elem directive in CSP. This directive allows you to target just script elements. Using this directive, you can overwrite existing script-src rules enabling you to inject unsafe-inline, which allows you to use inline scripts.

it will triger an alert pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5e453915-95f3-4552-92cf-12514432dd20)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8b6c825b-2242-4fe4-a740-1ac6d385acd2)
