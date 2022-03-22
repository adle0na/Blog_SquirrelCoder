<!-- Heading -->
#  두번째 도토리

<!-- Quote -->
> ## C# 이론 재정리
<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

오늘은 미뤄두었던 이론 자료를 총 정리해서 언제든지 꺼내 먹을 수 있도록 두번째 도토리를 심어 보겠습니다

<br>

<!-- Link -->
이 포스팅은 유튜브 **[케이디](https://www.youtube.com/channel/UC9w-j0OqNzdtOqiYj4lDHmg)**
님의 강의 영상을 참고 하였습니다

<br>

굉장히 주관적으로 정리하므로 이 도토리를 드시고 배탈이나도 책임지지 않습니다.
<!-- Heading -->

<hr>

<!-- Numbered list -->
##1. 변수

변수는 값을 가리키는 주소
```c#
// 우항의 값을 좌항 변수에 삽입
int x = 100;

void Start()
{
    x = -500;

    x = x - 500;
}
```
첫 영상 이라서 엔진 기초에 관한 내용이 많으니 빠르게 넘어 가도록 하자
<hr>

##2. 자료형

1. 정수 자료형

   + **sbyte** (-128 ~ +128) 1바이트
   + **short** (-3만 ~ +3만) 2바이트
   + **int** (-20억 ~ +20억) 4바이트
   + **long** 8바이트

음수를 사용 하지 않는 경우 앞에 u를 붙여서 양수 범위를 늘릴 수 있다.

2. 실수 자료형
   + **float** f = 4.000001f;
   + **double** d = 4.000001; // double은 d를 생략 가능
   + **decimal** m = 4.0000001m;

     decimal < double < float 순으로 오차 차이를 가진다.


3. 문자 자료형
    + **string** s = "가나다 abc @# 123"; // 한글 알파벳 숫자 특수 문자를 문자열로
    + **char** c = 'A'; // 유니코드를 기억 시키기 때문에 한 글자만 가능
    

4. 두가지 이상의 자료형을 사용 할 경우

```c#
    int a = 100;
    float b = 100.15f;
    
    int sum;
    
    void Start()
    {
        sum = (int)(a + b); // int형으로 강제 형변환
    }
```
변수를 괄호로 묶어 변경할 형식으로 지정 하는 방법
```c#
    int a = 100;
    string b;
    
    void Start()
    {
        b = a.ToString(); // int형을 문자형으로 강제 형변환
        print(b);
    }
```
ToString을 사용 하여 문자열로 강제 형 변환 하는 방법 
```c#
    int a;
    string b = "100";
    
    void Start()
    {
        a = int.Parse(b); // 문자열 "100"을 int형으로 강제 형변환
        print(a);
    }
```
Parse를 사용한 강제 형 변환은 포멧 에러가 잦아서 사용에 주의 해야 한다


<hr>

##3. 함수
```c#
    int intValue;
    
    float floatValue = 10.5f;
    float floatValue2 = 20.5f;
    
    // 2개의 float형 파라미터와 디폴트값을 가진 문자열 파타미터를 가진 FloatToInt 함수 선언
        // 추가로 디폴트 값을 지정하기 위해선 가장 뒤에 선언해야함
    void FloatToInt(float _parameter, float _parameter2, string _stringParm = "디폴트값")
    {
        // 두 파라미터 값을 합친 후 int형으로 형 변환
        intValue = (int)(_parameter + _parameter2); 
    }
    
    void Start()
    {
        FloatToInt(floatValue, floatValue2, "수정하고 싶은 내용"); // 함수 호출
    }
```

```c#
    int intValue;
    
    float floatValue = 10.5f;
    float floatValue2 = 20.5f;
    
    // 2개의 float형 파라미터와 디폴트값을 가진 문자열 파타미터를 가진 FloatToInt 함수 선언
        // 추가로 디폴트 값을 지정하기 위해선 가장 뒤에 선언해야함
    int FloatToInt(float _parameter, float _parameter2)
    {
        // 두 파라미터 값을 합친 후 int형으로 형 변환
        intValue = (int)(_parameter + _parameter2);
        print(intValue); // 출력 값 : 10.5 + 20.5를 더하고 int로 형 변환한 31 출력 
        
        return 4; // 이 함수의 반환값을 4로 지정
    }
    
    void Start()
    {
        FloatToInt(floatValue, floatValue2); // 반환값이 4인 함수 호출
        print(intValue); 반환값4 출력
    }
```
반복 작업을 할때 효율적으로 사용 가능한 필수 기능

<hr>

##4. 범위&접근 지정자

지역 변수와 전역 변수
```c#
    int a = 5; // 멤버 변수, 전역 변수
    
    void Abc()
    {
        // 지역 변수는 평상시엔 없음, 현재 함수가 실행되면 같이 실행되고 소멸할시 같이 소멸
        int a = 5; // 지역 변수
        a = 6;
        int b = 5; // 지역 변수 
        print(b);
    }
    
    void Abc2()
    {
        int b = 5; // 지역 변수
        print(b);
    }

public class Test2
{
    private int a;
    public int b;
    public static int c; // 공공의 공유 자원. 정적 변수
    
    public void Abc()
    {
    
    }
    private void Abc2()
    {
    
    }
}   

public class Test : MonoBehaviour
{
    Test2 a1 = new Test2();
    Test2 a2 = new Test2();
    Test2 a3 = new Test2();
    
    void Start()
    {
        Abc();
    }
    
    void Abc()
    {
        // 각각 다른 b의 값을 참조
        a2.b = 5;
        a1.b = 1;
        a3.b = 10;
        
        // 공유자원 수정은 클래스 자체에 접근해야함
        Test2.c = 100;
        
        print(a1.b); // 1출력
        print(a2.b); // 5출력
        print(a3.b); // 10출력
        print(Test2.c); // 클래스에 직접 접근
    }
}
```
지역, 전역 변수의 개념과 공유 자원, 정적 변수등 중요한 내용들 

<hr>

##5. 연산자

기본 연산자 +, -, *, /, %, = (대입 연산자)
```c#
    int a = 10;
    int b = 3;
    int c = 0;
    int d = false;
    
    void Start()
    {
        a = a + b; // 우항 a + b를 좌항 a 에 대입
        a += b; // 복합 대입 연산자 (자기 자신에게 연산을 할경우 대입 연산자 앞에 연산자 삽입 )
        d = (a == b); // 관계연산자 a와 b가 같은지 확인
    }
    // c = c + 1
    // c += 1
    // c++ // ++C 다 같은 기능을 하지만 C++, ++C는 1증가만 가능하다
    // ++, -- 앞뒤 위치에 따라 전위(선연산, 코드실행) 후위(선코드실행, 후연산)
    // 논리 연산자 &&(AND) ||(OR) !(NOT)
    // 비트 연산자 &(AND) |(OR) ^(XOR) ~(NOT)
```

<hr>

##6. 조건문

<hr>

##7. 반복문

<hr>

##8. 배열

<hr>

##9. 컬렉션

<hr>

##10. 네임스페이스

<hr>

##11. 구조체

<hr>

##12. 델리게이트

<hr>

##13. 상속

<hr>

##14. 프로퍼티 (속성)

<hr>

##15. 인덱서

<hr>

##16. 인터페이스

<hr>

##17. 형식 매개 변수T

<hr>

##18. 람다식

<hr>

##19. Action과 Func

<hr>

##20. 예외 처리

<hr>

##21. 코루틴


<hr>

<br>

<br>


<br>


<!-- Heading 
# 후기
이번 포스팅은 여기까지 입니다.

결국 저의 첫 포스팅은 뒤로가기 한번으로 블로그 포스팅 1시간 반을 날려먹은 매콤한 경험을 했지만

MarkDown이라는 Fun하고 Cool하고 Sexy한 언어를 새로 배우게 되었네요


역시 실수는 새로운 기회입니다 :wink:


<br>

## 추가 자료

위 기능들 말고도 더 많은 기능들이 있겠지만 게으른 저는 여기까지 하겠습니다.

필요하신 분들은 여기로 가보세요~

[heropy님의 블로그](https://heropy.blog/2017/09/30/markdown/)  MarkDown 사용법 총정리

-->

