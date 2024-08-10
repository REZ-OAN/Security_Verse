# What is SSL ?
**SSL (Secure Sockets Layer)** is a protocol designed to secure communication between a web server and a client, such as a web browser. By establishing an encrypted connection, SSL ensures that all data exchanged remains private and protected from interception, tampering, and forgery.

# How it works ? 
The process begins with the `SSL` handshake, where the server and client agree on `encryption` methods, authenticate the server (and optionally the client) using digital `certificates`, and exchange `keys` for encryption. Once the handshake is complete, all data transmitted is encrypted, ensuring secure communication. 

**NOTE**: Working of SSL is elaborately explained later in this document.

# Why it is shown as SSL/TLS now ?
While `SSL` has been replaced by **TLS (Transport Layer Security)** as the standard protocol for securing web traffic, the term **"SSL"** is still widely used to refer to both `SSL` and `TLS`. TLS is essentially a more modern and secure version of SSL.

# HTTP vs HTTPS (overview)

HTTP

![HTTP](https://github.com/REZ-OAN/Security_Verse/images/ssl/http-not-secure.png)

HTTPS

![HTTPS](https://github.com/REZ-OAN/Security_Verse/images/ssl/https-secure.png)

# How SSL comes into play ?

## First Player SYMMETRIC KEY ENCRYPTION

Let's assume you (a client, a browser) wants to communicate (send/receive data) with a server. You share your **id and password** (send as a plain text without any `encryption`) to access the server on a request and server gives you the access to it after verifying. In the mean time a **hacker** can `sniff` your data (id and password) and use these to harm you.

![hacker sniffs data when without any encryption](https://github.com/REZ-OAN/Security_Verse/images/ssl/without-encryption.png)

To **protect** your **sensitive** information from being exposed, `encryption` is essential. Encryption transforms your data into an unreadable format before it's transmitted, so even if a hacker intercepts it, they can't make sense of it. 

**NOTE**: `Encryption` is the process of **converting** plain, readable data (`plaintext`) into a coded form (`ciphertext`) that can only be understood by someone who has the correct `decryption key`. This ensures that even if the data is intercepted during transmission, it remains unreadable to anyone without the **key**.

Here comes the concept of **Symmetric Encryption** technique. In this method a client generates a key and this key is responsible to `encrypt` and also `decrypt` the data (**plaintext**) and encrypted data (**ciphertext**).

![generate-symmertic-key-and-data-pass-with-encryption](https://github.com/REZ-OAN/Security_Verse/images/ssl/symmetric-key-gen-data-pass.png)

But if we do not pass the symmetric key to the server, the server also cannot decrypt the data. Hence we have to sent the symmetric key to the server. And here the hacker will sniff the symmetric key and see the data after decryption.

![sniffing-the-symmetric-key-and-decrypt-data](https://github.com/REZ-OAN/Security_Verse/images/ssl/symmetric-key-sniffed.png)

To safeguard the **symmetric key**, we use the `asymmetric encryption` technique.

## Second Player ASYMMETRIC KEY ENCRYPTION

With symmetric encryption technique we saw that our data is insecure. But if we transfer the symmetric key using some encryption technique then it may be secure. To ensure this concept of securing the **symmetric key** here comes `Asymmetric Encryption` technique. In **asymmetric encryption**, two different but related `keys` are used: a `public key (locker)`for **encryption** and a `private key (key)` for **decryption**. The **public key** is shared `openly` and can be used by anyone to **encrypt** data, but only the person with the corresponding **private key** can **decrypt** it. This method is mostly followed by the server. In the sever side we generate these two keys and first we share the `public key` with the clients.

![protection-of-symmetric-key-as-well-as-data](https://github.com/REZ-OAN/Security_Verse/images/ssl/with-both.png)

**NOTE**: Once the server receives the symmetric key, all data is encrypted and decrypted using that key.

It's definitely a complex system, but does it fully guarantee that our data can't be intercepted? Unfortunately, the answer is no. A skilled hacker can act as a middleman, pretending to be a legitimate client to the server and a legitimate server to the client. The hacker would act as a proxy. 

![proxy-hacker](https://github.com/REZ-OAN/Security_Verse/images/ssl/proxy-hacker.png)

With the hacker in possession of the symmetric key, they can intercept and decrypt our data. So, how do we solve this problem? This is where SSL certificates steps in as the true savior.

## Final Player SSL certificates

When a server sends its `public key` to the client, it also sends an **SSL certificate** along with it. This certificate is signed by a trusted `Certificate Authority` (CA), which acts as the **issuer**. With this certificate, the client can `verify` whether the public key it received is indeed from the legitimate server or if it might have been intercepted and altered by a hacker.

![ssl-certificate](https://github.com/REZ-OAN/Security_Verse/images/ssl/ssl-certificate.png)

If a hacker intercepts and tries to alter the public key, the tampering will be detected during the verification process. As a result, the client will abort the connection, ensuring that the communication remains secure.

When requesting an SSL certificate from a Certificate Authority (CA), you will need to provide the following details:

```
Country Name=<>
State or Province=<>
Locality=<>
Organization Name=<>
Organizational Unit Name=<>
Common Name (your domain name)=<>
Email Address=<>
```
**Country Name**: The two-letter code for your country (e.g., "US" for the United States).

**State or Province**: The full name of the state or province where your organization is located.

**Locality**: The city or locality where your organization is based.

**Organization Name**: The legal name of your organization (e.g., "Example Corp").

**Organizational Unit Name**: The department within your organization (e.g., "IT Department").

**Common Name (your domain name)**: The fully qualified domain name (FQDN) for which you are requesting the certificate (e.g., "www.example.com").

**Email Address**: A contact email address for your organization.

These values are included in the Certificate Signing Request (CSR) and are used by the CA to verify your identity and issue the SSL certificate.


## How the CA Creates the Signature and What the Certificate Contains
The CA uses its `private key` to sign the **SSL certificate**. This signature acts as a guarantee that the certificate was issued by a trusted CA and that the information within the certificate is authentic and valid.

**The certificate includes:**

**Public Key:** Extracted from the Certificate Signing Request (CSR).

**CA Signature:** The CA's signature binds the public key to the certificate's information, confirming its authenticity.

**Validity Period:** The certificate specifies a start and expiration date, indicating its period of validity.

**Certificate Details:** Information about the domain, the organization, and the issuing CA.

# View the SSL certificate after visiting to a website

- [View SSL Certificate](https://github.com/REZ-OAN/Security_Verse/docs/CheckSSLCertification.md)