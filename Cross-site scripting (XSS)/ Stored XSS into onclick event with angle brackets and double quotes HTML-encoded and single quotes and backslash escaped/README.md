## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ad93c04e-6a60-4e35-a6ab-a238267a10db)

## Solution :

After landing the home page of the lab, choose one of the blogposts.Post a comment with a random alphanumeric string in the Website input field.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/427b9a0c-5004-46d0-b6dc-59497d55d772)

Observe that the random string has been reflected inside an onclick event handler attribute.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/19223f03-5d3e-4995-9636-b5db55172bfb)

>This is where the vulnerability comes into play. It takes href value as an input from the user, then passes this input directly into the tracker function without proper input sanitization.

 Try to inject another input to the Website input field. But this time make sure you use single quotes in your input, then observe that single quotes has been escaped by backslash.

 Payload

 ```js
'cyber
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a311af42-9fc4-4539-bbfb-ad831ef87b52)

As you can see the single quotes are escaped by backslash character.

## Bypassing Input Sanitization via HTML-Encoding

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/69ea7c86-8625-4d24-a7fa-1e3e16e8a194)



So the Payload will be -

```js
&apos;-alert()-&apos;
```

Clicking the name above your comment should trigger an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a8fb5b15-0e4f-45da-ae89-9b3bc0df9e37)

Html code-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/39eb0563-6fed-45a3-9be8-8c06ac87335c)


Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a8f0ecac-9cac-459d-af4d-fc21a958b336)
