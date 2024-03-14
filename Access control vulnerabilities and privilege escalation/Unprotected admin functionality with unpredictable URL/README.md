## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/5e9167e2-99db-452f-85db-9b46d63e8447)

## Solution :

Home page.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a636dd0b-3a15-46b4-9872-ccb1e8668df7)

first we check if  robots.txt is there or not.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/28e6751b-c48f-4589-9666-3e72bf5530aa)

It is not there. now we will check the source code to find whether ther is any left over or not to access the admin privilage.
On seeing the source code, we see a javascript code which checks if the user is admin, then it redirects us to /admin-59c6c7 endpoint which is the admin panel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/bf74c94d-cdda-4d6f-8dba-18c69410f479)

So we could directly browse to that directory to view the admin panel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/51160280-19ee-42e6-a3a8-47f5e6661bd3)

Lab solved were able delete the carlos from it.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d6bb6895-1845-48b1-81dd-be718a895c53)
