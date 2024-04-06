## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ed95b483-d32d-4894-9b7b-695fac768e09)

## Solution :

Inject a standard XSS payload, such as:

```html
<img src=1 onerror=alert(1)>
```

Observe that this payload gets blocked. In the next few steps, we'll use Burp Intruder to test which tags and attributes are being blocked.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/826e7137-b30d-4177-abd9-5810090ffe32)

>Note:The site is blocking common tags but misses some SVG tags and events.
`<svg> </svg>` we can try using this.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/309b9da9-4d9f-4933-a9e8-c3ba2f6b59e0)

The site is not  blocking `<svg>` tags.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/25db2a9f-edac-48ab-bed3-c662e5eb7547)

Send the resulting request to Burp Intruder.find the tag we can use in between `svg` tags.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5e2a7ca1-c348-4aee-a25e-90d88b1d14f7)

Now Visit the  [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click "Copy tags to clipboard".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/45dc13d1-2510-4d74-aee9-e8324b44b5fc)

In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. 
Click "Start attack".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/69fd9bef-8d8e-4823-abc7-f6f384e7a6b9)

When the attack is finished, review the results. Observe that all payloads caused an HTTP 400 response, except for 
the ones using the `<svg>`, `<animatetransform>`, `<title>`, and `<image>` tags, which received a 200 response.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8400c29f-57c7-4592-8b3e-3fab22884fc1)

`<animatetransform>` use an event atribute for finding that i use the payload
```html
<svg> <animatetransform a="alert()"></animatetransform></svg>
```
Send the request intuder.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f3bb470b-5cf9-4c1f-86c4-e6c4cdc7d563)

Visit the  [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)  and click "copy events to clipboard".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a906e820-5033-4111-b13a-5ed91832dabb)

Then start attack.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/477760b9-cf27-4fda-8d6b-801cc0d83d10)

Only `onbegin` has 200 response so will change the payload.

## Payload

```html
<svg> <animatetransform onbegin="alert()"></animatetransform></svg>
```
And search this alert will pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f3c855d6-e24c-44df-b6a3-9f14279d4acc)

LAB Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c4910269-0dec-48ea-aa32-f0b589f5da83)



