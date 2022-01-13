1 编码器选择错误 urlEncode not encode

2 第二 填充的=号 转义成%3D 再反转异常 [https://www.codenong.com/6916805/](https://www.codenong.com/6916805/)

\`\`\`
 public static void main(String[] args) throws UnsupportedEncodingException {
 String str = "sflsfsldfasdfsadfsadfsa as";
 byte[] encode = Base64.getEncoder().encode(str.getBytes(StandardCharsets.UTF\_8));
 String s = new String(encode, "utf-8");
 System.out.println(s);
 byte[] decode = Base64.getDecoder().decode(s);
 System.out.println(new String(decode, "utf-8"));
 byte[] decode2 = Base64.getDecoder().decode("c2Zsc2ZzbGRmYXNkZnNhZGZzYWRmc2EgYXM");
 System.out.println(new String(decode2, "utf-8"));
 //=符号转义成%3D再转回来异常 ，=号起填充作用
 byte[] decode3 = Base64.getDecoder().decode("c2Zsc2ZzbGRmYXNkZnNhZGZzYWRmc2EgYXM%3D");
 System.out.println(new String(decode3, "utf-8"));
 }


 private static String getLoginUrl(String pageUrl, String signInToken) throws URISyntaxException {
 URIBuilder builder = new URIBuilder("https://signin.aliyun.com/federation");
 builder.setParameter("Action", "Login");
 // 登录失效跳转的地址，一般配置为自建WEB配置302跳转的URL
 builder.setParameter("LoginUrl", "https://signin.aliyun.com/login.htm");
 builder.setParameter("SigninToken", signInToken);
 // 实际访问 DAS 的页面，比如全局大盘，实时大盘，某个实例详情等
 builder.setParameter("Destination", pageUrl);
 HttpGet request = new HttpGet(builder.build());
 return request.getURI().toString();
 }
\`\`\`