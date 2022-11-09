# lateinit
지연초기화

늦은초기화 라 함은, 말그대로 객체 초기화를 늦게하는 것이다.


fun main() {
    lateinit var text: String

    // 대충 중간에 뭔가 했음
    val result1 = 30

    text = "Result : $result1"
    println(text)

    // 대충 뭔가 또 했음
    val result2 = 50

    text = "Result : ${result1 + result2}"
    println(text)
}
ateinit 을 사용하여 text 변수를 선언해줬고, 이후에 어떤 동작의 결과 값을 기반으로 text 를 초기화 해주는 것을 확인할 수 있다.

이후에 또 한 번 값을 바꾸는 것을 확인할 수 있는데, lateinit 변수 선언부를 자세히 보면 var 로 선언되어 있다. lateinit 을 사용하면 늦은 초기화 이후에도 값이 계속하여 바뀔 수 있다.

그럼, 만약 lateinit 을 사용해놓고 늦은 초기화조차 하지 않은 경우는 어떻게 될까?

아래와 같은 에러를 볼 수 있을 것이다.



