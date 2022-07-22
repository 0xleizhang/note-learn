curl -v [https://bitseatech.com](https://bitseatech.com)

 过程：

握手分两个阶段，认证校验->交换key, 1次数据加密传输

client hello 版本，支持的加密方式 ->

server hello -返回证书 key->

client 交换key ->

server 交换key ->

![image.png](1616937786886-49b676ae-a26c-4701-abe7-559889f721d2.png)
\`\`\`
\\* Trying 8.136.159.28...
\\* TCP\_NODELAY set
\\* Connected to bitseatech.com (8.136.159.28) port 443 (#0)
\\* ALPN, offering h2
\\* ALPN, offering http/1.1
\\* successfully set certificate verify locations:
\\* CAfile: /etc/ssl/cert.pem
 CApath: none
\\* TLSv1.2 (OUT), TLS handshake, Client hello (1):
\\* TLSv1.2 (IN), TLS handshake, Server hello (2):
\\* TLSv1.2 (IN), TLS handshake, Certificate (11):
\\* TLSv1.2 (IN), TLS handshake, Server key exchange (12):
\\* TLSv1.2 (IN), TLS handshake, Server finished (14):
\\* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
\\* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
\\* TLSv1.2 (OUT), TLS handshake, Finished (20):
\\* TLSv1.2 (IN), TLS change cipher, Change cipher spec (1):
\\* TLSv1.2 (IN), TLS handshake, Finished (20):
\\* SSL connection using TLSv1.2 / ECDHE-ECDSA-AES128-GCM-SHA256
\\* ALPN, server accepted to use h2
\\* Server certificate:
\\* subject: CN=bitseatech.com
\\* start date: Feb 3 08:37:39 2021 GMT
\\* expire date: May 4 08:37:39 2021 GMT
\\* subjectAltName: host "bitseatech.com" matched cert's "bitseatech.com"
\\* issuer: C=US; O=Let's Encrypt; CN=R3
\\* SSL certificate verify ok.
\\* Using HTTP2, server supports multi-use
\\* Connection state changed (HTTP/2 confirmed)
\\* Copying HTTP/2 data in stream buffer to connection buffer after upgrade: len=0
\\* Using Stream ID: 1 (easy handle 0x7fad6800e000)
\> GET / HTTP/2
\> Host: bitseatech.com
\> User-Agent: curl/7.64.1
\> Accept: \*/\*
\>
\\* Connection state changed (MAX\_CONCURRENT\_STREAMS == 250)!
< HTTP/2 200
< accept-ranges: bytes
< content-type: text/html; charset=utf-8
< last-modified: Wed, 24 Mar 2021 10:03:14 GMT
< content-length: 5158
< date: Sun, 28 Mar 2021 13:19:59 GMT
<
破茧♥️给有价值的信息投票，获得有价值的信息

\\* Closing connection 0

\`\`\`