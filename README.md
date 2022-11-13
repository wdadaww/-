# Kotlin


# 고차함수 -> 람다식




![image](https://user-images.githubusercontent.com/117493614/200719897-bd21894e-1c8f-449d-9b7c-2d27e0f8f413.png)



람다식, 또는 람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수 (Anonymous Functions)를 지칭하는 용어이다.
람다 함수는 { } 안에 매개변수와 함수 내용을 선언하는 함수로 다음 규칙에 따라 정의한다.- 람다 함수는 항상 { }으로 감싸서 표현해야 한다.- { } 안에 -> 표시가 있으며 -> 왼쪽은 매개변수, 오른쪽은 함수 내용이다.- 매개변수 타입을 선언해야 하며, 추론할 수 있을 때는 생략할 수 있다.- 함수의 반환값은 함수 내용의 마지막 표현식이다.






# 프로퍼티 의 초기화

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



# 싱글톤 object

인스턴스가 하나만 있는 클래스 선언하는 키워드!

![image](https://user-images.githubusercontent.com/117493614/200966297-18c1d480-8a3e-4d38-86b1-37c9689c0aa8.png)



# Companion object

클래스 내의 객체클래스 (static이 아니다... 하지만 비슷한효과가나타난다.)


![image](https://user-images.githubusercontent.com/117493614/200966551-b83f187c-1be1-463d-b3b5-c26f62f8a203.png)


- 축약형이 가능

![image](https://user-images.githubusercontent.com/117493614/200967509-5924e4b5-52d8-4a50-9345-d90262054290.png)


# Sealed class

실드란 '봉인된'이라는 의미로 무언가 안전하게 보관하기 위해 묶어 두는 것을 뜻한다. 실드 클래스는 미리 만들어 놓은 자료형들을 묶어서 제공하기 때문에 어떤 의미에서는 열거형 클래스의 확장으로도 볼 수 있다.

 

실드 클래스는 sealed 키워드를 통해 선언할 수 있다. 실드 클래스 그 자체는 추상 클래스와 같기 때문에 객체를 만들 수 없다. (즉, 껍데기? 라고 생각하면 된다.) 또한 생성자도 기본적으로 private 이며 private이 아닌 생성자는 허용하지 않는다. 실드 클래스는 같은 파일 안에서는 상속이 가능하지만, 다른 파일에서는 상속이 불가능하게 제한된다. 블록 안에 선언되는 클래스는 상속이 필요한 경우 open 키워드로 선언될 수 있다. 실드 클래스를 사용해보자.
![image](https://user-images.githubusercontent.com/117493614/201450388-efcd33fa-0c8f-462d-b7a0-9d39f66e256e.png)


위  성공/실패를 Result 라는 실드 클래스로 감쌌다. 실드 클래스에서 특정 객체 자료형에 따라 when 문과 is 를 사용해 결과값에 따라 실행이 가능하다. 이렇게 모든 경우 Success / Error 가 열거 되있으므로 else 문이 필요 없다. 이는 실드 클래스를 사용했기 때문이다. (일반적으로 when 문을 사용할 때 컴파일러는 모든 경우의 수를 판단할 수 없기 때문에 else 문을 써야한다.)

![image](https://user-images.githubusercontent.com/117493614/201450575-d81d80e4-4f38-4f2a-a085-e48345ed4b25.png)


![image](https://user-images.githubusercontent.com/117493614/201450715-2ce72a34-ca5b-4d58-9dbf-234d8ab741ae.png)

![image](https://user-images.githubusercontent.com/117493614/201450795-c9838dab-291f-4032-b16f-5557fa8caef1.png)

# Enum class

열거형 클래스란 여러개의 상수를 선언하고 열거된 값을 조건에따라 선택할수 있는 클래스이다. 열거형 클래스는
실드 클래스와 비슷하다. 차이점은 열거형 클래스는 실드 클래스처럼 다양한 자료형을 다루지못한다.
열거형 클래스는 enum 키워드를 사용해서 선언한다.


![image](https://user-images.githubusercontent.com/117493614/201452065-5f7614a5-08c9-45c5-9f26-eb23f3d7ef70.png)

![image](https://user-images.githubusercontent.com/117493614/201452102-d18f145d-acf4-40e0-9eb8-6a7472b3ad13.png)


![image](https://user-images.githubusercontent.com/117493614/201452119-100647d8-7e93-49f6-a2cc-312d64a76eb8.png)


# 제네릭 (Gneric)

in, out 키워드를 알아보기 전에 먼저 제네릭에 대해 간단하게 짚고 넘어가도록 하자.
제네릭은 자주 보았던 <> 요런 모양을 가진 친구이다.
클래스, 인터페이스, 함수 등에서 동일한 코드를 재사용하고 싶을때 여러 타입을 지원하기 위한 유용한 기능이다.

![image](https://user-images.githubusercontent.com/117493614/201459034-03ad20e5-cf09-4f66-9017-0ffa695d03a5.png)

# 변성

제네릭에서 파라미터화된 타입이 서로 어떤 관계에 있는지 설명하는 개념.
공변성, 반공변성, 무공변성으로 나뉜다.
이펙티브 자바에서는 공변성과 반공변성에 대해서 이야기할 때, PECS라는 규칙을 언급한다.
PECS 는 Producer - Extends / Consumer - Super 의 약자입니다. 

# 공변성은 자바의 extends 키워드이고 코틀린에서는 out
# 반공변성은 자바의 super 키워드이고 코틀린에서는 in

 out: A<서브타입>을 A<슈퍼타입>에 대입할수있도록지원
 in: A<슈퍼타입>을 A<서브타입>에 대입할수있도록 지원
 * : A<*>은 타입인수가 무엇이든 상관없이 대입 할 수 있도록 지원
 
 ![image](https://user-images.githubusercontent.com/117493614/201503964-26bebe07-4873-43ff-988d-d82054f828ac.png)

 



