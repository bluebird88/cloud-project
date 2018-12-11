# cloud-project
基于Spring Cloud的分布式微服务架构

### 测试过程说明：
- 针对：https://www.jianshu.com/p/c987c208859d SpringCloud(八)：API网关整合OAuth2认证授权服务
，测试阶段入口未api网关（8080），不在是上一篇的auth server（8020），否则会出现错误
    因为api网关在application.yml中进行了鉴权配置，其中也隐含了url的映射：
   ```$xslt

#API网关配置
zuul:
  #路由配置
  routes:
    auth:    #认证服务
      #响应的路径
      path: /auth/**   //这里增加了一个auth的虚拟目录
      #敏感头信息
      sensitiveHeaders:
      #重定向到的服务（根据服务id名称从注册中心获取服务地址）
      serviceId:  auth-server
    producer: #生产者服务
      #响应的路径
      path: /producer/**  //这里增加了一个producer的虚拟目录
      sensitiveHeaders:
      #重定向到的服务（根据服务id名称从注册中心获取服务地址）
      serviceId:  producer-service
  #添加代理头
  add-proxy-headers: true
```

- 配置：
    需要支持mongodb、redis、rabbitmq的支持，这些都开在hd02上。
    