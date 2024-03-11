## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/b09ae1d9-860d-48ee-b20b-e2b516a07a85)

## Solution : 

Use Burp Suite to intercept and modify the request that submits feedback.

Then

Modify the email parameter, changing it to:

`email=||whoami>/var/www/images/whoami.txt||`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/615f61a5-1b21-4108-b93c-4cba60a8de67)

Now use Burp Suite to intercept and modify the request that loads an image of a product.

Modify the filename parameter, changing the value to the name of the file you specified for the output of the injected command:

`filename=whoami.txt`

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e17ad7bb-2b61-4cb5-861c-afba02af4dc3)

LAB solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dd74b27f-5797-4369-bc6a-90ab068cd091)
