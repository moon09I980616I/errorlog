### ValueError: Found input variables with inconsistent numbers of samples: [394428, 788856]

```jsx
Traceback (most recent call last):
  File "/home/classifi/bert_ev2.py", line 89, in <module>
    test_metrics = compute_metrics(test_results, test_label)
  File "/home/classifi/bert_ev2.py", line 27, in compute_metrics
    precision, recall, f1, _ = precision_recall_fscore_support(labels, preds, average=None)
  File "/usr/local/lib/python3.8/dist-packages/sklearn/utils/_param_validation.py", line 211, in wrapper
    return func(*args, **kwargs)
  File "/usr/local/lib/python3.8/dist-packages/sklearn/metrics/_classification.py", line 1721, in precision_recall_fscore_support
    labels = _check_set_wise_labels(y_true, y_pred, average, labels, pos_label)
  File "/usr/local/lib/python3.8/dist-packages/sklearn/metrics/_classification.py", line 1499, in _check_set_wise_labels
    y_type, y_true, y_pred = _check_targets(y_true, y_pred)
  File "/usr/local/lib/python3.8/dist-packages/sklearn/metrics/_classification.py", line 84, in _check_targets
    check_consistent_length(y_true, y_pred)
  File "/usr/local/lib/python3.8/dist-packages/sklearn/utils/validation.py", line 409, in check_consistent_length
    raise ValueError(
ValueError: Found input variables with inconsistent numbers of samples: [394428, 788856]
```

평가하려고 배치 돌릴 때 실수로 `test_results.extend(preds.cpu().numpy())` 이 코드를 두 번 넣었다😅
