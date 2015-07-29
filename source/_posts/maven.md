title: "使用Gradle编译链，在Github上托管一个Maven资源库。"
date: 2015-03-11 18:02:21
tags:
---
1. 在github创建账号，创建Repositories.
2. 创建maven本地仓库目录

          $ mkdir maven
          $ cd maven
          $ mkdir abptrcompat
3. 在代码的build.gradle文件中加入

		apply plugin: 'maven'
		uploadArchives {
		    repositories.mavenDeployer {
		        repository(url: "file:///Users/yangzhixin/maven/abptrcompat/")
		        pom {
		            version = '1.0.0'
		            artifactId = 'yzx-abptrcompat'
 		           groupId = 'com.yzx'
 		       }
		    }
		} 
4. 编译上传到本地仓库

		$ gradle clean build uploadArchives
5. 进入本地仓库目录 maven/abptrcompat

		$ git init
          $ git remote add remotecompat https://github.com/yzx41099298/abptrcompat.git
          $ git add .
          $ git commit -m “abcompat-1.0.0”
          $ git push remotecompat master
6. 在调用库的build.gradle中加入

		repositories {
			maven{ url "https://github.com/yzx41099298/abptrcompat/raw/master/"}
		}

		dependencies {
		    compile 'com.yzx:yzx-abptrcompat:1.0.0@aar'
		} 

参考：http://downright-amazed.blogspot.com/2011/09/hosting-maven-repository-on-github-for.html