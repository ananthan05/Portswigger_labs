## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/361c37eb-5a1c-466c-ac38-a65002be313f)

## Solution :

After the landing page is loaded set a canary and inject into the search field.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c1e865a8-ea48-42e9-8655-07a6f5d42736)

View the page source and observe that your canary is between the angularJS script.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3903d9b3-d49a-48eb-bd3e-55af2d37745a)

>Remember that you are dealing with angularJS sandbox, that means regular attack vectors are not going to work.
For being able to deliver a successfull XSS attack you have to bypass the angularJS sandbox.

## PAYLOAD
```js
https://YOUR-LAB-ID.web-security-academy.net/?search=1&toString().constructor.prototype.charAt%3d[].join;[1]|orderBy:toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1
```

View the page source

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/358fafb7-90b7-41d3-83ee-7497e62135cd)

LAb solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/95e3b1fb-4200-4c7d-9a5c-5055ee8ab4b7)


## Reverse Engineering the Payload

>The payload starts with the expression `toString().constructor.prototype.charAt=[].join;`. This line of code modifies the behavior of the charAt method of the JavaScript string object.
The charAt method is typically used to extract a character at a specified index of a string. By assigning [].join to charAt, the behavior of the charAt method is changed to join all elements of an array into a string, instead of extracting characters from a string.

>The `:` at the end of the line seperates the charAt modification from the rest of the payload.

>The next part of the payload is `[1]`. This creates an array with one element, which is the number 1.

>The `|` symbol is used to apply the orderBy filter to the array

>The orderBy filter is followed by the argument: `toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1`.
 This is a JavaScript expression that converts the ASCII codes: `(120,61,97,108,101,114,116,40,49,41)` into the string x=alert().
This is a malicious JavaScript code that displays an alert message with the value 1.

>The `=1` at the end of the expression is included to ensure that the expression returns a truth value. In AngularJS, a filter expects a truthy value to be returned from the argument expression, the expression returns the truthy value 1, allowing the orderBy filter to execute the malicious JavaScript code.

>The final expression is passed as the argument to the orderBy filter, which sorts the array of elements based on the argument expression. However, since the argument expression is malicious, the orderBy filter will execute the malicious JavaScript code, bypassing the AngularJS Sandbox security feature and allowing an attacker to execute arbitrary code in the AngularJS environment.

>The entire payload is included in a URL query parameter which is passed to the vulnerable website. When the website processes the URL, the payload is executed and the malicious JavaScript code is run, bypassing the AngularJS Sandbox security feature and allowing an attacker to perform arbitrary actions on the target website.
