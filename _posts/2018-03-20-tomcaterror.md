---
title: MAC] Tomcat Server Error:No Output Folder Error
date: 2018-03-20 13:46:47
categories:
- Error
tags:
- tomcat
photos:
- 
---

[MAC] Eclipse Mvn Webapp Project 로 Tomcat Server 실행 시 No output Folder Error 해결방법<br />

# Solving Talk
![]({{ site.url }}/assets/post/tomcatservererror.png)


Tomcat을 Terminal을 통해서 그냥 실행시켰을 경우에도 발생할 수 있다.<br />
그럴 경우엔<br />
```sh
sudo ./startup.sh
```

혹은 Tomcat이 읽기 전용으로 설정되어 있어 일어나는 현상으로

```sh
sudo chown -R {username} {tomcat폴더경로}
```

내 계정에 쓰기권한을 주는 것으로 해결!!


# Reference
- <https://juristr.com/blog/2010/12/tomcat-illegalstateexception-no-output/>

