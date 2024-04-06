## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1e445eb2-309d-4310-adaa-6004b4eeeffd)

## Solution :

Inject a standard XSS Payload.

```html
<img src=1 onerror=alert()>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/47d8c30a-2349-416a-bc77-40873141ac91)

Resulted in an `400 Bad Request` error and the message `Tag is not allowed`.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3fdde15f-373d-4da1-a358-77bf1472bb4d)

This implies that the filtering is done and blocking our request.

>This doesn't mean that everything is being filtered out. Example if i try the angle brackets themselves`<>` 
these are evidently not being filtered out by the web application firewall (WAF).

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/226d0cef-5a88-42bc-8d38-8bf2fab938df)

Resulted in no error.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a6298c50-de91-4a86-b0ec-1f7407374aa7)

The following HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0f5885ce-9446-40b3-9d36-9b6fe1d856f3)

>To find the Payload first we need to find the tags and attributes which will bypass this WAF.

>For that we'll use use Burp Intruder to test which tags and attributes are not being blocked by WAF.

Capture the request.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6bd89d8a-fe54-481f-9ebc-8e8b8f4f2d03)

Send it to Burp Intruder.In Burp Intruder, in the Positions tab, replace the value of the search term with: `<>`.Place the cursor between the angle brackets and click "Add §" twice, to create a payload position. The value of the search term should now look like: `<§§>`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/43637db2-f255-49d0-ae1a-07774a1108ae)

Now Visit the  [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click "Copy tags to clipboard".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/45dc13d1-2510-4d74-aee9-e8324b44b5fc)

In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. 
Click "Start attack".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d9776e8e-8be6-4f68-9476-831569a77286)

When the attack is finished, review the results. Note that all payloads caused an HTTP `400` response, except for the `body` payload, which caused a `200` response.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/27a48e99-e650-4bb2-a99f-65a343ea69f3)

Now go back to the browser and try sending 

```html
<body>
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e8034b59-6c1a-4c42-b00a-823f8ca1237a)

It was successful.

Now we need find the attributes which will bypass this WAF.For send this request Intruder replace your search term with `<body%20=1>` .Place the cursor before the = character and click "Add §" twice, to create a payload position. The value of the search term should now look like: `<body%20§§=1>`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bc0fe18e-db48-4c13-9dd5-8c6f88a171c9)

Visit the  [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)  and click "copy events to clipboard".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a906e820-5033-4111-b13a-5ed91832dabb)

In Burp Intruder, in the Payloads tab, click "Clear" to remove the previous payloads. Then click "Paste" to paste the list of attributes into the payloads list. Click "Start attack".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/768e79f9-0519-4e43-a251-0054b81248bc)

When the attack is finished, review the results.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7968c3db-dd1d-4a9a-a7e5-06f49460d1c8)

> Note : Your solution must not require any user interaction. Manually causing print() to be called in your own browser will not solve the lab.

> All the Payloads  events which give response of `200` has require user interaction.

For example if we are taking the event `onbeforeinput`.

We created a payload 
```html
<body onbeforeinput= alert()>
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b480f021-36aa-4463-88b9-f49cdb3c572e)

and result.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f9cd657e-8dcb-462d-9fba-4eecf3e4e5a8)

If we need to get the alert pop we need type something in search blog that will be user interaction.

When i tried to type the pop alert came.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9a5a629a-c41b-45d2-b55c-022b5b39d788)

we need to Manually causing `print()` to be called in your own browser will not solve the lab.Similarly
`onresize` event.

Payload 

```html
<body onresize= print()>
```
and result.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6ee581db-5aa4-429e-bf24-9c0a8c23b5bc)

If we need to get the `print` we need press the minmise button.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/db0ec23b-60e5-4d97-96fd-9dc21fb16b8c)

So the every Payloads  events are has user interaction . For that we can use `iframe` and i am using `onresize` with that because `iframe` has a property to cahnge its size so that why this will work with iframe.

So the payload will looklike this.

```html
<iframe src = "exploit url path "onload=this.style.width="pixel size according to you.px"></iframe>
```

> First this i frame will load the sorce exploit url initally .Once  it completely loads right this `onload`get triger automatically which will ultimately change `this.style.width="pixel size according to you.px"` the width of the iframe. when width change the malicious payload will get executed .

## Payload

The exploit url path we alredy executed. =`https://0a13007604878ef3817f17ce005d007f.web-security-academy.net/?search=%3Cbody+onresize%3D+print%28%29%3E` in which we have already used the payload `<body onresize= print()>`.

So The payload will be 

```html
<iframe src = "https://0a13007604878ef3817f17ce005d007f.web-security-academy.net/?search=%3Cbody+onresize%3D+print%28%29%3E" onload=this.style.width="200px" ></iframe> 
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/98c3a63c-a476-4071-b731-d47652ddcc1d)

Press view exploit. 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9dfc2a54-13f3-4fff-80b9-ed737345a584)

Now send to the victim and lab will be solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aae66dcd-f79c-4fc3-b78f-b42060c131c3)
