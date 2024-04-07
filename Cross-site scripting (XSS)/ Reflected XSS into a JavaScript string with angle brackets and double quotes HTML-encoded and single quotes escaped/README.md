## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a4f32214-4076-40b3-99a8-7412d6ba6b43)

## Solution :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a095375f-1ede-45ea-9d32-d68c0f2d5974)

Add a unique alpha-numeric string to the search bar. One that will not be anywhere else on the page. Click ‘Search’.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/7fe6fbea-6ebb-47e8-accf-5d8f284a7aa4)

Our search string appears in a `<script>` tag and is being assigned to the variable ‘seachTerms’. This is where we are going to try to break out and insert our `alert()` function.

>The title of this lab let’s us know that single quotes are not going work.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d8c98395-3328-4c57-bf0f-f0553c46c46d)

>After finding your string in the DOM, you’ll see that the server responded with the addition of a backslash, ‘\’. 
A result of server-side input handling. This is the ‘escaping’ the lab title was referring to.

>Since the title gave us a clue about the single quote, it is also giving us a clue by NOT mentioning the backslash.
 Maybe, if we successfully add our own backslash before our single quote, the server will insert it’s own backslash in between.
>Effectively, our backslash will escape the server’s backslash, leaving our single quote to terminate our search string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/946b1a7c-24e1-46c5-8e59-cc5fad3f845b)

It worked! This opens the door for us to inject our ‘alert()’ function into this line of JavaScript code.

Let’s try it now with our `-alert()` function added.

Payload will be.

```js
\'-alert()
```

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/665b8726-07ee-44bf-bd0a-3198bbe0afb7)

Still didn’t work. However our `alert()` function IS broken out. We still have that trailing single quote and semi-colon preventing it from being valid code.

>To remove certain parts in JavaScript, we often use two forward slashes `//` as a comment marker to effectively `comment out` those sections of code.

Now let’s try adding `//` to the end of our payload.

```js
\'-alert()//
```
This will triger an alert pop up.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/8364fd53-d451-4124-817c-3e56d71317bf)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d9df5440-d3a2-4d05-be64-22070a20e263)

