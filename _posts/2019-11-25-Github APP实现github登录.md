---
title: Github APP实现github登录
layout: post
author: Wu
tags: 学习笔记 GitHub APP
---

# Github APP实现github登录

### 注册github APP 

登录github后的操作步骤

1.创建一个OAuth App

<img src="https://ws1.sinaimg.cn/large/ba7713efgy1g98fp6vymbj20y10d6dh4.jpg"/>

2.填写信息

<img src="https://ws1.sinaimg.cn/large/ba7713efgy1g9a069k975j20fv0fgq3s.jpg"/>

3.创建成功后会给一个Client ID和Cilent Secret，没人使用这个APP进行第三方登录的话，显示的是0 user

<img src="https://ws1.sinaimg.cn/large/ba7713efgy1g9a081wtyoj20ao06f3yn.jpg"/>

### 登录流程

1.用户访问BBS

2.点击登录，BBS先执行自己的业务逻辑

3.调用authorize接口访问GitHub

4.GitHub回调一个uri，携带code

5.BBS调用access_token接口携带code

6.验证通过的话会返回一个真正的token

7.使用token用user接口进行认证

8.返回用户信息

9.存入数据，更新登录状态

10.返回给用户登录成功的信息

```sequence
User->>BBS: 1.访问
BBS->>BBS:2.登录
BBS->>GitHub:3.authorize
GitHub->>BBS: 4.回调redirect-uri携带code
BBS->>GitHub:5.access_token携带code
GitHub-->BBS:6.返回access_token
BBS->>GitHub:7.user接口携带access_token
GitHub-->BBS:8.返回User信息
BBS->>BBS:9.存入数据，更新登录状态
BBS->>User:10.登录成功
```

[OAuth documentation](https://developer.github.com/apps/building-oauth-apps/authorizing-oauth-apps/) OAuth文档

### 1.返回code

```
项目中访问的接口：https://github.com/login/oauth/authorize?client_id=0edababf293cfd3a6950&redirect_uri=http://localhost:8887/callback&scope=user&state=1
```

```
`client_id`
```
### 2.使用code请求API返回token

#### 模拟http请求

[okhttp官网](https://square.github.io/okhttp/)

##### GET方式

```java
OkHttpClient client = new OkHttpClient();

String run(String url) throws IOException {
  Request request = new Request.Builder()
      .url(url)
      .build();

  try (Response response = client.newCall(request).execute()) {
    return response.body().string();
  }
}
```

##### POST方式

```java
public static final MediaType JSON
    = MediaType.get("application/json; charset=utf-8");

OkHttpClient client = new OkHttpClient();

String post(String url, String json) throws IOException {
  RequestBody body = RequestBody.create(JSON, json);
  Request request = new Request.Builder()
      .url(url)
      .post(body)
      .build();
  try (Response response = client.newCall(request).execute()) {
    return response.body().string();
  }
}
```

引入okhttp相关依赖

```
<!-- okhttp -->
<dependency>
	<groupId>com.squareup.okhttp3</groupId>
	<artifactId>okhttp</artifactId>
	<version>3.14.1</version>
</dependency>
```

封装一个请求参数类

```java
public class AccessTokenDTO {
    private String client_id;
    private String client_secret;
    private String code;
    private String redirect_uri;
    private String state;
	//省略getter/setter方法
}
```

封装OKHTTP模拟请求

请求接口：`https://github.com/login/oauth/access_token`

参数：就是上面类中的五个

```java
@Component   //使用这个注解，对象自动实例化到spring的上下文中，使用时直接拿来用就可以
public class GithubProvider {
    public String getAccessToken(AccessTokenDTO accessTokenDTO) {
        MediaType JSON = MediaType.get("application/json; charset=utf-8");
        OkHttpClient client = new OkHttpClient();
        RequestBody body = RequestBody.create(JSON, json);
        Request request = new Request.Builder()
                .url("https://github.com/login/oauth/access_token")
                .post(body)
                .build();
        try (Response response = client.newCall(request).execute()) {
            String string = response.body().string();
            return string;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

### 3.使用token获得用户信息

请求api：`GET https://api.github.com/user`

参数：access_token

封装GitHubUser对象

```java
public class GithubUser {
    private String name;
    private Long id;
    private String bio;
}
```

使用OKhttp模拟get请求获得user信息

```java
public GithubUser getUser(String access_token) {
	OkHttpClient client = new OkHttpClient();
	Request request = new Request.Builder().url("https://api.github.com/user?access_token="+access_token).build();
		try (Response response = client.newCall(request).execute()) {
			String string = response.body().string();
			GithubUser githubUser = JSON.parseObject(string, GithubUser.class);
 			return githubUser;
		} catch (IOException e) {
			e.printStackTrace();
		}
 	return null;
}
```

