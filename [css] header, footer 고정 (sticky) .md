### header, footer 고정

HTML

```html
<header> 헤더영역 <header / >

<body> // 스크롤바가 나오는 긴 내용 <body />

<footer> 푸터영역 <footer / >
```

CSS

```jsx
header {
  position: sticky; // 포지션을 스티키로 주면 자연스레 고정된다.
  top: 0;	    // 탑에 붙여야 하므로 0을 준다.
}

footer {
  position: sticky;
  bottom: 0;	    // 여기는 바텀에 붙여야 하므로 0을 준다.
}
```
