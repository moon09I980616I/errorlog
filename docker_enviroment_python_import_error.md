### import error

```jsx
Traceback (most recent call last):
  File "/usr/local/bin/transformers-cli", line 5, in <module>
    from transformers.commands.transformers_cli import main
  File "/usr/local/lib/python3.8/dist-packages/transformers/commands/transformers_cli.py", line 24, in <module>
    from .pt_to_tf import PTtoTFCommand
  File "/usr/local/lib/python3.8/dist-packages/transformers/commands/pt_to_tf.py", line 24, in <module>
    from .. import (
  File "<frozen importlib._bootstrap>", line 1039, in _handle_fromlist
  File "/usr/local/lib/python3.8/dist-packages/transformers/utils/import_utils.py", line 1121, in __getattr__
    value = getattr(module, name)
  File "/usr/local/lib/python3.8/dist-packages/transformers/utils/import_utils.py", line 1120, in __getattr__
    module = self._get_module(self._class_to_module[name])
  File "/usr/local/lib/python3.8/dist-packages/transformers/utils/import_utils.py", line 1132, in _get_module
    raise RuntimeError(
RuntimeError: Failed to import transformers.models.auto.image_processing_auto because of the following error (look up to see its traceback):
initialization failed
```

python 버전 변경해서 나온 에러 같은데 확실한 원인이라고 생각 안한다.

파이썬 환경변수도 변경해보고 껐다켜보고 트렌스포머와 파이썬 버전도 확인해봤지만 트랜스포머는 4.11 파이썬은 3.7로 버전도 맞아서 방법이 없어서 도커 환경을 삭제하고 다시 깔았을 때 됐다.
