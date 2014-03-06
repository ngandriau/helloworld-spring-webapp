# Introduction

This project is a sample of spring and jersey integrated
It is based on the helloworld-spring-webapp sample from
https://github.com/jersey/jersey/tree/2.6/examples/helloworld-spring-webapp

The pom.xml has been replaced by a build.gradle

The webapp deploy in tomcat and you can invoke it with http://localhost:8080/<context>/rest/jersey-hello

tested with Idea and tomcat 7.0.47
Need to test more the gradle plugin: "war"

- - -

Securization of the rest resources with spring and oauth2 is under way, but not yet operational

If you reactivate the 'springSecurityFilterChain' in web.xml, rest call fail.

In the end, you should be able to get a token with this call:

    curl -X POST -d "client_id=the_client&client_secret=1234567890&grant_type=client_credentials" http://localhost:8080/hello/oauth/token


Right now, this request validate the credential, as indicated by the call with a bad pasword:

    $ curl -X POST -d "client_id=the_client&client_secret=badPassword&grant_type=client_credentials" http://localhost:8080/hello/oauth/token
    {"error":"invalid_client","error_description":"Bad client credentials"}

But if we pass valid credential, we get a 404:

    <h1>HTTP Status 404 - /hello/oauth/token</h1>
    Status report</p><p><b>message</b>
    <u>/hello/oauth/token</u></p><p><b>description</b>
    <u>The requested resource is not available.</u>

and this call:

    http://localhost:8080/hello/rest/jersey-hello

return

    An Authentication object was not found in the SecurityContextunauthorized