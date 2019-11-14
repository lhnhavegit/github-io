---
layout: post
categories:
  - ACM
  - Template
tags: MAVEN
date: 2019-10-17 14:10:33
---
## No plugin found for prefix 'install' in the current project解决方案
maven 使用的setting配置文件为默认配置文件，未修改，运行install时报如下错误
命令：
```java
mvn install:install-file -Dfile=td-pay-3.0.1.jar -DgroupId=com.tdlbs.pay -DartifactId=td-pay -Dversion=3.0.1 -Dpackaging=jar
```
配置文件如下：
```dtd
  <mirrors>
    <!-- mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |
    <mirror>
      <id>mirrorId</id>
      <mirrorOf>repositoryId</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://my.repository.com/repo/path</url>
    </mirror>
     -->
  </mirrors>
```
错误信息：
```java
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 5.464 s
[INFO] Finished at: 2019-10-17T13:40:27+08:00
[INFO] Final Memory: 9M/155M
[INFO] ------------------------------------------------------------------------
[ERROR] No plugin found for prefix 'install' in the current project and in the plugin groups [org.apache.maven.plugins, org.codehaus.mojo] available from the repositories [local (C:\my\.m2\repo), nexus (http://g.lordar.com:8081/nexus/content/groups/public/), lordar (http://g.lordar.com:8081/nexus/content/groups/public/)] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/NoPluginFoundForPrefixException
```
只需要添加一个镜像配置就可以了
```dtd
<mirror>
	<id>maven2</id>
	<mirrorOf>*</mirrorOf>
	<name>maven</name>
	<url>http://repo1.maven.org/maven2 </url>
</mirror>
```
