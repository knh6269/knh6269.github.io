---
layout: post
title: "Jekyll을 이용해 간단하게 Github 블로그를 만들어보자!"
date: 2023-01-29 14:22:18 +0900
image: 12.jpg
tags: [jekyll, docs]
categories: blog
lastmode: 2023-01-29 14:22:18 +0900
sitemap:
  changefreq: daily
  priority : 1.0
---

<div style = 'width : 48vw; display : flex; align-items: center; flex-direction : column; margin-top : 3vh'>
    <text style = 'font-size : 1.2vw; font-weight : bold'>시작하기 전</text>
    <strong style = 'background-color : yellow; margin-top : 1vh;'>Ruby 를 다운받아주세요! </strong>
    다운받으신 후 Enter만 계속 눌러주세요
    <a style = 'font-weight : bold' href = "https://rubyinstaller.org/downloads/">다운로드 링크</a>
    <img src = 'https://user-images.githubusercontent.com/44117975/215042177-81a7b03f-ae1c-48e4-ab95-df63413d9669.png' 
        style = 'width : 50%; border : 0.5px solid gray; margin-top : 1.2vh;'
    />
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh'>레퍼지토리 생성</text>
    <img src = 'https://user-images.githubusercontent.com/44117975/215030305-e31ab33d-243a-4e2c-a7af-4ef7abe9236d.png' 
        style = 'width : 50%; border : 0.5px solid gray; margin-top : 1.5vh;'
    />
    <br/>
    레퍼지토리 이름은 <strong>반드시</strong>
    <text style = 'background-color : yellow; font-weight : bold'>
        깃허브 아이디.github.io
    </text>
    <img src = 'https://user-images.githubusercontent.com/44117975/215032405-abee8bd0-76d7-42f2-8368-d6d8e79e0a81.png'
        style = 'width : 50%; margin-top : 3vh; border : 0.5px solid gray'
    /> 
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh'>클론 후 접근</text>
    <img src = 'https://user-images.githubusercontent.com/44117975/215038804-53046aa4-c07d-422c-9e5f-bd29a974ae30.png'
        style = 'width : 50%; margin-top : 3vh; border : 0.5px solid gray'
    />
    <img src = 'https://user-images.githubusercontent.com/44117975/215039514-e8f1f8c9-d9a3-4c58-a2b0-b67d48ec6b54.png'
        style = 'width : 50%; margin-top : 3vh; border : 0.5px solid gray; margin-bottom : 1vh;'
    />
     <img src = 'https://user-images.githubusercontent.com/44117975/215040268-3c35ba11-84ca-4856-a60a-932c75ae8d9b.png'
        style = 'width : 20%; height : 5vh;  border : 0.5px solid gray; margin-bottom : 2vh'
    />
    터미널창에 <strong style = 'background-color : yellow;'>git clone 복사붙여넣기 </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>cd 아이디.github.io </strong>
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh; margin-bottom : 1vh'>지킬 다운로드</text>
    터미널창에 <strong style = 'background-color : yellow;'> gem install jekyll bundler </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>jekyll new ./ </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>bundle install </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>bundle exec jekyll serve --trace</strong>
    <text>순서대로 입력</text>
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh'>개설 완료</text>
    <img src = 'https://user-images.githubusercontent.com/44117975/215306279-64dd8609-cd2f-4710-b96c-24772e1c33b3.png'
        style = 'width : 50%; margin-top : 3vh; border : 0.5px solid gray'
    />
    <text>위 그림과 같이 나온다면 아이피 주소를 주소창에 입력</text>
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh; margin-bottom : 1vh'>깃에 올리기</text>
    터미널창에 <strong style = 'background-color : yellow;'> git add . </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>git commit -m '깃 블로그 시작' </strong>
    <strong style = 'background-color : yellow; margin-top: 1vh'>git push origin main</strong>
    <text>순서대로 입력</text>
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh; margin-bottom : 1vh'>주소 입력해보기</text>
    주소창에 <strong style = 'background-color : yellow;'> 아이디.github.io</strong>입력
    <img src = 'https://user-images.githubusercontent.com/44117975/215306667-75a4193e-0eab-47a3-a3af-5c63ffbc15ab.png'
        style = 'width : 50%; margin-top : 3vh; border : 0.5px solid gray; margin-bottom : 1vh'
    />
    <text>이런 화면이 나온다면 성공!</text>
    <text style = 'font-size : 1.2vw; font-weight : bold; margin-top : 5vh'>마치며</text>
    <strong style = 'margin-top : 1vh'>다음은 이제 블로그를 꾸미기 위해 테마를 적용해보자!</strong>

</div>

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
