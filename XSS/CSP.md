# CSP(Content Security Policy)

이는 응답 헤더나, meta태그를 통해 아래와 같이 선언해서 사용하며,
각각의 지시어를 적용하여 사이트에서 로드하는 리소스들의 출처를 제한할 수 있습니다.
```json
    { Content-Security-Policy : <지시어>; ... }
```

예를 들면
    defautl-src 'self' *.dreamhack.io*
    