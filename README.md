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

*  공변성은 자바의 extends 키워드이고 코틀린에서는 out
*  반공변성은 자바의 super 키워드이고 코틀린에서는 in

 * out: A<서브타입>을 A<슈퍼타입>에 대입할수있도록지원
 
 * in: A<슈퍼타입>을 A<서브타입>에 대입할수있도록 지원
 * 스타프로젝션: A<*>은 타입인수가 무엇이든 상관없이 대입 할 수 있도록 지원
 
 ![image](https://user-images.githubusercontent.com/117493614/201503964-26bebe07-4873-43ff-988d-d82054f828ac.png)

 

# 액티비티 생명주기

![image](https://user-images.githubusercontent.com/117493614/202933766-ba2f04af-7370-40be-a071-919413246baf.png)


* 1.앱을 실행한다.

![image](https://user-images.githubusercontent.com/117493614/202933921-72791de4-a52b-4cad-8398-6f6c3ba7ebf6.png)

![image](https://user-images.githubusercontent.com/117493614/202933929-669c1788-5ab0-42af-8b1d-2a4aed48a00a.png)

OnCreate()-> onStart()-> onResume() 순으로 실행.

1.최초에 한번 OnCreate()실행

2.앱이 화면에 보이는 시점에 OnStart()실행

3.사용자가(버튼을 클릭하는 등) 상호 작용을 할수 있도록 준비된 시점에 onResume()실행



* 2.앱을 실행한후 닫은 경우


![image](https://user-images.githubusercontent.com/117493614/202933921-72791de4-a52b-4cad-8398-6f6c3ba7ebf6.png) 

![image](https://user-images.githubusercontent.com/117493614/202934116-b714aab0-fed8-4ac5-9604-97341f4f1be5.png)


![image](https://user-images.githubusercontent.com/117493614/202934095-2dcc78ef-ad25-4356-aacf-749562b2519c.png)

앱을 종료하니 위에서 로그를보면 OnResume 이후 onPause()-> onStop()-> onDestroy()순으로 실행

1. 사용자가 상호 작용을 할수 시점에서 OnPause()실행.

2. 앱이 화면이 보이지않게되면서 OnStop() 실행.

3. 앱이 종료되면서 onDestroy()실행.


* 3.앱을 닫은후 다시 켠경우.


![image](https://user-images.githubusercontent.com/117493614/202934487-d43ea2f8-d921-4f48-93bb-0c3c1a6b33a2.png)


![image](https://user-images.githubusercontent.com/117493614/202934492-210cca4f-d093-479b-9539-ec6389f5be8d.png)

![image](https://user-images.githubusercontent.com/117493614/202934530-f2bdf675-665d-4624-be2e-cea5da80a573.png)

앱을 처음 실행했을때 와 같은 과정이다.


* 4.기기의 홈 버튼을 눌러  앱을 백그라운드로 보낸경우.


![image](https://user-images.githubusercontent.com/117493614/202934629-3a2a9cd4-9ca9-4361-b917-3a978861446d.png)


![image](https://user-images.githubusercontent.com/117493614/202934637-d501080b-8bdb-49be-97d9-1e7b133811d8.png)


앱을 아예 껐을 때와 다르게 OnDestroy()가 실행되지 않고 OnPause() -> OnStop()이 실행된다.


![image](https://user-images.githubusercontent.com/117493614/202934837-c297a722-0c91-4ab5-98ea-b19a4e014a8a.png)

* 5.최근 실행 앱에서 앱을 다시 활성화한 경우

![image](https://user-images.githubusercontent.com/117493614/202934964-9a6bc3ea-e840-4d4e-ad44-8df06c30d46a.png)



OnRestart() -> OnStart() -> OnResume() 순으로 실행된다.



![image](https://user-images.githubusercontent.com/117493614/202934975-3b3a0639-3109-461a-ab7c-585296f7987d.png)




# 프래그먼트

Fragment는 FragmentActivity 내의 어떤 동작 또는 사용자 인터페이스의 일부를 나타냅니다. 여러 개의 프래그먼트를 하나의 액티비티에 결합하여 창이 여러 개인 UI를 빌드할 수 있으며, 하나의 프래그먼트를 여러 액티비티에서 재사용할 수 있습니다.

이는 자체적인 수명 주기를 가지고, 자체 입력 이벤트를 수신하고, 액티비티 실행 중에 추가 및 삭제가 가능합니다(다른 액티비티에 재사용할 수 있는 "하위 액티비티"와 같은 개념)

프래그먼트는 항상 액티비티 내에서 호스팅되어야 하며 해당 프래그먼트의 수명 주기는 호스트 액티비티의 수명 주기에 직접적으로 영향을 받습니다. 예를 들어 액티비티가 일시정지되는 경우, 그 안의 모든 프래그먼트도 일시정지되며 액티비티가 소멸되면 모든 프래그먼트도 마찬가지로 소멸됩니다. 그러나 액티비티가 실행 중인 동안(재개됨 수명 주기 상태에 있을 경우)에는 각 프래그먼트를 추가 또는 제거하는 등 개별적으로 조작할 수 있습니다. 그와 같은 프래그먼트 트랜잭션을 수행할 때는 이를 액티비티가 관리하는 백 스택에도 추가할 수 있습니다. 각 백 스택 항목이 발생한 프래그먼트 트랜잭션의 기록이 됩니다. 이 백 스택을 사용하면 사용자가 프래그먼트 트랜잭션을 거꾸로 돌릴 수 있습니다(뒤로 이동). 이때 Back 버튼을 누르면 됩니다.


# 프래그먼트 생명주기 

![fragment_lifecycle](https://user-images.githubusercontent.com/117493614/203220860-fbb38f83-a88a-4bcb-b3d4-0f1b7d2a5e49.png)



초기화단계: OnAttach,OnCreate 함수가 호출.
프래그먼트의 화면을 구성할 뷰가 준비되어있지않은상태.

생성단계: OnAttach -> OnCreate -> OnCreateView -> OnActivityCreated -> OnStart -> OnResume 함수가 호출됨.
프래그먼트의 처음 화면이나옴. 이후 다른 프래그먼트로 교체될 때는 백 스택을 사용하지는에 따라 생명주기가 다르게 동작합니다


재개단계: OnPause -> OnStop -> OnDestroyView -> 이후 다시 프래그먼트가 준비되어 화면에출력되면 -> OnCreateView -> OnActivityCreated -> OnStart -> OnResume

-백 스택을 사용하면 이전 프래그먼트로 화면을 전환할수있다
-그러나 백 스택을 사용하지않으면 프래그먼트가 교체될때 기존의 프래그먼트는 onDestroy까지 호출되어 제거됩니다.


소멸단계:  OnPause -> OnStop -> OnDestroyView -> OnDestroy -> OnDetach

onCreateView()로 전달된 조작가 container가 상위 ViewGroup이고(액티비티 레이아웃으로부터), 이 안에 프래그먼트 레이아웃이 삽입됩니다. savedInstanceState양자는 취소 Bundle로, 이것은 프래그먼트가 재개되는 느린 경우 프래그먼트의 이전 폐쇄에 대한 데이터를 제공합니다(상태를 복원하는 것은 프래그먼트 수명 주기 처리 에서 더욱 자세히 설명합니다).

inflate()방법은 다음과 같은 세 개의 인수를 취합니다.

팽창자를 하기 위한 레이아웃의 폐쇄형 ID.
팽창된 레이아웃의 상위가 될 ViewGroup. container를 전달해야 하는 (실행 가능한 상위 뷰에서 등록되기까지는) 시스템이 레이아웃을 가지고 끌어서 팽창된 레이아웃의 검토에 적용할 수 있는 행정 진행이 중요합니다.
팽창된 레이아웃이 팽창 ViewGroup(두개 활성화)에 연결되어야 하는 것을 나타내는 부울 값. (이 경우, 이 값은 false입니다. 시스템이 이미 팽창된 레이아웃을 container안에 삽입하기 쉽습니다. true를 전달하면 최종 레이아웃에 겹쳐진 뷰 그룹을 생성하게 됩니다.)
이제 레이아웃을 제공하는 프래그먼트를 생성하는 방법을 알게 되었습니다. 다음은 프래그먼트를 요청에 추가해야 합니다.


* 프래그먼트 관리

![image](https://user-images.githubusercontent.com/117493614/203225331-090c952c-3cf9-4a0e-a2ab-1b869f5418e2.png)


* 백스택: 프래그먼트가 화면에 보이지않는 순간 제거하지 않고 저장했다가 다시 이용할 수 있는 기능
하지만 commit()을 호출하기전에 백스택을 먼저 호출해야합니다.


# 뷰바인딩 사용법 (액티비티)
* 빌드.그래들 (모듈) 에 이것을 넣어 주세요


![image](https://user-images.githubusercontent.com/117493614/203270324-9ff74488-1721-4122-81f0-ecee44742e43.png)


# findViewById와의 차이점
* 뷰 결합에는 findViewById를 사용하는 것에 비해 다음과 같은 중요한 장점이 있습니다.

Null 안전: 뷰 결합은 뷰의 직접 참조를 생성하므로 유효하지 않은 뷰 ID로 인해 null 포인터 예외가 발생할 위험이 없습니다. 또한 레이아웃의 일부 구성에만 뷰가 있는 경우 결합 클래스에서 참조를 포함하는 필드가 @Nullable로 표시됩니다.
유형 안전: 각 바인딩 클래스에 있는 필드의 유형이 XML 파일에서 참조하는 뷰와 일치합니다. 즉, 클래스 변환 예외가 발생할 위험이 없습니다.
이러한 차이점은 레이아웃과 코드 사이의 비호환성으로 인해 런타임이 아닌 컴파일 시간에 빌드가 실패하게 된다는 것을 의미합니다.


# let 함수

