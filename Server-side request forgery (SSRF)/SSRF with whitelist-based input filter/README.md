## Lab Description :

![image](https://github.com/ananthan05/Portswigger_labs/assets/140697378/686d930a-4877-4aa0-a21a-3ace9863b84a)

## Solution :

Intrecepted the stock check request and tried accesing the `127.0.0.1/admin` page

![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/bba583a9-ea94-40e0-8029-b2ff3534b661)

It was blocked by the server.

Tried using the `username@stock.weliketoshop.net`

![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/84de93ed-4778-41b4-9e37-f0e52f8c9051)

It was accepted by the server.

adding a `#` and the URL is now rejected.

![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/0f4489b9-6713-45f6-ab3b-c7d79f1a5f75)

using URL encoding encoded `#` to `%2523` and it was accepted.

used the payload `http://127.0.0.1%2523@stock.weliketoshop.net/admin` and the access was attained.

![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/f8e5a403-c757-436f-86ae-965333f2cd43)

Deleted user carlos.

![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/bafcdf30-9b0e-4706-8a1b-891362fb0025)

Lab Solved.
 
![image](https://github.com/RahulMMenon011/PortSwigger_Labs/assets/140642506/7a3ab584-c87c-4710-b5b0-c3d89dea873a)
