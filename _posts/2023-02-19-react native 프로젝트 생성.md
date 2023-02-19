---
layout: post
title: "react native 프로젝트 생성하기(2023년, window 기준)"
date: 2023-01-29 14:22:18 +0900
tags: [react-native, webview]
categories: react-native
---

# 소개
react native프로젝트를 생성하는 중 발생한 오류와 해결방법 소개 

# 과정

## choco 설치
cmd 창을 관리자 권한으로 실행한 후 아래 명령어 입력
```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```


## node js 설치
위에서 설치한 choco를 활용해 node js를 설치한다
아래 명령어 입력
```
choco install -y nodejs.install
```


## react native cli 설치
아래 명령어 입력
```
npm install -g react-native-cli 
```

## jdk 설치
여기서 다른 블로그 글을 참고해 설치했는데 버전이 11 이하라서 오류가 발생했다.
<a style = 'border-bottom : none' href = 'https://www.oracle.com/kr/java/technologies/javase/jdk11-archive-downloads.html'>여기서 다운받아 해결했다!</a><br/>

## 잘 설치 되었는지 확인하기 위해 아래 명령어 입력
``` 
choco -version
```
``` 
node -version
```
``` 
npx react-native --version
```
``` 
java -version
```

## android studio 설치
<a style = 'border-bottom : none;' href = 'https://developer.android.com/studio'>여기서 설치</a><br/>
쭉 쭉 next를 누른후 설치가 완료되었다면 Basic Activity프로젝트 생성 ↓
<img src = 'https://user-images.githubusercontent.com/44117975/219950477-1bb01750-d253-4cc9-a401-8a59e27cffaf.png' alt = 'android'/>
아래 명령어 꾹
```
ctrl + alt + s
```
JDK를 아까 설치한 11버전으로 변경
<img src = 'https://user-images.githubusercontent.com/44117975/219950753-42f7b612-d9b1-4c53-8ef0-fa391f1eb25d.png' alt = 'android2'/>

## 환경변수 설정
윈도우 검색창에 `시스템 환경 변수 편집` 검색
<div style ='display : flex'>
    <img  src = 'https://user-images.githubusercontent.com/44117975/219951125-7d8be915-143f-42d2-be41-2e773295f324.png' alt = 'android3'/>
    <img  src = 'https://user-images.githubusercontent.com/44117975/219951253-4596c143-f74d-4663-960b-7e690ac2daa0.png' alt = 'android4'/>
</div>
<br/>
새로운 사용자 변수 생성<br/>
이때 변수 값은 `Sdk 위치`로 해줘야한다
<img src = 'https://user-images.githubusercontent.com/44117975/219951405-cb4d344e-bc90-48d5-90c1-77101fe29b21.png' alt = 'android5'/>

<br/>
이후 `path`라는 사용자 변수 클릭 후 새로 만들어준다. <br/>
이때 주소는 위의 Sdk 위치 하위 `platform-tools`폴더로 작성후 확인버튼 꾹
<img style = 'width : 100vw' src = 'https://user-images.githubusercontent.com/44117975/219951647-b2cb3a48-2ff3-4ee5-b5d3-cdaf9dd8438b.png' alt = 'android6'/>

<br/>
모두 잘 했다면 아래 명령어를 cmd 창에 입력
``` 
adb
```
아래와 같은 결과가 나왔다면 성공!
```
Android Debug Bridge version 1.0.41
Version 29.0.1-5644136
Installed as /Users/dev-yakuza/Library/Android/sdk/platform-tools/adb
```

## react native 프로젝트 생성
커맨드 창에 아래 명령어 입력
```
npx react-native init SampleApp
```
성공적으로 만들어졌다면 아래 명령어 입력
```
cd SamplApp
react-native start
```

## 완료
아래 화면이 애뮬레이터에 나온다면 성공<br/>
<div>
    <img style = 'width : 10vw;  margin-top : 1vh; ' src = 'https://user-images.githubusercontent.com/44117975/219952242-8f539f84-6407-44f5-b7a3-457f6421722d.png' alt = 'react-native1'/>
</div>

# 내가 발생한 오류들

### 1. 프로젝트 생성을 했지만 app.js 가 생기지 않는 오류
### 2. cli.init is not a function 오류 
이 두가지 오류 모두 한방에 해결했다. 왜인지 모르겠으나 <br/>
1. 프로젝트를 시작할 폴더를 생성 후 
2. 해당 폴더로 이동하는 과정<br/>

위 과정을 두번 거치고 프로젝트 생성을 해줬더니 해결이 됐다.<br/>
즉
`react-native-practice\practice\` 위치에서 아래 명령어를 입력해주니 해결이 되었다.
```
npx react-native init practice
```

### 3. Jdk 버전때문에 발생한 오류
위 과정을 모두 해 준뒤 실행을 했더니 아래 문구가 발생했다.
```
A problem occurred evaluating project ':app'.
> Failed to apply plugin 'com.android.internal.application'.
   > Android Gradle plugin requires Java 11 to run. You are currently using Java 1.8.
      Your current JDK is located in C:\Program Files\Java\jdk1.8.0_211\jre
```
적혀있는 그대로 java 버전때문에 발생한 문제인데 <br/>
자바 11을 설치하고 android studio에서 경로를 변경해줘도 해결이 되지 않았다. <br/>
환경 변수 설정중 `사용자 변수`가 아닌 `시스템 변수의 path`로 이동후 
<br/>`jdk11`을 제외한 jdk 설정을 모두 `제거`해주었더니 해결되었다.

# 마치며
옛날 자바 버전때문에 꽤나 고생을 했다. 환경변수의 중요함을 새삼 느꼈다..