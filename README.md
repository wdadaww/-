# lateinit
지연초기화

늦은초기화 라 함은, 말그대로 객체 초기화를 늦게하는 것이다.

![image](https://user-images.githubusercontent.com/117493614/200717605-e0e8daeb-00d7-4ed3-aefe-3fb070f632d5.png)


lateinit 을 사용하여 
text변수를 선언해줬고, 이후에 어떤 동작의 결과 값을 기반으로 text 를 초기화 해주는 것을 확인할 수 있다.

이후에 또 한 번 값을 바꾸는 것을 확인할 수 있는데, lateinit 변수 선언부를 자세히 보면 var 로 선언되어 있다. lateinit 을 사용하면 늦은 초기화 이후에도 값이 계속하여 바뀔 수 있다.

그럼, 만약 lateinit 을 사용해놓고 늦은 초기화조차 하지 않은 경우는 어떻게 될까?
Exception in thread "main" kotlin.UninitializedPropertyAccessException: lateinit property text has not been initialized

이런식으로 컴파일 단계에서 오류가 발생하기 때문에 잠재적 오류를 방지해주기도 한다.


