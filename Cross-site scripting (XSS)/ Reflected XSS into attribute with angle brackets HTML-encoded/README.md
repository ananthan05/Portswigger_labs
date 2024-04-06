## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/47fe23f1-2817-4955-aa45-74a90751cb3b)

## Solution :

Payload-

>Autofocus: This is an attribute that can be applied to form elements like input fields or buttons. When a page loads, the browser automatically focuses on the element that has the autofocus attribute. This means that if you have an input field with autofocus, when the page loads, that input field will be automatically selected, allowing the user to start typing without having to click on it.

>Onfocus: This is an event handler attribute that triggers a JavaScript function when an element receives focus. For example, if you have an input field and you want something to happen when the user clicks on it or tabs into it, you can use the "onfocus" attribute to specify a JavaScript function to execute at that moment.

```html
"autofocus onfocus="alert()"
```

This HTML code creates an input field that automatically receives focus when the page loads, and when it receives focus, it triggers a JavaScript alert dialog with an empty message. 
This payload will triger an alert popup

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/aab59a29-4653-4c74-9193-641c0ef4326e)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c9826bfb-f796-47f0-ac12-3ef9d9cbf322)
