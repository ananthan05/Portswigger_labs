## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0d982c39-ea85-4bdc-9fed-a46b62673abf)

## Solution :

In Burp Suite, go to the Proxy tool caputer the request when typing `cyber`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/94671318-f984-4cd7-b5dd-f9351fd113e1)

Notice that the string is reflected in a `JSON response` called `search-results`.

From the Site Map, open the searchResults.js file and notice that the JSON response is used with an eval() function call.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/1c98bb42-54d7-4e3d-b51d-fc7784c08e8a)


Send the request Repeter to experiment with it.

first tried broke out java string using `\"`.The `man` was shown outside the string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/20c763bf-96c8-41c6-bc4e-52b231bd2037)

>The problem is that we don't have a valid Javascript object at this stage this becuse we have this trailing quote and Curly backet at this end of the object.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b4675855-5c8e-4957-8715-10d647445214)

> We can actully comment that out that we use comments in JavaScript `//` we are going to end our java script object first.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a888bfbc-7a20-40a8-b765-7cff825b715b)

Payload-

Now we will make out payload by `-alert()` instead of `man` we are using `-` because `+` used for url encoding.

```js
\"-alert(1)}//
```
![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3fc3824a-902f-45e4-9b82-12f80e5f79f8)

> As you have injected a backslash and the site isn't escaping them, when the JSON response attempts to escape the opening double-quotes character, it adds a second backslash. The resulting double-backslash causes the escaping to be effectively canceled out. This means that the double-quotes are processed unescaped, which closes the string that should contain the search term.

> An arithmetic operator (in this case the subtraction operator) is then used to separate the expressions before the alert() function is called. Finally, a closing curly bracket and two forward slashes close the JSON object early and comment out what would have been the rest of the object

Now go and search the payload and it will trigger an alert!.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/9819b165-8d38-48ca-a29e-a02eeb51dde8)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bad87e9c-355e-4f1e-9f49-354d59b4d8a4)

