
# SampleJwtSimpleServerPCF
The repository just wanted to demonstrate an issue with JWTSimpleServer whenever used within PCF, the issue was that PCF Apps Manager couldn't access to the actuators endpoints.

After testing this sample locally I pushed it to PCF and it worked perfectly.

This Sample includes:

1. Net Core API 
2. An **Unauthorised Controller** that allows every request
3. An **Authorised Controller** that enforces security, only request with a proper bearer token reach the controller methods
4. [JwtSimpleServer](https://github.com/Xabaril/JWTSimpleServer) as the security mechanism with a simple A**uthenticationProvider** (user: sampleapi, password: sampliapipassword)
	4.a. To get the token you have to **POST**:
		- To **http:YourHost:YourPort/token**
		- With **HEADER**: [{"key":"Content-Type","value":"application/x-www-form-urlencoded"}]
		- With a RAW **BODY** with this text: 'grant_type=password&amp;username=sampleapi&amp;password=sampliapipassword' 
5. **[Swagger](https://swagger.io) with [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)**
	5.a. Default route opens /swagger ( '/' redirects to '/swagger')
	5.b. Swagger includes **XML documentation**
	5.c. **Allows JWT Authentication**, this sample solves the issue that some people have authorising requests with JWT (security dictionary needs a 'Bearer' as key so that once you have **the token the input MUST be 'Bearer {token}'**)
