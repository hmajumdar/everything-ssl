# Everything You Ever Wanted to Know About SSL (but Were Afraid to Ask)

This project is a companion piece to the blog post ["Everything You Ever Wanted to Know About SSL (but Were Afraid to Ask)"](http://localhost:4000/blog/2015/12/22/everything-you-ever-wanted-to-know-about-ssl-but-were-afraid-to-ask). 

It is a Java 8 Spring Boot application to demonstrate two-way SSL. It enables both HTTP and HTTPS communication (with client certificates).

Unit tests use Apache's `HttpClient` and `HttpServer`:

* `execute_WithNoScheme_ThrowsClientProtocolExceptionInvalidHostname`
* `httpRequest_Returns200OK`
* `httpsRequest_WithNoSSLContext_ThrowsSSLExceptionPlaintextConnection`
* `httpsRequest_With1WaySSLAndValidatingCertsButNoClientTrustStore_ThrowsSSLException`
* `httpsRequest_With1WaySSLAndTrustingAllCertsButNoClientTrustStore_Returns200OK`
* `httpsRequest_With1WaySSLAndValidatingCertsAndClientTrustStore_Returns200OK`
* `httpsRequest_With2WaySSLAndUnknownClientCert_ThrowsSSLExceptionBadCertificate`
* `httpsRequest_With2WaySSLButNoClientKeyStore_ThrowsSSLExceptionBadCertificate`
* `httpsRequest_With2WaySSLAndHasValidKeyStoreAndTrustStore_Returns200OK`

Integration tests use the Spring Boot application and `TestRestTemplate`:

* `rest_OverPlainHttp_GetsExpectedResponse`
* `rest_WithMissingClientCert_ThrowsSSLHandshakeExceptionBadCertificate`
* `rest_WithUntrustedServerCert_ThrowsSSLHandshakeExceptionUnableFindValidCertPath`
* `rest_WithTwoWaySSL_AuthenticatesAndGetsExpectedResponse`