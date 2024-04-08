## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9cece796-52a9-4149-839a-b22891aaf932)

## Solution :

Enter your string in the search bar and click ‘Search’.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e5cb6d43-beaf-410e-b5cf-6354029e3a27)

HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8429be10-4b30-466a-bd8a-39509909072e)

You can use the search bar in the DOM to easily find your string. It appears two times.Our DOM-browser shows two results for our string: the first within an `<h1>` tag, and the second below within the `<script>` tag.

There is the template literal the lab title was telling us about. It is being defined as the variable ‘message’.

## Template Literals (Template Strings)

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1b647283-813a-4b41-aaf8-0dffa0e9b92b)

Payload will be-

```js
${alert()}
```
It will triger the alert pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/48d9c79e-abe8-46c5-9de3-e0d6607555de)

HTML-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/02ba1bf6-05aa-4ce9-a2b1-e76602b9cd7e)

Lab Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/11844791-7d57-4d3e-9c93-ce5988065b99)
