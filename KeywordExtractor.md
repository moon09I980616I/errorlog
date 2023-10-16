```java
Exception has occurred: AttributeError
partially initialized module 'yake' has no attribute 'KeywordExtractor' (most likely due to a circular import)
  File "/home/classifi/yake.py", line 26, in <module>
    kw_extractor = yake.KeywordExtractor()
  File "/home/classifi/yake.py", line 1, in <module>
    import yake
AttributeError: partially initialized module 'yake' has no attribute 'KeywordExtractor' (most likely due to a circular import)
```

이 에러가 났을 때 module ~ no attribute ~ 만 보고 module 설치가 제대로 되지 않은 줄 알고 파이썬 경로부터 import error 문제 위주로 계속 살펴봤는데 저 에러 문구를 해석해보니까 모듈이름과 동일하게 파일명을 설정해서 문제가 났었다.
