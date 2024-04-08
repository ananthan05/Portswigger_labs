## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4eae5b9a-1dba-4eb9-818c-41cfe38eaaf5)

## Solution :

Payload-
```js
<script>
location='https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cinput%20id=x%20ng-focus=$event.composedPath()|orderBy:%27(z=alert)(document.cookie)%27%3E#x';
</script>
```

Go to the exploit server and paste the following code.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a746a2e6-88b0-4b08-b5b6-6ab8ec146da8)

>The exploit uses the ng-focus event in AngularJS to create a focus event that bypasses CSP. It also uses $event, which is an AngularJS variable that references the event object. The path property is specific to Chrome and contains an array of elements that triggered the event. The last element in the array contains the window object.

>Normally, | is a bitwise or operation in JavaScript, but in AngularJS it indicates a filter operation, in this case the orderBy filter. The colon signifies an argument that is being sent to the filter. In the argument, instead of calling the alert function directly, we assign it to the variable z. The function will only be called when the orderBy operation reaches the window object in the $event.path array. This means it can be called in the scope of the window without an explicit reference to the window object, effectively bypassing AngularJS's window check.

Click "Deliver exploit to victim" and Lab is solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7f71bbb0-8fa2-46bb-aa2e-10de67406a28)
