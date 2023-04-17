---
layout: post
title: "css position 속성 정리"
date: 2023-04-17 16:10:18 +0900
tags: [css, position]
categories: css
---

# 소개

css position 정리글

# 정리 

## position이란?

HTML 문서상에서 요소가 배치되는 방식을 결정하는 속성 

## position의 종류

- static (default)
- relative
- absolute
- fixed
- sticky

## static 

원래 있어야 하는 `기본적인 위치` 

## relative

`원래 위치`를 기준으로 `top` `bottom` `left` `right` 을 사용해 배치

## absolute

상위 요소중 position이 static이 아닌 요소를 기준으로 `top` `bottom` `left` `top`을 사용해 배치 (없다면 `body`가 기준)

## fixed

뷰포트를 기준으로 `top` `bottom` `left` `top`을 사용해 배치 (항상 정해진 위치에 있는 경우)

## sticky

스크롤하지 않을때 -> static
스크롤 할 때 -> fixed

# 참고 자료

<a href ='https://www.daleseo.com/css-position/'>https://www.daleseo.com/css-position/</a>