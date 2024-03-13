## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/05d84be4-044f-4791-bf74-bd9b1f38d76f)

## Solution :

This is the homepage url.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/02029df8-6931-4163-b9cf-bdc679ea64a3)

Now we need to bypass this page and directly access the admin page.

For that we tried accessing it using `/admin` but not worked.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/34bcc7c7-0635-4e41-80af-8bd0ebda8f65)

 
For that we can look for one of the common web directories like the robots.txt and sitemap.xml

by appending `/robots.txt` to the lab URL. Notice that the Disallow line discloses the path to the admin panel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/925078d3-fb23-4dc3-a8f8-473bdd0a7188)

In the URL bar, replace /robots.txt with /administrator-panel to load the admin panel.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/dc7f42b8-d66c-4157-8068-df3b8a8bb8eb)

Now delete carlos.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/2752e029-e7cd-4110-8bd4-0c9e0071ec5f)

Lab Solved.
