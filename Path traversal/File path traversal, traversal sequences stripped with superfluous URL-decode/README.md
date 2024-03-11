![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/13f52a30-93cb-435b-bedf-0b5a66c1fa69)## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/64872c97-dc1e-4d34-9c13-6e7a42a529d2)

## Solution : 

You can sometimes bypass this kind of sanitization by URL encoding, or even double URL encoding, the `../ characters`. This results in `%2e%2e%2f` and `%252e%252e%252f` respectively. Various non-standard encodings, such as `..%c0%af` or `..%ef%bc%8f`, may also work.

Use Burp Suite to intercept and modify a request that fetches a product image.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6440a5ba-cc1a-4a65-a4b2-93ed0a4e69c9)

Modify the filename parameter, giving it the value:


`..%252f..%252f..%252fetc/passwd` what we did here is double url enconding.

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/6c4c4864-9e40-4bb4-b80e-9af5f7ee2c13)

Lab solved .

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/d0a8e406-d9e7-40f2-a5bf-22eee49c61e0)
