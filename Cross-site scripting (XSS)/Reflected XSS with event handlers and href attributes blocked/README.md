## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1dc5e5b7-5df1-4ae4-a49e-f363ca1e4f39)

## Solution :

So event handlers and `href` attribute are blacklisted.

Let’s use Burp intruder to see whether we have any tags that we can use.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fa5aacfa-0562-4d9b-84b3-e649af190fd7)

Now Visit the  [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click "Copy tags to clipboard".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/45dc13d1-2510-4d74-aee9-e8324b44b5fc)

In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. Click "Start attack".

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1942c6c6-dd1b-40e2-8c6c-dbb64ea7dcf2)

When the attack is finished, review the results.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f535fd89-75cb-461f-9b72-849cf967a9a5)

Valid tags:

```
<a>
<animate>
<image>
<svg>
<title>
```

>
>Note that you need to label your vector with the word "Click" in order to induce the simulated lab user to click your vector. For example:

```html
<a href="">Click me</a>
```
but this is blocked we have to some inject alert using the valid tags.

our normal payload is this.

```html
<a href="javascript:alert()>Click me</a>
```
 > scince this payload is not accepeted. we will create this payload using  Some of the whitelisted tags are `svg`, `animate` and `a`. We can use them to our advantage and easily trigger our javascript.

for refernce how animate tag works.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9ed9f099-ae32-4906-ba9c-ceaba290d857)

So our payload will be

```html
<svg>
 <a>
  <animate attributeName="href" values="javascript:alert()"></animate>
   <text x="20" y="20">Click me</text>
 </a>
</svg>
```

Give the payload in search.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2ada6cc9-4f6b-4f08-830d-e6973a0935ec)

By pressing `click me` an alert pop will come.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/862c7fca-ee22-4130-b7f5-52603bf5a4d2)


Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0122f910-064f-4b76-8631-8dcb9a579e0d)

