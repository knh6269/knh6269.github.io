---
layout: post
title: "react-query"
date: 2023-04-09 14:10:18 +0900
tags: [react query, develop]
categories: react query
---

# 소개
react-query에 대해 정리해보는 글 

---

# react-query란?
`react-query` 서버의 값을 클라이언트에 가져오는 fetch, 캐싱, 에러처리 등의 비동기 과정을 편하게 해주는 라이브러리
보통 redux를 사용해 상태관리를 하는 경우 서버 관련 로직을 클라이언트 state와  함께 사용하게 되는 경우가 많다
이러한 경우 보일러 플레이트가 너무 커지는데 이러한 현상을 방지하기 위해 서버관련 로직을 redux에서 분리시킨다
이때 사용되는게 `react-query`이다

---

# react-query를 쓰는 이유 
- 캐싱
- 데이터가 `stale`한 상태가 되면 다시 `get` 
- `get`한 데이터가 변경되면 다시 `get` 수행 
    - react의 `state`와 유사
- 동일 데이터를 여러번 요청하면 한번만 요청 
    - `debounce`와 유사

---

# 사용법 
```
npm i react-query
```

최상단 컴포넌트를 QueryClient 태그로 감싸준다.

```javascript
import {QueryClient} from "react-query";

const Index = () => {
    const queryClient = new QueryClient();

    return(
    <QueryClientProvider client={queryClient}>
        <App />
    </QueryClientProvider>
    );
}
```


---

# useQuery - get
```js
const { isLoading, isError, error, data } = useQuery(쿼리키, 쿼리함수, 옵션)

if (isLoading) return 'Loading...'
if (isError) return `오류 이유 : ${error.message}`
```

- `isLoading` : API 호출이 진행 중인지 여부를 나타내는 `boolen`값
- `isError` : API 호출 실패 여부를 나타내는 `boolean`값
- `error` : API 호출 중에 발생한 오류정보를 가지고 있는 객체 
- `data` :  API 호출 결과를 나타내는 데이터 객체. 이전에 동일한 `queryKey`로 `useQuery` 를 호출한 경우, `캐시`된 데이터를 반환

```js
const { status, error, data } = useQuery(쿼리키, 쿼리함수, 옵션)

if (status === 'loading') return 'Loading...'
if (status === 'error') return `오류 이유 : ${error.message}`
```

- 다음과 같이 isLoading, isError을 status로 한번에 사용이 가능

- `쿼리키` 
    - 유니크한 키
    - `캐시`를 저장하는데 사용 
    - 동일한 쿼리에 여러 번 요청하는것을 방지
    - react-query v4 버전 이상에서는 쿼리키를 `배열 형태`로 전달해야한다.
    - 배열을 전달 시 0번 배열은 '유니크한 키', 1번 배열은 props가 전달된다.
- `쿼리함수` 
    - 데이터를 가져오는 역할을 하는 `비동기`함수 
    - 이 함수의 반환값은 `data` 변수에 저장
    - `useQery` hook에서 호출될 때 마다 실행
    - `refetch` 메서드를 호출하여 수동으로 다시 호출이 가능
- `옵션`
    - 훅에 대한 옵션 객체
    - `enabled` 
        - `true`로 설정하면 `useQuery`가 컴포넌트가 마운트될 때 자동으로 API 호출을 시작 
        - `false`로 설정하면 컴포넌트가 마운트 되어도 API 호출을 하지않는다.
    - `staleTime`
        - 캐시된 데이터가 만료되기 전에 허용되는 시간
        - 데이터가 fresh에서 stale 상태로 변경되는데 걸리는 시간 (3000 : 3초)
        - 만료된 데이터가 있으면 API 호출을 시작 
        - 기본값 : 0
    - `cacheTime`
        - 캐시된 데이터를 유지할 시간
        - 이 시간이 지나면 캐시된 데이터가 삭제 
        - 기본값 : 5분
    - `refetchOnMount`
        - 데이터가 `stale` 상태일 경우, `mount`마다 `refetch`를 실행하는 옵션
        - 기본값 : `true`
    - `refetchOnWindowFocus`
        - 데이터가 `stale`상태일 경우 `윈도우 포커싱`될 때마다 `refetch`를 실행하는 옵션
        - 기본값 : `true`
    - `refetchInterval`
        - `시간`을 값으로 넣어주면 일정 시간마다 자동으로 `refetch`를 실행하는 옵션
        - `polling`을 위해 사용 
    - `refetchIntervalInBackground`
        - 탭/창이 백그라운드에 있어도 `refetch`를 실행하는 옵션 
        - `polling`을 위해 사용 
    - `retry`
        - 쿼리가 `실패`하면 `useQuery`를 일정 횟수만큼 `refetch`하는 옵션
        - false : 재요청하지 않음
        - ture : 무한 재요청
        - 숫자 : 그 숫자만큼 재요청
    - `select`
        - 데이터의 일부를 변환하거나 선택이 가능 
    - `keepPreviousData`
        - 쿼리키가 변경되어 새로운 데이터를 요청하는 동안에도 마지막 data 값을 유지
        - 캐싱 되지 않은 페이지를 가져올 때 깜빡거리는 현상을 방지할 수 있다.

---

# useQueries - get 
한 파일에 여러 비동기가 존재하는 경우 한번에 처리가 가능 

```js
const result = useQueries([
    {
        queryKey: ["getStore", city],
        queryFn: () => getStore(city)
    },
    {
        queryKey: ["getLocation", city],
        queryFn: () => getLocation(city)
    }
])
```


---

# useMutation - post
```js
const { mutate, isLoading, isError, error } = useMutation(쿼리함수, {
    onSuccess: (data) => {
        console.log(data)
    }
})

mutate({
    title: e.target[0].value
    description: e.target[1].value 
})

if (isLoading) return 'Loading...'
if (isError) return `Error:${error.message}`
```

`update`후에 `get`을 다시 실행하고 싶을때 `invalidateQueries(쿼리키)`를 사용

```js
const mutation = useMutation(postTodo, {
  onSuccess: () => {
    queryClient.invalidateQueries("getStore");
  }
});
```

---

# Refetching을 하는 경우
data 가 `stale` 한 상태가 되었다고 판단되는 경우
-  브라우저에 포커스가 들어왔을 경우 
- 새로 마운트가 되었을 경우
- 네트워크가 끊어졌다가 다시 연결된 경우

---

# 쿼리 무효화
`ADD`, `DELETE` 후 수동적으로 `refetch`를 해줘야 화면에 보여진다.
이러한 문제를 `Invalidation`을 사용하면 해결할 수 있다.
```js

 const { mutate, isLoading, isError, error } = useMutation(store, {
    onSuccess: () => {
        queryClient.invalidateQueries();
        queryClient.invalidateQueries('store');
    }
  });
```

---

# 이 글에서 사용된 다른 개념

>컴포넌트 mount란?

- 컴포넌트 생성부터, 최초 렌더링까지의 과정
- 마운트될 때 
    - props로 받은 값을 컴포넌트의 state로 설정할 때
    - 컴포넌트가 나타났을때, 외부 API를 요청해야할 때
    - 라이브러리를 사용할 때
    - setInterval이나 setTimeout과 같은 작업을 할 때
    <br/>

>polling이란?

- 일정한 주기를 가지고 서버와 응답을 주고받는 방식
- `refetchInterval`, `refetchIntervalInBackground`을 이용해서 구현 가능

---

# 출처 

<a href = 'https://kyounghwan01.github.io/blog/React/react-query/basic/'>https://kyounghwan01.github.io/blog/React/react-query/basic/</a>
<br/>
<a href = 'https://github.com/ssi02014/react-query-tutorial'>https://github.com/ssi02014/react-query-tutorial</a>
