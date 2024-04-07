## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/538d9380-735e-495e-8508-10b80024d5af)

## Solution :
Submit a random  string in the search box.Observe that the random string has been reflected inside a JavaScript string.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/55bf90fe-82a3-441b-884c-97a11ddb1d71)

Replace your input with the following payload to break out of the JavaScript string and inject an alert:

```js
'-alert(1)-'
```
it will triger an alert.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/eef5357f-4606-4420-93e5-deb31be965dc)

Lab solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ec1778cd-7694-4382-9b07-25817257347c)

