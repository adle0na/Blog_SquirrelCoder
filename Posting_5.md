<!-- Heading -->
#  다섯번째 도토리

<!-- Quote -->
> ## 이론 정리
> 
> ### 11, 12, 13, 14, 15, 16, 17 강
<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

오늘은 오랫만에 이론 정리 입니다

코로나로 일주일 쉬니까 예제도 잘 안되고 셀프코딩까지 또 막막해서

무작정 강의 영상 하나 잡고 공부 시작합니다 이번엔 유튜브에서 눈코딩 이라는 분의

C#강의 영상을 볼려고 합니다

이미 초반 영상은 좀 봤는데 오늘부턴 정리도 해볼려구요

<br>

이 포스팅은 유튜브 눈코딩 님의 **[유니티C#](https://youtu.be/bqNW08Tac0Y)**
강의 영상을 참고 하였습니다

<br>
바로 들어갑니다

<hr>
<!-- Numbered list -->

##11편 Var키워드

var를 사용하면 변수를 선언할 때 형식을 직접 선언한 것처럼 컴파일러가 형식을 결정 해줍니다

원래는 변수타입과 변수명을 선언하여
```c#
int hp;
float damage;
string name;
bool isTest;
char word;
object obj;
```
이렇게 변수 선언시에 변수명 앞에 변수 타입을 명시 해줘야 하지만 var키워드를 사용하면

변수에 할당되는 값에 따라 컴파일러가 형식을 결정합니다

이번엔 var키워드로 변수들을 선언 해보겠습니다

```c#
var hp = 10;
var damage = 12.3f;
var name = "다람쥐코더";
var isTest = true;
var word = 'A';
var obj = new object();
```

이렇게 알아서 해주네요 그런데 var로 선언하게 되면 반드시 값을 할당해 주어야 합니다
```c#
// 잘못쓴경우
var armor;

// 올바르게 사용
var armor = 12;
```
그리고 직접 실행 해보시고 이번 영상은 끝이 납니다

<hr>
그럼 이제 생기는 호기심

아니 그럼 왜 다들 var로 자동으로 형식을 지정하지 않을까? 라는 궁금증으로

검색을 해본 결과 저와 똑같은 호기심을 가진분이 이미 질문을 올려 두셨더라구요

[유니티 도움말](https://answers.unity.com/questions/1087276/why-woud-i-use-var-in-c.html) 
여기로 접속을 해보시면

var 키워드는 유형이 지정된 변수를 선언하고 값을 즉시 할당할 때, 그리고 지역 변수에서만 작동합니다
그래서 클래스 변수가 아닌 메서드의 내부에만 존재합니다 그래서 이는 특별한 장점이 없으며

**"지역 변수를 선언하는 더 짧은 방법입니다"**

라고 답변을 주셨네요

그리고 코드로 긴 제네릭 유형에 사용하면 유용하다고 예시로 알려주십니다

```c#
 // 두코드는 같은 기능을 합니다
 var dict = new Dictionary<string, List<GameObject>>();
 
 Dictionary<string, List<GameObject>> dict = new Dictionary<string, List<GameObject>>();
```

그리고 마지막에 답변자와 질문자의 대화입니다
<!-- Image -->
![image description](https://i.imgur.com/PiPE6PA.png)

### 강의 한줄 후기

var 키워드.. 저도 이런게 있다는 것 정도로만 넘어갈 것 같습니다

<hr>
<!-- Numbered list -->

## 12편 상수

수식에서 변하지 않는 값이며 변하는 값인 변수와는 반대의 개념입니다

**상수는 변경할 수 없는 값입니다**

앞으로의 프로그램 수명 동안 변경하지 말라고 농담을 하시네요

언제든지 변경될 수 있는 정보를 나타낼 때는 상수를 만들면 안됩니다

상수의 정의는 const키워드로 선언 하고 변수앞에 const를 붙여 주면 됩니다
```c#
const int MaxHp = 10;

// 아래와 같이 선언만 할 수는 없습니다
cont int MaxHp;
```
선언과 값 할당을 동시에 해야 합니다

그리고 이후로 **선언 후 값을 할당하는 것을 초기화 라고 부르기로 합니다**

이후에 직접 실행 해보시고 이번 영상은 가볍게 끝이 납니다

<hr>

<!-- Numbered list -->

##13편 열거형식

변수 앞에는 변수 타입이 붙습니다 어떤 값을 변수에 넣을지 고민 후에 변수 타입을 지정합니다

그리고 값에는 종류가 있고 종류에따라 사용하는 키워드가 다릅니다

그리고 평소에 쓰던 미리 정의되어 있는 키워드 이외에도 사용자가 직접 타입을 만들 수도 있습니다

바로 전에 배운 상수들을 묶어서 열거형이라는 이름으로 사용자 정의 타입을 만들어 봅니다

**열거형은 상수들의 집합**입니다

열거형을 정의하려면 enum 키워드를 정의하고 열거형 멤버의 이름을 지정합니다

```c#
enum Animal
{
    // 내부값은 모두 상수입니다
    // 0으로 시작하고 정의된 텍스트 순서에 따라 1씩 증가합니다
    Dog,
    Cat,
    Squirrel,
    Snake
}
```
기본적으로 열거형 멤버의 연결된 상수 값은 int 형식입니다

연결된 상수 값을 명시적으로 지정할 수도 있습니다
```c#
enum Animal
{
    Dog = 10,
    Cat = 20,
    Squirrel = 50,
    Snake = 100
}
```
위와 같이 열거 형식을 정의한다는 것은 새로운 타입 정의를 의미 합니다

### 변수 정의와 완전 다른 내용입니다

열거형식 정의는 class내부 또는 namespace내부 에서 합니다

그리고 직접 실행 하고 영상은 끝이 납니다

```c#
// 열거형식 변수 정의
Animal animal;

// 열거형식 변수에 값 할당
animal = Animal.Squirrel;

// 출력값 Squirrel
Debug.Log(animal);

// 값도 변경해보기
animal = Animal.Snake;

// 출력값 Snake
Debug.Log(animal);

// 열거형 변수의 값은 할당된 열거형 멤버 이름으로 출력 됩니다
```
<hr>
<!-- Numbered list -->

##14편 형식 변환

변수가 선언된 후에는 다시 선언되거나 다른 형식의 값이 할당될 수 없습니다

(형식이 변수의 형식으로 암시적으로 변환될 수 있는 경우는 예외)

예를 들어 string은 int로 암시적 변환이 불가능합니다

형식을 변환하는데는 두가지 방법이 있습니다

```c#
int hp = 12;
float damage = 12.3f;

hp = (int)12.3f; // 명시적 변환

damage = 23; // 암시적 변환
```
사용법도 여러가지가 있습니다

**정수를 실수로 변환** ~~(mistake)~~
```c#
int hp = 12;
float temp = Convert.ToSingle(hp);
// 정수값이 실수값인 12.0f로 변환됨
```
**실수를 정수로 변환** 
```c#
float damage = 5.8f;
int temp = Convert.ToInt32(damage);
// 6으로 변환됨
// 두 정수 사이의 값이면 짝수 값을 반환합니다 4.5는 4로 5.5는 6으로 변환됩니다
```
**정수를 문자열로 변환**
```c#
int hp = 10;
string temp = hp.ToString();
// "10"으로 변환됨
```
**문자열을 정수로 변환**
```c#
string str = "123";
int num = Convert.ToInt32(str);
// 123으로 변환됨
```
**문자열을 실수로 변환** 
```c#
string str = "12.3";
float num = Convert.ToSingle(str);
// 12.3으로 변환됨
// 문자열에 포함되는 숫자 형식만 가능합니다
```
**정수를 문자로 변환**
```c#
int num = 65;
char word = Convert.ToChar(num);
// 'A'로 변환됨
```
그리고 직접 실행 후 영상은 끝납니다

전부 외울 수 없으니 적어두고 나중에 참고하기로 합니다

<hr>

##15편 문자열 보간

이번 영상엔 바로 예제 코드를 실행하셨다
```c#
// 문자열 변수 name 선언
string name; // 변수 정의

name = "다람쥐코더"; // 변수에 값 할당

Debug.Log($"{name}의 블로그");
// $와 쌍따옴표사이에 공백이 있어서는 안되며 중괄호의 짝을 확인해야 합니다

// 출력문 하나에 여러 변수 출력하기

int Dotori;
Dotori = 5;
Debug.Log($"{name}의 {Dotori}번째 포스팅");
// 다람쥐코더의 5번째 포스팅으로 출력완료


// 다른 방법
// 이방법은 Debug.Log로는 출력에 오류가 있는듯 합니다
string name = "다람쥐코더";
int dotori = 5;

// Debug.Log는 무시하고 뒤의 형식만 알아갑시다
Debug.Log("{0}번째 포스팅을 올린 {1}입니다.",  dotori, name);        
```
영상에서 배운걸로는 조금 모자라서 자료를 찾아봤다

LAYER6AI님의 [끝나지 않는 프로그래밍 일기](https://youtu.be/bqNW08Tac0Y) 블로그 자료에서

영상에 나온 두번째 방식이 복합 형식 지정이라는 방법이란걸 알게 되었고

이 방법보다는 첫번째 방법인 문자열 보간이 직관적이라고 한다

<!-- Image -->
![image description](https://i.imgur.com/Xx0LEXy.png)

요런 짤막한 팁도 있으니 챙겨가도록 하자

<hr>
<!-- Numbered list -->

## 16편 값형식과 참조형식 

변수는 저장된 값의 메모리 주소입니다 프로그램이 실행되면 크게 2개의 메모리 영역을 사용합니다

<br>

첫번째 메모리 영역의 이름은 **스택 메모리**입니다

**스택**은 가장 **나중에 넣은 데이터를** 가장 **먼저 꺼내는** 선형적 구조 입니다

<br>

두번째 메모리 영역의 이름은 **힙 메모리**입니다

힙은 **계층적** 구조입니다 **임의의 순서로 저장**됩니다

<br>

변수가 선언되면 스택 메모리에 공간이 할당됩니다

변수에 값을 할당 한다는 것은 메모리에 값을 저장한다는 뜻입니다

모든 값이 스택 메모리에 저장 되는 것은 아닙니다

어떤 값들은 힙 메모리에 저장됩니다

**스택에 값이 직접 저장**되는 형식을 **값형식** 이라고 부릅니다

힙에 값이 저장되는 형식을 참조형식 이라고 부릅니다

참조형식은 스택과 힙 메모리 모두를 사용합니다

**힙**에는 **값**을 **스택**에는 **값의 주소**를 저장합니다

값을 참조 한다고 해서 참조 형식이라고 부릅니다

**값형식**은 **스택에 값이 직접 저장**됩니다

참조형식은 다음과 같습니다 string, object

마찬가지로 **참조형식**의 **값은 힙메모리**에 **값의 주소는 스택**에 저장됩니다

null은 아무것도 참조하지 않는 **값**이며 **참조 형식 변수의 기본값**입니다

값은 변수에 할당이 가능하구요

string은 참조형식이므로 string변수에 null값 할당이 가능합니다

```c#
string name = null;
```

생각보다는 긴 내용의 텍스트가 3분23초 동안 나오는데 영상의 핵심은

 ### "값형식은 스택에 참조형식은 힙에 값이 저장된다" 입니다

<hr>

## 17편 박싱과 언박싱

Boxing은 값 형식을 object형식으로 변환하는 프로세스 입니다

Boxing은 값을 내부에 래핑하고 힙에 저장합니다

값형식은 값이 직접 스택에 저장됩니다

값형식의 값을 Boxing하면 래핑해서 힙에 저장합니다

Boxing은 암시적이며 UnBoxing은 명시적입니다

Boxing
```c#
int i = 123;
object obj = i;
```
Unboxing
```c#
int i = 123; // 값 형식
object obj = i; // 암시적 박싱
int j = (int)obj; // 명시적 언박싱
```

도대체 이해가 안가서 따로 자료를 찾아봤다 이번엔 여러 사이트를 돌아다녔고

ArrayList와 같이 여러타입의 자료를 저장하게 되면 값을 가져올 때 박싱이 되는데
이때 박싱되기 전 자료형으로 명확히 캐스팅도 해줘야해서 형식 불안정성도 증가되고
뭐 아무튼 피해야 한다고 한다

## 오늘 정리를 마치며

하루종일 이론만 정리하고 이해하려고 하니 막바지엔 집중력도 흐려지고 이해력도 떨어졌다
이론 정리는 하루 5개정도로만 하고 예제로 실력 키우는게 나을것 같다