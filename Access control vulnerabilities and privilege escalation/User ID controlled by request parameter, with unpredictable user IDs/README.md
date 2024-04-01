## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/80b960bd-8a3f-4510-9eb1-cb8bad7d9a9e)

## Solution :

`In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. Here, an attacker might be unable to guess or predict the identifier for another user. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.`

Click on My Account , it takes us to login page. Use the credentials `wiener:peter` to login.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bd9c75c0-9df8-4d68-a020-b78176cfda9e)

Once we login, we can see the API key  And Specfic GUID of wiener.

 Our aim is to find the GUID of carlos to get his API key. For that , click on the home page and browse through all the blog posts by carlos, Click on his username.

 After some browsing on the web we find out a a blog written by carlos.

 ![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/4b1d4707-5235-4be5-925c-b94f44e94cfa)

By clicking on carlos it will leak the GUID OF Carlos.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/803b739d-eca2-43a5-8dc7-70f71404b884)

Carlos GUID is `c4017d20-d076-49dd-b07d-489cb6ed55f6`

Now we need replace the GUID of Wiener with the GUID of Carlos in that we can get API Key of carlos.for that we need to send the GET request containing  the GUID of Wiener to repeater and repalce it.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/e3c3e605-4093-48ff-b4e1-9eb824680517)

After replacing.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/f0c983e3-accf-4d96-970f-2869bec0210e)

The API KEY IS `JcKPnb3jJ7oGv69x32DydN5VGsRoydxE`

Go to home page and submit it.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3547fe7d-4885-43ef-8824-2c92e2bea08a)

LAB solved.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/c7e959ee-19ed-4117-a431-694384b37d38)
