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
    - 캐시를 저장하는데 사용 
    - 동일한 쿼리에 여러 번 요청하는것을 방지
    - react-query 3.14.0 버전 이상에서는 쿼리키를 배열 형태로 전달하는 것을 권장하고 있다. 
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
        - 만료된 데이터가 있으면 API 호출을 시작 
        - 기본값 : 0
    - `cacheTime`
        - 캐시된 데이터를 유지할 시간
        - 이 시간이 지나면 캐시된 데이터가 삭제 
        - 기본값 : 5분


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

# 출처 
https://kyounghwan01.github.io/blog/React/react-query/basic/