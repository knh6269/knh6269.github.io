---
layout: post
title: "react native webview 로컬 개발환경 구성(Expo)"
date: 2023-02-25 15:10:18 +0900
tags: [react-native, expo]
categories: react-native
---

# 소개
하이브리드 앱을 제작 중 mac 이 없는 사람들의 경우에는 `xCode`를 사용할 수 없어 `Expo`를 사용할것이다.<br/>
그 과정에서 `휴대폰`을 활용해 `web`의 `localhost`를 `webview`에 띄워 개발하고 싶은 사람들이 있을것이다.<br/>
오늘은 그 과정을 소개하고자 한다.

---

# react (web) 쪽 환경 구성
## react 다운로드
```
npm install -g create-react-app
```

## react 기반 프로젝트 생성
```
create-react-app my-app
```

## 내 프로젝트로 이동
```
cd my-app
```
아래 코드들은 잘 되는지 확인을 위한 코드입니다 ㅎ
## App.js 다 지우고 해당 코드로 수정 
``` javascript
import './App.css';

function App() {
  return (
    <div className="App">
      성공이요~
      이얏호우!
      
    </div>
  );
}

export default App;
```
## App.css 다 지우고 해당 코드로 수정
``` css
.App {
  text-align: center;
  justify-content: center;
  align-items: center;
  display :flex;
  height: 90vh;
  font-size : 10vw;
  background-color: yellow;
}
```
## 프로젝트 시작
```
npm start
```

## 아래와 같이 나오면 성공
<div>
    <img src=  'https://user-images.githubusercontent.com/44117975/221342835-e7a3f0ad-5f7b-4a87-9ea5-7de872385610.png' alt = 'img1'/>
</div>


---

# react-native (native) 쪽 환경 구성
## expo-cli 다운로드
```
npm install --global expo-cli
```

## expo 기반 프로젝트 생성
```
expo init my-project
```

## 내 프로젝트로 이동
```
cd my-project
```

## react-native-webview 다운로드
```
expo install react-native-webview
```

## App.js 다 지우고 해당 코드로 수정 
<div>
  <img src= 'https://user-images.githubusercontent.com/44117975/221343962-73c5d4ce-c112-4af4-8eed-81d374a72d4b.png' alt = 'img'/>
</div>
여기서 `구글 화면`이 제대로 나오면 성공입니다.<br/>
이제 `localhost`로 작업을 하기위한 환경 설정을 위해 `핸드폰의 와이파이`와 `노트북의 와이파이`를 일치시킵니다.
그리고 react에서 npm start를 했을때 적혀있는 `On Your Network` 코드를 `WebView`의 `uri`에 입력합니다.<br/>
## expo 시작
```
expo start
```

## qr 코드 인식
1. App store의 `Expo go`를 다운로드 받습니다. <br/>
2. `react-native-expo(native)` 프로젝트에서 `c`를 눌러줍니다 <br/>
3. 나온 qr 코드를 기본 카메라를 이용해 인식해줍니다.<br/>
4. 화면이 제대로 나오면 성공!<br/>

# 내가 겪은 오류
```
Domain: NSURLErrorDomain 
Error Code: -1001
Description: The request timed out.
```
와이파이를 일치시켰지만 휴대폰에서는 프로젝트가 실행되지가 않고 아래 사진만 나왔다<br/>
구글링도 해봤지만 어떠한것을 적용해도 해결되지 않았다. 그러다 문득 든 생각<br/>
"이게 같은 와이파이라면 `react` 프로젝트 `ip` 를 핸드폰 주소창에 넣어도 나오지 않을까??"<br/>
하지만 나오지 않았고 아이피의 문제라는것을 알았다. 같은 와이파이라도 다르게 적용이 될 수 있구나!<br/>
바로 `cmd` 창을 켜 `ipconfig를` 해본 결과<br/> 
1. `react` 프로젝트에서 알려준 ip는 `이더넷의 ip주소`고 <br/>
2. 핸드폰은 `무선 LAN ip 주소`를 가지고 있기때문에 안되고 있었다.<br/>

`무선 LAN 주소`를 `webview의` `uri`에 입력했더니 잘 나왔다!

<div style = 'display : flex'>
    <img style = 'width : 90%' src = 'https://user-images.githubusercontent.com/44117975/221343116-87cc4641-713c-45c0-a1da-91e34f113411.png' alt = 'img2'/>
    <img style = 'width : 90%' src ='https://user-images.githubusercontent.com/44117975/221343419-c659e8ed-41b5-4790-b560-b0b9f5ce7651.png' alt = 'img3'/>
</div>

# 마치며
맥북이 있었다면 Xcode로 이렇게 힘들지 않았을텐데...





