### type error

```jsx
Exception has occurred: TypeError
unsupported format string passed to numpy.ndarray.__format__
  File "/home/classifi-d/bert_classifi04.py", line 117, in test
    print(f"Test F1 Score: {f1:.2f}")
  File "/home/classifi-d/bert_classifi04.py", line 172, in train
    acc = test(test_dataloader, model, device)
  File "/home/classifi-d/bert_classifi04.py", line 188, in run
    train(train_dataloader, test_dataloader, args)
  File "/home/classifi-d/bert_classifi04.py", line 204, in <module>
    run(args)
TypeError: unsupported format string passed to numpy.ndarray.__format__
```

`precision_recall_fscore_support(true, pred, average=None)`

format 함수에서 오류가 났다. aaverage의 값을 micro와 weighted로 했을 때 값이 나왔다.

https://scikit-learn.org/stable/modules/generated/sklearn.metrics.precision_recall_fscore_support.html
https://runebook.dev/ko/docs/scikit_learn/modules/generated/sklearn.metrics.precision_recall_fscore_support

내가 필요한 값은 참, 거짓 이라고 예상하고 micro 값을 넣어서 평가했다.
