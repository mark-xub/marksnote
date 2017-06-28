---
title: spring aop VS aspectj VS cglib
date: 2017-06-28 13:28:37
tags: [web]
---

最近做的一个项目，是需要用到aop拦截的，顺便总结一下，感觉概念比较绕。  
简单点来说，spring aop 和 aspectj 都是做aop拦截的框架，而cglib是和jdk动态代理一样是用来生成代理类的库。aspectj支持编译/加载织入 。
<!-- more -->
## spring aop
spring aop 是spring 大家庭中的一员，它支持jdk动态代理以及cglib代理。默认对于有接口的实现，spring使用jdk动态代理；对于没有接口的实现，使用cglib代理。当指定(springboot 应用)
```
spring.aop.proxy-target-class=true
```
都是使用cglib代理。  
因为 spring aop出来之前aspectj做为一个优秀的框架已经出现了，所以spring aop中沿用了aspectj里面的annotation，比如@Aspect,@Before等，所以这里就是容易混淆的地方。 

## aspectj
aspectj有自己的字节码生成方式，当然也可以指定用cglib代理。
使用aspectj，可以做一些使用jdk动态代理和cglib代理无法做到的事情，比如对final类，private方法或者调用自己内部方法时，这时候就需要aspectj的编译时织入。在maven build 下添加aspectj 插件。
```
<plugin>
				<groupId>org.codehaus.mojo</groupId>
				<artifactId>aspectj-maven-plugin</artifactId>
				<version>1.4</version>
				<dependencies>
					<dependency>
						<groupId>org.aspectj</groupId>
						<artifactId>aspectjrt</artifactId>
						<version>${aspectj.version}</version>
					</dependency>
					<dependency>
						<groupId>org.aspectj</groupId>
						<artifactId>aspectjtools</artifactId>
						<version>${aspectj.version}</version>
					</dependency>
				</dependencies>
				<executions>
					<execution>
						<phase>process-sources</phase>
						<goals>
							<goal>compile</goal>
							<goal>test-compile</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<outxml>true</outxml>
					<source>${java.version}</source>
					<target>${java.version}</target>
				</configuration>
			</plugin>
``` 



