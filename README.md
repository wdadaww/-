# 고차함수 -> 람다식




![image](https://user-images.githubusercontent.com/117493614/200719897-bd21894e-1c8f-449d-9b7c-2d27e0f8f413.png)



람다식, 또는 람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수 (Anonymous Functions)를 지칭하는 용어이다.
람다 함수는 { } 안에 매개변수와 함수 내용을 선언하는 함수로 다음 규칙에 따라 정의한다.- 람다 함수는 항상 { }으로 감싸서 표현해야 한다.- { } 안에 -> 표시가 있으며 -> 왼쪽은 매개변수, 오른쪽은 함수 내용이다.- 매개변수 타입을 선언해야 하며, 추론할 수 있을 때는 생략할 수 있다.- 함수의 반환값은 함수 내용의 마지막 표현식이다.






# lateinit
 늦은초기화
 말그대로 객체 초기화를 늦게하는 것이다.

![image](https://user-images.githubusercontent.com/117493614/200717605-e0e8daeb-00d7-4ed3-aefe-3fb070f632d5.png)


lateinit 을 사용하여 
text변수를 선언해줬고, 이후에 어떤 동작의 결과 값을 기반으로 text 를 초기화 해주는 것을 확인할 수 있다.

이후에 또 한 번 값을 바꾸는 것을 확인할 수 있는데, lateinit 변수 선언부를 자세히 보면 var 로 선언되어 있다. lateinit 을 사용하면 늦은 초기화 이후에도 값이 계속하여 바뀔 수 있다.

그럼, 만약 lateinit 을 사용해놓고 늦은 초기화조차 하지 않은 경우는 어떻게 될까?
Exception in thread "main" kotlin.UninitializedPropertyAccessException: lateinit property text has not been initialized

이런식으로 컴파일 단계에서 오류가 발생하기 때문에 잠재적 오류를 방지해주기도 한다.


# lazy
초기화 지연

![image](https://user-images.githubusercontent.com/117493614/200742148-83a4c2aa-eeb9-42c8-b48b-9ad61f333094.png)




변수를 실행하는 시점까지 초기화를 자동으로 늦춰주는 지연 대리자 속성(lazy delegate properties)을 알아보자. lazy는 lateinit과 달리 val 변수를 사용해야한다. val을 사용하기에 값을 변경할 수는 없고, 호출할때 어떤식으로 선언될지 정의할 수 있도록 돕는 초기화 지연 프로퍼티라 할 수 있다.

lazy는 람다함수 형태의 초기화 함수를 사용하는 형태로 val 변수를 선언한 뒤, by lazy를 붙이고 람다함수를 정의해주면 된다. 이렇게 코드를 작성하면 코드상으로는 선언시에 즉시 객체를 생성 및 할당하여 변수를 초기화하는 것처럼 보이지만, 실제 실행시에는 val 변수를 사용하는 시점에 초기화가 진행하여 코드의 실행시간을 최적화할 수 있도록 한다. 람다함수로 초기화가 진행되므로 함수안에 여러개의 구문이 들어갈 수 있으며 맨 마지막 구문의 결과가 변수에 할당된다

