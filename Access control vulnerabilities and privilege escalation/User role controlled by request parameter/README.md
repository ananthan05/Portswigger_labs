## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3e8de528-ea76-4db0-aab6-9eb5fc3b6dff)

## Solution :

we need to admin privalge to delete the user calrlos.
So first we try `/admin` and observe that you can't access the admin panel

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/187450bc-a7b8-4a00-8072-c0edffee07ce)

It says we can view only if we are admin. We have a login credential wiener:peter lets try with that.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/a0b116cb-c201-462f-bdb6-fed92d716112)

 loged in but admin panel is missing.

 so we need to check the request we made while login.

 In post request-

 ![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/86ca6a2a-48c2-4cfb-9684-d2416d50e1c2)

it is saying adimn= false that why we are not getting admin panel.

we will change this to `True` in GET request get admin panel.

In Get request-

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/0dd90cd7-54a1-49eb-8ce1-d8a0b0dacfed)

we searched but not admin panel is given now we will send the get request to repeter and change the Admin=true.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/ab9416dd-5c59-4f69-a7fd-a78eed0ba293)

Now admin panel is visble now send this request and access the admin privilage.

for that  select incepect go to application then go to cookie and change admin= false from admin= true . 

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2dac2df0-008e-4585-a570-4de85b72a6f9)

And  then refresh.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/3d0f63d1-8ef1-47a1-85a7-82600b597306)

Now delete carlos.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6bfae76b-db2c-4710-a9b0-7c23e659236d)

