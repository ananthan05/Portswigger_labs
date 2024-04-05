## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a4656271-94b9-46a6-87cc-ddaa5c6a5f70)

## Solution :

>This lab mentions AngularJS expressions. I never used it before so a quick google search leads to the [respective documentaion](https://docs.angularjs.org/guide/expression) on the angular website.

>AngularJS expressions are executed in HTML sections inside of nodes containing the`ng-app` attribute. Fortunately, the full HTML body of the page is set as valid scope:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/abcdc919-5d1f-4d4c-a167-79f447f47cd7)

The most trivial example given at the documentation linked above is a simple addition with `{{1+2}}`. So using `foobar{{1+2}}` as search term, the search term is displayed as:

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2f839089-288c-4726-825b-1300368b5e24)

This confirms the execution of the expression. The next step is to find a possibility to inject script code.

payload to trigger an alert!

 ```js
{{$on.constructor('alert(1)')()}}
```

[PortSwigger](https://portswigger.net/research/xss-without-html-client-side-template-injection-with-angularjs) This page also contains example payloads that can be used to inject Javascript into Angular.

This raises the alert box-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/cbb97ee0-6921-4459-b46e-24ee57dc4832)

LAB Solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/24de33bf-e608-4894-80cd-69e69f3c19ac)
