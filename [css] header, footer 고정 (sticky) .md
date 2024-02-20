### header, footer 고정

HTML

```html
<body>
	<header> // 헤더 영역 // </header>
	<article> // 내용 // </article>
	<footer> // 푸터 영역 // </footer>
</body>
```

CSS

```jsx
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0;
}

article {
  flex: 1; /* article 요소가 남은 공간을 채우도록 함 */
}

footer {
  flex-shrink: 0; /* footer 요소가 브라우저 크기보다 작아질 수 없도록 함 */
}
```
