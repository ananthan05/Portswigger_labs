## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/137d285a-416f-4aab-9a50-18b923e777af)

## Solution :

> A Reflected Cross-Site Scripting (XSS) vulnerability in the canonical link tag refers to an attack where an attacker injects malicious code into
 the URL parameter of the canonical link tag, leading to the execution of the injected code when the browser renders the URL.

> The canonical link tag is used to specify the preferred URL for a webpage to search engines, helping to prevent duplicate content issues.
>It is commonly implemented in the HTML head section using the following format:


``` html
<link rel="canonical" href="https://example.com/page" />
```
>However, if the URL parameter of the canonical link tag is not properly validated or sanitized, it can be vulnerable to XSS attacks. An attacker can craft a malicious URL that includes JavaScript code,
 which will be executed by the victim’s browser when the page is loaded.
>FOR example.

```html
<link rel="canonical" href="https://example.com/page?param=<script>alert()</script>" />
```

>When the victim visits the page, the JavaScript code within the URL parameter will be executed, leading to an XSS attack. This can allow the attacker to steal sensitive information,
perform actions on behalf of the victim, or deface the website.


To begin, we need to identify potential injection points. Upon analyzing the application, we observe that there is no search functionality.

However, upon opening the dev tools, we discover that the URL is reflected in a head link tag.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/514fc41e-5c0a-4795-b67e-508be2ba5510)

So we have a link tag that we can inject XSS payloads on, so let’s try to escape the href attribute and add an onclick event.

Payload will be.

```html
<link rel="canonical" href="https://0a36007f03cab26381eccce7006700ef.web-security-academy.net/?'onclick='alert()"
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3753c9e4-aa31-47d0-ba70-8d1ed431426e)

Not reflected in the web page.

This event is going to be fired if the element is not visible on the page by  using `html accesskeys`

>HTML AccessKeys

>Is a keyboard shortcut for clicking on a certain element and its functionality depends on the browser and the operating system used, since not all browsers support access keys. access keys are added as an attribute

So payload will be changed to.

```html
<link rel="canonical" href="https://0a36007f03cab26381eccce7006700ef.web-security-academy.net/?'accesskey='x'onclick='alert()"
```

This sets the `X` key as an access key for the whole page. When a user presses the access key, the `alert` function is called.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/55f8846c-0b0e-485d-80ff-ffbb0b3961b2)


To trigger the exploit on yourself, press one of the following key combinations:

On Windows: `ALT+SHIFT+X`
On MacOS: `CTRL+ALT+X`
On Linux: `Alt+X`

I am using Windows so when I click on `ALT+SHIFT+X` the alert is triggered.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0c6048e1-5084-4817-8d80-6eaebd6f8909)

LAB Solved.

