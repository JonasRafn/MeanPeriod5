# MeanPeriod5
### Question 1: Explain basic security terms like authentication, authorization, confidentiality, integrity, SSL/TLS and provide examples of how you have used them.
#### Authentication  
Authentication is simply put the act of verifying a users identity. This can be done through an email and password.  
#### Authorization  
Authorization is delegating rights for resources to multiple users, you might not want any user to be able to see all data.
#### Confidentiality
Making sure that the user data that is stored on your system is in safe hands even if someone gets to it, ie. Hashing and Salting passwords.
#### Integrity
Making sure that data is not just modified by anybody, but the modifications is monitored to assure the integrety of the data.
#### SSL/TLS
Secure Socket Layer, a protocol that enables end to end encryption of http network traffic. Transport Layer Security a newer and more secure protocol that has replaced SSL.

### Question 2: Explain basic security threads like: Cross Site Scripting (XSS), SQL Injection and whether something similar to SQL injection is possible with NoSQL databases like MongoDB, and DOS-attacks. Explain/demonstrate ways to cope with these problems

#### XSS
When designing webpages that show user entered content it is important to sanitize the user input to avoid cross site scripting.
#### SQL-Injection
Again neccessary to sanitize input to avoid SQL-injections when f.ex. searching for an item.
#### DOS-attack
Denial of Service attacks is a type of attack that prevent legitemate users from using your service. This can either be done by crashing your service, or by flooding your service. 

### Question 3: Explain, at a fundamental level, the technologies involved, and the steps required initialize a SSL connection between a browser and a server and how to use SSL in a secure way

When using end to end encryption like SSL you need a pair of keys to encrypt the data, this is normally done by using 2 key encryption, this means that both the client and the server has 2 keys to encrypt, a public and a private key.  
The client only knows the servers public key and vice versa, this way it is only the server or the client that can un encrypt the message from the other. This is how a basic transaction looks:  
1. Client hello, client sends a hello message containing basic information like SSL/TLS version and a random byte string.  
2. Server hello, server responds with a hello message containg basic information like in client hello, a random byte string and a digital certificate.  
3. Client verification, the client verifies the certificate.  
4. Server verification, the clients send a certificate that the server verifies.  
5. Clients message, the client uses the random byte string(key) from the server to encrypt a message, then encrypt both the encrypted message and the key, using the servers public key, and sends it to the server.  
6. Server message, the server uses its private key to unencrypt the encrypted message and key, and uses the key to unencrypt the message. The server then does the same as the client using the clients public key and sends a message back.  


### Question 4: Explain and demonstrate ways to protect user passwords on our backends, and why this is necessary
See answer to question 5.

### Question 5: Explain about password hashing, salts and the difference between bcrypt and older (not recommended) algorithms like sha1, md5 etc.
#### Hashing 
Hasing is a method that turns a string of characters in to a new string, sort of like encryption except you can only go 1 way. You cant hash a string and then get the original string back. Hasing is used in many different ways, f.ex. in storing passwords, making sure a file has not been changed, like a digital certificate, or program you download from a website you trust but you might suspect that you are behind a proxy that has changed the download link.
#### Salting
A way to counter hashing is a method called rainbow tables, this basically means that isntead of trying to reverse a hashing algorithm, you just hash the most used passwords and save them. When you then get a hold of some hashed passwords you can look them up in a rainbow table. This can be countered by using a salt when hashing, it is reaaly simple. You just a random string(could be "1234") to the string you are hashing.
```
hash("password") = 	5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8
hash("password" + "1234" = 	b9c950640e1b3740e98acb93e669c65766f6670dd1609ba91ff41052ba48c6f3
````
The salt should never be reused and should be unique for every username-password combo.

#### SHA1, MD5
Both SHA1 and MD5 are old hashing algorithms and are today not considered safe anymore, this is due to 2 things. 1 computers have gotten super fast compared to when these algorithms were developed, and rainbow tables have been created all of the most common passwords for both algorithms.  
You should instead use a newer algorithm like SHA256 or SHA512 these hashes strings using more bits.

#### BCrypt
BCrypt takes another approach to the hashing algorithm than SHA256 or SHA512. Instead of trying to create a longer and more complex string, it tries to defeat rainbow tables by being a very slow algorithm. It is not a slow algorithm to hash a single password, but the create a rainbow table of the 100000 most used password would take an infinetly big amount of time. So even if you were a bad developer and using the same salt for all your passwords, and a bad guy got a hold of it, he would not have the time to create a rainbow table for the passwords in your database. 

### Question 6: Explain about JSON Web Tokens (jwt) and why they are very suited for a REST-based API

JWT is a new way to handle token based authentication, whenever a user logs in to your site, they get a token in return this token holds information about the user and whether they are autheticated or not. Whenever the user makes and http request it sends along this token that is used for authentication, this is called stateless authentication.

### Question 7: Explain and demonstrate a system using jwt's, focusing on both client and server side.

Refer to [SimpleMEANSeed]
#### Client
When the client logs in to the system the Authentication Token is saved in local storage(session).
```javascript
$window.sessionStorage.token = data.token;
```
Next time the client makes an http request, a authinterceptor will intercept the request and add a header called Authorization containing the token.
```javascript
config.headers.Authorization = $window.sessionStorage.token;
```

### Question 8: Explain and demonstrate use of the npm passportjs module
Refer to app.js in [SimpleMEANSeed]  
The NPM module passport is used for token based user authentication, by putting alot of the stuff, a developer would make him/herself beforehand, in to this package. It has the possibility to get the header automatically instead of having to grab it yourself, also makes the authentication with your database alot easier as it handles most of it out of the box. 

```javascript
app.use('/api', function (req, res, next) {
    passport.authenticate('jwt', {session: false}, function (err, user, info) {
        if (err) {
            res.status(403).json({success: false, message: "Token could not be authenticated", fullError: err})
        }
        if (user) {
            return next();
        }
        return res.status(403).json({success: false, message: "Token could not be authenticated", fullError: info});
    })(req, res, next);
});
```
As you can see you simply pass the token into a authenticate method from passport and it takes care of the rest, super simple. 

### Question 9: Explain, at a very basic level, OAuth 2 + OpenID Connect and the problems it solves.
OAuth the predecessor to OAuth2 is a protocol/standard makes 3rd party sites able to get access to a ressource server on your site this is simply done by given the 3rd party an authentication token. This can seen many places today, where you can login with Facebook on many different services.
OAuth2 and OpenID Connect, adds another token to this protocol. An ID token that is used for identification this way the resource server knows which user is trying to get informatin. 

### Question 10: 
See [SimpleMEANSeed]

[SimpleMEANSeed]: <https://github.com/JonasRafn/SimpleMEANSeed>