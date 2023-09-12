- 에러 내용
```jsx
can't convert cuda:0 device type tensor to numpy. Use Tensor.cpu() to copy the tensor to host memory first.
```

- 에러 원인
  -  gpu에 할당되어 있는 텐서를 numpy 배열로 변환할 때 생기는 에러

- 해결
  - model에 gpu 할당
