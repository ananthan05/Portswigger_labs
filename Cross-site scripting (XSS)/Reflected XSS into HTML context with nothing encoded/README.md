## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4913ceb4-2bb5-42f7-8429-d7f7aaf1c81d)

## Solution :

We straightaway see a search functionality.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3449e929-2f96-4855-89a4-66863258d660)

what ever we are typing there is reflected in the web application .when i type `cyber` and send.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/03e6834b-1886-4289-8e0c-b0f6b1ae9da0)

Click  **View Selection Source**, shows how our data is being embedded in the page.

```html
<h1>0 search results for 'cyber'</h1>
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/804d9fa2-af6d-4234-803d-e036afe5698c)


## Payload

Enter the following simple XSS payload to trigger an alert!

```js
<script>alert(1)</script>
```

Enter the following simple XSS payload to trigger an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/69154e29-8d5a-4ad0-a2d8-b5c26f0d234a)

LAB Solved.
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6d61f853-603d-4fb6-8448-496473dcb3c5)
