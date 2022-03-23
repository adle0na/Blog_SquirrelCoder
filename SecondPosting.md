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

굉장히 주관적으로 정리 하였고 강의처럼 VisualStudio와 Unity Engine에서 컴파일 하며 확인 한게 아니고

라이더 툴에서 메모 하듯이 적어 놓는거라 오타나 오류가 날 수 있습니다

이 도토리를 드시고 배탈이 나도 책임지지 않습니다
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
수식, 논리를 계산 하기 위해 사용 하며 전위 후위는 오류 생기기 좋아 보인다

<hr>

##6. 조건문

조건문은 크게 두가지 if 문과 switch 문을 사용 한다

if를 여러개 사용 하면 조건과 관계 없이 계속 연산을 해서 연산 낭비를 하게 된다

그래서 else if를 통해 여러 조건을 하나로 연결해 줄 수 있다

if 문
```c#
   int input = 10;
   int num = 10;
   
   void Start()
   {
        if(input == num)
        {
            print("input값과 num값이 같음");
        }
        else if(input > num)
        {
            print("input값이 num값 보다 큼");
        }
        else if(input < num)
        {
            print("input값이 num값 보다 작음");
        }
        else
        {
            print("조건에 맞지 않음");
        }       
   }
```
switch 문
```c#
   int input = 11;
   int num = 10;
   
   void Start()
   {
        switch(input)
        {
            case 10:
                print("input값이 10입니다");
                break;
            case 11:
                print("input값이 11입니다");    
                break;
            case 12:
                print("input값이 12입니다");
                break;
            default:
                print("그외의 숫자");
                break;
        }
   }
```
특이한 경우, 삼항 연산자
```c#
    int input = 14;
    int num = 10;
    void Start()
    {
         // 먼저 쓴 50은 true의 경우, 100은 false의 경우
         int temp = input == num ? 50 : 100;
    }
```

<hr>

##7. 반복문

반복문도 크게는 두가지 for 문과 while 문을 사용 한다.

for 문
```c#
   int num = 0;
   
   void Start()
   {
        for(int i = 0; i <= 10; i += 2)
        {
            num = i;
            print(num);
        }
   }
```
continue와 break 사용 해보기
```c#
   int num = 0;
   
   void Start()
   {
        for(; ;)
        {
            num++;
            if(num % 2 == 0)
                continue; // 해당 회차를 끝냄, 조건에 맞으면 처음부터 실행
            
            print(num);
            
            if(num >= 10)
                break; // 현재 반복문 탈출, 조건문 탈출
        }
   }
```
while 문
```c#
   int num = 0;
   
   void Start()
   {
        while(num < 10)
        {
            num++;
            print(num);
        }
   }
```
for문은 반복횟수가 명확할 때, while문은 그렇지 않을 때

사용 한다고 하시는데 직접 코딩 해봐야 감이 올것 같다

<br>

추가로 배우는 while 문의 파생 do while 문!

조건에 맞지 않아도 무적권 1회는 실행 한다고 한다
```c#
   int num = 0;
   
   void Start()
   {
        do
        {
            num++;
            print(num);
        }
        while(num < 10);
   }     
```
크게 두가지 있다고 해놓고 이번엔 foreach 문이다
```c#
   string text = "가나다라마바사";
   
   void Start()
   {
        foreach(char a in text)
        {
            print(a);
        }
   }
```
출력하면 가 나 다 라 이렇게 쪼개져서 출력 된다
<hr>

##8. 배열
배열은 변수의 집합체로 내부의 인덱스 값을 바꿀 수는 있지만 배열의 크기를 임의로 변경 할 수는 없다
```c#
   int[] exp = { 50, 100, 150, 200, 250, 300 };
   
   void Start()
   {    
        // 배열의 인덱스 값을 변경 해보기
        exp[5] = 500;
        print(exp[5]);
        // 배열을 새로 추가할 수는 없다
        exp[6] = 1000;
        // 배열은 0 부터 시작하기 때문에 배열의 크기인 Length를 사용할땐 포함 시켜주면 안된다
        for(int i = 0; i < exp.Length; i++)
        {
            print(exp[i]);
        }
```
여러 차원의 배열을 사용 할 때
```c#
   // 1차원 배열
   int[] exp = { 50, 100, 150, 200, 250, 300 };
   int[] array = new int[10];
   // 2차원 배열
   int[,] array2 = { {1,2,3,4,5}, {10,20,30,40,50} };
   // 3차원 배열 ( 무슨일이 생겨도 여기까진 써볼일이 없을것 같다 )
   int[,,] array3 = {{{1,2,3,4,5},{10,20,30,40,50}}.{{1,2,3,4,5},{10,20,30,40,50}}};
   
   void Start()
   {
        print(array3[1, 1, 2]); // 두번째 배열의 두번째 배열의 3번째 값인 30
        print(array3[0, 0, 3]); // 첫번째 배열의 첫번째 배열의 4번째 값인 4
   }
```

<hr>

##9. 컬렉션
배열은 한번 선언 하면 크기를 변경할 수 없는 단점이 있지만 이를 극복한 것이 컬렉션이며

종류도 리스트, 큐, 스택, 해시테이블, 딕셔너리, 어레이리스트 등 여러가지가 있다.

우선 ArrayList 사용을 해보자
```c#
   ArrayList arrayList = new ArrayList();
   
   void Start()
   {
        arrayList.Add(1);
        arrayList.Add(2);
        arrayList.Add(3);
        arrayList.Add("가나다라");
        arrayList.Add(5);
        
        arrayList[3] = 4; // 4번째 배열 값을 4로 치환 
        arrayList.Clear(); // 모든 인덱스 값 초기화
        
        arrayList.CopyTo // 인덱스 값을 다른 인덱스 값에 복사 (정확한 사용법은 따로..)
        
        arrayList.Contains("가나다라"); // 특정 인덱스 값이 있는지 확인 해준다
        for(int i = 0; i < arrayList.Count; i++)
        {
            print(arrayList[i]);
        }
   }
```
그리고 다른 컬렉션들

리스트 List
```c#
   List<int> list = new List<int>();
```
해시테이블 HashTable
```c#
   Hashtable hashTable = new Hashtable();
   
   void Start()
   {
        hashTable.Add("만", 10000);
        hashTable.Add("백반", 1000000);
        hashTable.Add(50, "오십"); // ()의 첫번째 값은 두번째 값을 불러오기 위한 키 값이다
        // 다른 컬렉션과 기능은 비슷하다
        hashTable.remove
        hashTable.Contain
        hashTable.Clear();
        
        // 이 출력은 Null값으로 출력된다
        print(hashTable[0]); // 해시 테이블은 인덱스값이 아닌 키값을 받기 때문
        print(hashTable["만"]); // 이렇게 받아와야 10000이 출력된다
        print(hashTable["50"]); // 마찬가지로 키인 50을 서치하여 "오십"을 출력한다
   }
```
딕셔너리 Dictionary
```c#
   Dictionary<string, int>dictionary = new Dictionary<string, int>();
   
   void Start()
   {
        // 처음에 자료형을 선언하기 때문에 반드시 맞춰서 사용해야 한다
        dictionary.Add("가", 100);
   }
```
큐 Queue, 선입 선출, FIFO (은행 대기줄)
```c#
    Queue<int> queue = new Queue<int>();
    
    void Start()
    {
        queue.Enqueue(5);
        queue.Enqueue(10);
        
        if(queue.Count != 0) // 먼저 선언된 5출력
        print(queue.Dequeue());
        if(queue.Count != 0) // 그다음 선언된 10출력
        print(queue.Dequeue());
        if(queue.Count != 0) // 아무값도 출력 되지 않음
        print(queue.Dequeue());
    }
```
스택 Stack, 후입 선출, LIFO 

1 2 3 순서로 넣으면 먼저 넣은 1이 맨밑에 쌓이고 이렇게 쌓는 과정을 Push라고 하며

나중에 값을 꺼낼 때엔 가장 나중에 쌓아서 맨위에 있는 3이 꺼내지는데 이 과정은 Pop이라고 한다.
```c#
   Stack<int> stack = new Stack<int>();
   
   void Start()
   {
        stack.Push(1); // 반드시 명시한 자료형을 사용
        stack.Push(2);
        stack.Push(3);
        
        // 쌓인 순서의 역순으로 출력
        print(stack.Pop()); // 3
        print(stack.Pop()); // 2
        print(stack.Pop()); // 1
        // 그 이후 하나라도 있는지 파악
        if(stack.Count != 0)
            print(stack.Pop());
   }
```
자료 구조의 기초가 될 예정인 중요한 내용, 기억 안날 때마다 복습 하자

<hr>

##10. 네임스페이스
맨위에 누군가 만들어 놨던 클래스를 사용할때 코드 맨위에 using을 통해 선언

네임스페이스를 사용하는 이유는 협업, 대형 프로젝트, 외부 라이브러리 때

각각 네임스페이스가 중복되는 이름을 가져도 내부참조를 통해 사용 가능한 장점이 있기 때문
```c#
using UnityEngine;
//using Adle0na; // 하위 네임스페이스 선언시 필요없어짐
    
// 하위 네임스페이스는 .을 찍어 선언
using Adle0na.Blog;

    namespace Adle0na
    {
        // 하위에 네임스페이스 재 선언 가능
        namespace Blog
        {
            // 내부에 클래스 생성
            public class Squirrel
            {
                // 내부에 변수 생성
                int dotori;
                // 동작시킬 메소드 생성
                public void HideDotori(int count)
                {
                    dotori = count;
                }
                
                public bool hasDotori()
                {
                    return dotori != 0;
                }
            }
        }
    }
    // 기존 디폴트 클래스
public class This : MonoBehavior {
        
        void Start()
        {
            Squirrel me = new Squirrel();
            
            void Start()
            {
                me.HideDotori(2); // 위에서 만든 HideDotori의 파라미터에 2값을 넣음
                
                print(me.hasDotori());
                // dotori가 0이 아닌지 검사하는 hasDotori는 2를 받았기 때문에 출력값은 True
            }
        }
}
```
강의에서는 네임스페이스 하위 클래스가 중복 사용 되었을 때 참조 오류도 다루지만

나는 블로그 글 싸개라 기본 사용법만 익히고 넘어 갔다 나중에 문제 생기면 해보겠다
<hr>

##11. 구조체
우선 구조체는 더 심화내용이 많으며 이 강의에서는 Unity 게임 제작 목적으로 다룰 때만

간단히 알려준다고 댓글에 적어 두셨다 모르겠고 바로 사용 해보자
```c#
public struct Blog
   {
        public int s;
        
        public void GetS(int value)
        {
            s = value;
        }
   }
}
   // 디폴트 클래스
public class This : MonoBehavior {
   
        Blog squirrel;
        
        void Start()
        {
            squirrel.S = 5;
            
            squirrel.GetS(5);
        }
}        
```
쓰고 나니 뭔가 똑같은 느낌? 과거에 struct를 써왔고 지금은 class가 추가 되었는데

예전에 struct를 썼던 자료와의 호환성 때문에 그대로 쓰고 있다고 한다

그리고 예전 버전인 struct에는 상속이 불가능하다고 한다

그럼에도 struct를 사용하는 이유는 클래스는 new를 통해 사용 선언을 해야하지만

struct는 선언과 동시에 new를 자동으로 실행하여 사용 선언을 해준다

그 외에도 여긴 다루지 않지만 간단히 핵심, 심화 내용, 생성자도 알려주신다

~~(영상으로는 잘알려주시는데 내가 적고보니 뭐라는지 모르겠다)~~

<br>

추가로 배우는 enum타입

엉뚱한 자료가 들어가지 않게 들어 갈 값을 지정
```c#
    public enum Item
    {
        Weapon,
        Shield,
        Potion,
    }
    // 디폴트 클래스
 public class This : MonoBehaviour {
            Item item;
            
            void Start()
            {
                item = Item.Weapon;
                item = Item.Shield;
                
                print(item); // 마지막에 넣은 Shield값 출력
            }
 }        
```
나중에 인벤토리 만들때 꼭 쓸거 같으니 잘 기억해 둡시다
<hr>

##12. 델리게이트
이번 강의는 함수들을 통합 실행 시켜주는 델리게이트와

다른 클래스의 함수까지 통합 실행 시켜주는 이벤트를 배운다
```c#
   // 델리게이트 함수 ChainFunction선언
   public delegate void ChainFunction(int value);
   public static event ChainFunction OnStart;
   
   int power;
   int defence;
   
   public void SetPower(int value)
   {
        power += value;
        print("power의 값이" + value + "만큼 증가함, 총 power : " + power);
   }
   
   public void SetDefence(int value)
   {
        defence += value;
        print("defence의 값이" + value + "만큼 증가함, 총 defence : " + defence);
   }
   
   void Start()
   {
        // 델리게이트로 묶을 함수를 연산자와 함께 지정
        OnStart += SetPower;
        OnStart += SetDefence;        
   }
   
   private void OnDisable()
   {
        OnStart(5);
   }

```
연동 테스트를 위한 다른 스크립트
```c#
   // 디폴트 클래스
   public class This2 : MonoBehavior {
   
   void Start()
   {
        // 위에서 만지던 스크립트의 OnStart를 호출하여 Abc의 값 조정
        This.OnStart += Abc;
   }
   public void Abc(int value)
   {
        print(value + "값이 증가");
   }
 }
 
```
함수를 묶어서 사용하는 아주 맛있는 기능 꼭 익혀 두고 유용하게 쓰자

<hr>

##13. 상속
말그대로 부모 클래스의 변수나 메소드를 자식 클래스에게 물려주는 상속을 배워보자

일단 Human이름의 스크립트 생성
```c#
// 추상함수를 사용 할 때는 반드시 클래스도 추상 클래스로 선언 해주어야 함 
abstract public class Human : MonoBehaviour {
    
    // 상속 받은 자식 클래스만 사용 가능한 접근자 protected
    protected string humanName;
    protected int humanAge;
    
    // 자식 클래스에서 맘대로 값을 변경 할 수 있는 가상함수 설정 virtual
    protected virtual void Info()
    {
        print("나는 닝겐입니다");
    }
    
    // abstract는 추상함수로 자식 클래스에서 기능을 완성시키게끔 지정 해준다
    // ( 사용을 까먹지 않게끔 하는 좋은 기능이고 이를 다형성이라고 한다 )
    abstract protected void Name();
}
```
그리고 Student라는 스크립트도 생성
```c#
 public class Student : Human {
 
    string schoolName;
    
    void Start()
    {
        schoolName = "다람쥐 학교";
        humanName = "Adle0na";
        humanAge = 28;
        
        Info();
    }
    
    // virtual로 지정된 가상 함수를 Override를 사용하여 재정의
    protected override void Info()
    {
        // base가 지정된건 부모 클래스
        base.Info();
        print("나는 학생입니다");
        
        // 출력은 부모 클래스의 나는 닝겐입니다 와 나는 학생입니다가 둘다 출력된다
    }
    
    // 부모 클래스에서 추상 함수로 지정한 Name 메소드 완성
    protected override void Name()
    {
        print(humanName);
    }
 }
```
이번에 배운 상속 개념도 관리 하기 편하게 해준다 메소드를 미리 지정 해서 까먹으면 오류 나게끔

미리 설정도 할 수 있어서 이번에도 협업 할 때 유용 할듯 하다
<hr>

##14. 프로퍼티 (속성)
변수(데이터)의 은닉성 보장과 편리성을 위한 프로퍼티(속성) 를! 배워 보자

먼저 Salary 스크립트 생성
```c#
public class Salary : MonoBehaviour {

    private int salary;
    
    private void SetSalary(int value)
    {
        salary = value;
    }
    // 이렇게 해주면 타 클래스에서 수정은 못해도 읽기는 가능하다 (은닉성)
    public int GetSalary()
    {
        return salary;
    }
}
```
그리고 다른 클래스로 Program 생성
```c#
public class Program : MonoBehaviour {
    Salary mySalary = new Salary();
    
    void Start()
    {
        print(mySalary.GetSalary());
        
        // 이렇게 수정하려고 하면 보호 수준 때문에 접근 할 수 없다고 오류가 발생한다
        // mySalary.SetSalary(55);
        
    }
}
```
이렇게 은닉성 테스트를 끝냈는데 위와 같이 하면 함수를 한개 동작 하는데 두개를 써야 한다

이런 비효율적인 작업은 ~~(유사)~~개발자로써 참을 수 없기에 다음 기능을 배우기 위해 다시 Salary 스크립트로 돌아가자
```c#
public class Salary : MonoBehaviour {

    private int salary;
    
    // value는 위에서 선언한 적이 없다 미리 예약어 처럼 만들어 진 변수이다 반드시 value로 사용해야 한다
    // 그리고 set단계에 private를 걸어서 다른 클래스에서는 수정을 못하게 해주었다
    public int SalaryP { get { return salary; } private set { salary = value; } }

    void Start()
    {
        // 위의 SalaryP값 안의 salary value에 10이 들어가게 되고 순차적으로 private salary에도 10이 들어간다
        SalaryP = 10;
        
        print(SalaryP);
    }
}
```
이로써 은닉성 보장을 마쳤으니 프로퍼티의 편리성도 챙겨 보자

다시 Salary 스크립트
```c#
public class Salary : MonoBehaviour {
    
    private int salary;
    
    private int bonus = 10;
     
    // get의 값에 보너스를 더해 주고 set에 입력 오류 방지를 위해 조건문과 값 보정 기능을 넣어 주었다
    public int SalaryP { get { return salary + bonus; } set { if(value < 0) salary = 10; else salary = value; } }

    void Start()
    {
        // 이 경우 value가 0보다 작은 조건문에 걸려서 강제 지정한 값 10으로 준다
        salary = -5;
        
        // 정상 적인 경우 else로 넘어가서 salary 변수에 입력 된다
        salary = 5;
        
        print(SalaryP);
    }
}
```
근데 이렇게 해도 프로퍼티를 쓰기 위해선 변수도 필요 했기 때문에 두줄을 사용 했다

더 단순한 프로퍼티 사용법을 알아 보자 굳이 이렇게 까지 해야하나 싶지만

내가 선택한 개발자의 길이니 악으로 깡으로 버티자

또 다시 Salary 스크립트
```c#
public class Salary : MonoBehaviour {
    
    private int salary;
    
    public int SalaryP { get { return salary; } set { if(value < 0) salary = 10; else salary = value; } }
    
    // 이렇게 간단한 프로퍼티를 만드는 법도 있다
    public int Bonus { get; set; }
    
    void Start()
    {
        // 그이후 이렇게 써주면 된다
        Bonus = 10;
        print(Bonus);
    }
}
```
이렇게 프로퍼티의 편리성도 챙겨 보았다 영상 끝에 간단한 팁도 적어 주셨는데

배열도 프로퍼티를 사용한 예라고 한다
<!-- Image -->
![image description](https://i.imgur.com/8OaRnKG.png)

요렇게 옆을 보면 { get; } 이 생략 되어 있는것을 볼 수 있다

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

