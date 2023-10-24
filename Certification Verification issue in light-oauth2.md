\[NAME OF AFFECTED PRODUCT(S)]: light-oauth2

\[AFFECTED AND/OR FIXED VERSION(S)]: before version 2.1.27

\[PROBLEM TYPE]:

Vulnerability Type: MITM (Man in The Middle Attack)

Root Cause: Insecure cryptographic implementation

\[DESCRIPTION]:

The Light-oauth2 library uses Json Web Tokens (JWT) to transmit identity and permission information during the implementation of the OAuth protocol. It employs digitally signed JSON Web Signatures (JWS) to ensure the security of JWT. However, in the process of validating JWT, the Light-oauth2 library does not directly verify the validity of the digital certificate containing the public key. Instead, it directly uses the public key from the digital certificate to validate the JWT's validity.

![image](https://github.com/KANIXB/JWTIssues/assets/119597423/860072c4-14c5-4626-ae4a-fe06c49794b5)


In this scenario, attackers can exploit self-signed digital certificates or revoked digital certificates to forge JWT and successfully pass the validation process. This can potentially lead to man-in-the-middle attacks against identity authentication or authorization systems.

The Location of the issue: Package: com.networknt.oauth.key.handler; Class: Oauth2KeysGetHandler.class

Security issue: not verify the public key certificate used to validate JWT signature.

Issue: <https://github.com/networknt/light-oauth2/issues/369>
