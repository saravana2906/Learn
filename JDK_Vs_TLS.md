### Issue : 

JDK 1.7 defaults to TLS1.0 and JDK 1.8 deafults to TLS1.2.
When trying to hit the site which is TLS1.2 compliant with application compiled using JDK1.7 we are getting SSL handshake error.
[Source](https://blogs.oracle.com/java-platform-group/diagnosing-tls,-ssl,-and-https)

### Error:
```
javax.net.ssl.SSLHandshakeException: Remote host closed connection during handshake
        at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:946)
        at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1312)
        at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1339)
        at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1323)
        at sun.net.www.protocol.https.HttpsClient.afterConnect(HttpsClient.java:563)
        at sun.net.www.protocol.https.AbstractDelegateHttpsURLConnection.connect(AbstractDelegateHttpsURLConnection.java:185)
        at sun.net.www.protocol.http.HttpURLConnection.getOutputStream(HttpURLConnection.java:1091)
   ```     
### Resolution:

[StackOverflow](https://stackoverflow.com/questions/39157422/how-to-enable-tls-1-2-in-java-7)

As For  standalone  application , we can force the JVM to use TLS1.2.
we can force JDK1.7 to use TLS1.2
 ```
 java -Dhttps.protocols=TLSv1,TLSv1.1,TLSv1.2 -cp "depedencies;." MainProgram
```
