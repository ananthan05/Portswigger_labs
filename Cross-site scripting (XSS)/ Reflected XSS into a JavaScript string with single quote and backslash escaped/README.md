## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/fc8305a0-5349-4016-b955-7d1061b34998)

## Solution :

In the serch functionality type `cyber` and observe the html code.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f92cca3b-dcd7-42a4-a2c8-36fc2d9c46c6)

Try sending the payload `test'payload` and observe that your single quote gets backslash-escaped, preventing you from breaking out of the string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0694340c-5c1f-4ba2-9f49-67b26af34b85)

Since we can not break out of the string context, what if we can close the `<script>`
 
Payload wiil be

```html
</script><script>alert()</script>
```
it will triger the alert pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/957b7389-7949-4e6a-911d-56e5bad84f49)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ece4f09d-6246-4d90-bb0e-f7d0431b1e03)

