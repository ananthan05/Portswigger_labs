## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d32e9e7a-dd3a-4234-8d6c-50081ac53189)

## Solution :

>jQuery $ selector function is used to auto-scroll to a post based on the location.hash property

>Goals:Deliver an exploit that calls print


The first step is to analyse the web application. An interesting script can be found at the bottom of the page:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2195a18b-ddb6-436e-b0f5-2d6196c17ef0)

A quick check in some [online documentation](https://developer.mozilla.org/en-US/docs/Web/API/Window/hashchange_event) shows that the script is used to scroll to a post indicated by the fragment part of the URL. Using the title of a post after a `#`, the browser scrolls to the post.

entering `It's All in the Game - Football for Dummies` after `#`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e84bf453-2e9b-467b-8bd8-c63ef85755c7)

It will get redirected to there.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b9d4a08c-686d-43b2-8b90-34d15589b821)

According to scrip it should come.verfiying using the console.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/18b51a15-7720-4275-abf9-2247a8531ca8)

When I use a non-existing title, the console shows an error.But the value taken by the web app.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8d29b071-4757-4ade-9595-99a27999c17d)

## Payload to exploit

>So I can use content from the URL to trigger an error. If I am able to also inject an onerror handler, than I can call any command I want.
Fortunately there is the exploit server that I can use to prepare and deliver a custom made page. So I can create a page including an iframe to the vulnerable page. With an `onload` event I change the fragment which in turn triggers the `hashchange` event.

As a first step I try to trigger an error with this payload:

```html
<iframe src="https://ac8a1f4d1e3d1aa3c06b541e0003009a.web-security-academy.net/#" onload="this.src+='xxx'"></iframe>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4e6975b2-f4c6-4dce-a61a-e3736eb5503c)

It also shows an error similar to the one shown in the previous section.

Unfortunately, I can not simply attach an onerror handler on the iframe, I guess because of differing origins of the page itself (exploit server) and the iframe.

Instead, I try to inject an img tag with an invalid source and local onerror handler:

```html
<iframe src="https://0ae600e2041534388151a2c5003f00a6.web-security-academy.net/#" onload="this.src+='<img src=xxx onerror=alert()>'"></iframe>
```

And shows the alert box confirming that the script triggers on the main domain:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/89d0a035-6a92-4d91-818f-551e67d7fede)

Now it is simple: Changing the error handler to call print and deliver the exploit to the victim:

```html
<iframe src="https://0ae600e2041534388151a2c5003f00a6.web-security-academy.net/#" onload="this.src+='<img src=xxx onerror=print()>'"></iframe>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5dc75e7b-14f5-466b-a2bf-9945f1f41106)

Sending the page to the victim:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6a884256-43a9-4c2c-b573-c8be7500d2a4)


