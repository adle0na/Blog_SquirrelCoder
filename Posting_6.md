<!-- Heading -->
#  여섯번째 도토리

<!-- Quote -->
> ## 이론 정리
> 
> ### 18, 19, 20, 21, 22, 23, 24, 25, 26-1,2 강
<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

계속해서 이론 정리 입니다

셀프코딩의 단계를 위하여!

유튜브에서 눈코딩 이라는 분의 C#강의 계속해서 봅니다

<br>

이 포스팅은 유튜브 눈코딩 님의 **[유니티C#](https://imgur.com/d96nlwG)**
강의 영상을 참고 하였습니다

<br>
바로 들어갑니다

<hr>
<!-- Numbered list -->

##18편 입력받기

**버퍼 (Buffer)**

데이터를 한곳에서 다른 한 곳으로 전송하는 동안 일시적으로

그 데이터를 보관하는 메모리의 영역

**스트림 (Stream)**

데이터가 순서대로 전송되도록 보장하는 데이터의 흐름

영상보고 나니 저의 Unity 프로그래밍과는 관련이 없는 내용이었네요

입력받는 개념만 챙겨가도록 하겠습니다

![image description](https://i.imgur.com/d96nlwG.png)

입력해주세요 문구를 띄운뒤

string형식으로 input변수를 선언하고 값을 입력받아 삽입합니다 Console.ReadLine(); (엔진에서는 다른걸로)

Console.WriteLine(input); 으로 입력받은 값을 출력합니다

그뒤에는 입력 시스템에 대해 설명해주십니다 이번강의는 빠르게 넘어가도록합니다

<hr>

## 19편 산술 연산자

일반적인 수학 연산과 비슷한 연산자의 집합이다

단항으로는 ++증가, --감소, +더하기, -빼기

이항으로는 +더하기, -빼기 *곱하기, /나누기, %나머지로

모든 정수 및 소수점 숫자 형식을 지원합니다

먼저 증가 연산자입니다

전위 ++x와 후위 x++가 있으며

후위 증가 연산자는

피 연산자 값을 다른 연산에 먼저 사용하고 값을 1 증가시킵니다

반대로 전위 증가 연산자는

피 연산자 값을 1증가 시키고 다른 연산에 사용합니다

그대로 --x는 전위 감소 연산자, x--는 후위 감소 연산자입니다

나머지 +, -, *, / 더하기 빼기 곱하기 나누기는 전부 우리가 아는대로 사용하지만

%는 나눈 값의 나머지를 출력합니다

추가로 나오는 복합연산자의 개념입니다

앞에 수식으로 알려주시는데 이것보다는

아래 코드를 보는게 이해가 빠릅니다
```c#
int a = 5;
a += 9;
//출력값은 14입니다

int a = 5;
a = a + 9;
// 마찬가지로 출력값은 14로 동일합니다
```

마지막으로 일반 수학처럼 괄호()안의 연산 먼저 처리합니다

<hr>

##20편 비교 연산자

관계형 연산자라고도 하며 피연산자를 비교합니다
```c#
>, <, <=, >=
```
모든 정수 및 부동 소수점 숫자 형식을 지원합니다

char 형식은 비교 연산자도 지원합니다 char 피연산자의 경우 해당 문자 코드가 비교됩니다

열거형 형식은 비교 연산자도 지원합니다. 동일한 열거형 형식의 피연산자의 경우

기본 정수 형식의 해당 값이 비교됩니다

```c#
== !=
```
연산자는 피연산자가 같은지 여부를 확인합니다

비교 연산자의 연산은 일반 부등호 사용과 결과가 같으며 해당 결과가

옳은 경우 true 틀릴경우 false가 출력됩니다

<hr>

##21편 논리 연산자

논리 연산 또는 부울 연산은 연산된 결과 값이 참, 거짓만 존재하는 연산입니다

```c#
&& // 조건부 논리 AND
|| // 조건부 논리 OR
! // 논리 부정 NOT
```
&& (AND)

A와 B의 값이 모두 참일 경우 결과값 true 그렇지 않으면 false

|| (OR)
A와 B의 값이 둘중 하나라도 true면 true 그렇지 않으면 false

! (NOT)
A값이 true면 false 반대로 false면 true 출력

##22편 선택문 if문

if문의 "문" 프로그램이 수행하는 작업은 문으로 표현됩니다 코드 한줄 혹은 블럭일 수 있습니다

"식" 은 연산자와 피연산자로 구성됩니다

그리고 "선택문" 은 하나 이상의 지정된 조건에 따라 코드의 다른 섹션으로 분기할 수 있습니다.

if문

```c#
if(//부울 식)
{
    // 앞의 부울 식의 값이 참이면 실행할 코드 블록입니다
}
```

else if문

if의 조건이 false로 평가될 때만 실행됩니다

따라서 if, else if 둘중 하나는 실행 할 수 있지만 둘 다 실행할 수는 없습니다.

else 문

else if문은 여러번 사용 할 수 있지만 else문은 if문 내에서 한 번만 사용할 수 있습니다

조건을 포함할 수 없으며 이전의 모든 조건이 false로 평가될 때 실행됩니다

<hr>
<!-- Numbered list -->

## 23편 선택문 switch문

지정된 일치 표현식을 기반으로 조건 중 하나의 코드를 실행합니다

일치 식은 char, 문자열, 부울, 정수 및 숫자형식 또는 열거형 형식 중 하나여야 합니다

case 레이블에는 상수 식만 사용할 수 있습니다

```c#
switch(expression)
{
    case expression_value1:
        break;
    case expression_value2:
        break;
    default:
        break;
} 
```
일치 표현식 값과 일치하는 값에 대해 case 코드 블록이 실행됩니다

표현식 값이 case 값과 일치하지 않으면 기본 옵션 코드가 실행됩니다

옵션이 여러 개 있을 때 if else문 처럼 사용할 수 있습니다

switch를 사용하면 코드가 깨끗하고 읽기 쉬워 질 수 있습니다

아래와 같이 정수형 값을 표현식으로 사용할수도 있습니다

```c#
int day = 4;
switch (4)
{
    case 9:
        Debug.Log("화요일")
        break;
    case 10:
        Debug.Log("수요일")
        break;
    default:
        Debug.Log("주말이 빨리 왔으면..")
        break;
}
```
default 는 else문 처럼 일치하는 결과가 없을때 출력됩니다

<hr>

## 24편 반복문 for문

반복문은 명령문 또는 명령문 블록을 반복적으로 실행합니다

for문

지정된 부울 식이 true로 계산되는 동안 문 또는 문 블록을 실행합니다

```c#
for ( int i = 0; (초기화) i < 3; (조건) i++ (반복자) )
{
    //반복되는 블록
}
```
초기화 : 루프로 유입되기 전에 한번만 실행되는 초기화 섹션

조건 : 루프의 다음 반복을 실행할지 여부를 결정하는 조건 섹션

이결과가 true이거나 없으면 다음 반복이 실행되고 false면 루프가 종료됩니다 (조건 섹션은 부울 식이여야 합니다)

현재는 i의 값이 3보다 작을 경우 for문 블록을 실행합니다

반복자 : 루프의 본문을 실행할 때마다 수행되는 작업을 정의하는 반복자 섹션입니다

현재는 for문이 반복 될 때마다 i값을 1증가(후위) 시킵니다 (반복자 섹션에는 세미콜론 ; 가 없습니다)

<hr>

## 25편 반복문 while문

while문

루프를 실행하기전에 부울 식이 평가되기 때문에 while 루프는 0번 이상 실행됩니다


```c#
int i = 0;
while( i < 3 ) // 부울식이 true일 경우 블록을 실행합니다 값이 false가 될때까지 반복함
{
    Debug.Log("세번 출력됩니다");
    i++;
}
```
영상에서는 간단히 알려주셨기 때문에 추가적으로 찾아보자면

[BenKim님의 블로그](https://velog.io/@praconfi/for%EB%AC%B8%EA%B3%BC-while%EB%AC%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90) 자료 for문과 while문의 차이는 먼저

for문은 반복횟수가 정해진 경우, 주로 배열과 함께 많이 사용합니다

예시
```c#
int sum = 0;
for(int i=0; i<10; i++)
{
    sum +=i;
}
Debug.Log(sum);
```

while문을 사용하는 경우는 무한루프나 특정 조건에 만족할 때까지 반복하는 경우

주로 파일을 읽고 쓰는데 많이 사용된다

예시
```c#
int sum = 0;
i = 1;
while(i <= 10)
{
    sum += i;
    i++
}
Debug.Log(sum);
```

<hr>

## 26편 break문

배치된 지점에서 가장 가까운 바깥쪽 루프 또는 switch문을 종료합니다

제어는 종료된 문 뒤의 문으로 전달됩니다(있는 경우만)

바로 예시를 보여드리자면 우선 for문의 break입니다
```c#
for(int i = 0; i < 5; i++)
{
    if(i == 1)
    {
        break;
    }
    Debug.Log(i);
}
```

이중 for문에서 break문
```
for(int i = 0; i < 2; i++)
{
    for(int j = 0; j < 5; j++)
    {
        if(j == 1)
        {
            break;
        }
        Debug.Log(j);
    }
    Debug.Log("Hello I'm Drunken);
}
```
이런식으로 조건이 true가되서 break실행되면 가장 바깥쪽 루프를 종료한다

while문에서 break문
```c#
int i = 0;

while (i < 10)
{
    if( i == 1 )
    {
        break;
    }
    Debug.Log(i);
    i++
}
```

switch문에서 break문
```c#
string name = "홍길동"

switch (name)
{
    case "임꺽정" :
        Debug.Log("의적 임꺽정");
        break;
    case "홍길동" :
        Debug.Log("동해 번쩍 서해 번쩍!");
        break;
```

<hr>

## 26-2편 continue문

continue문은 이 명령문을 둘러싼 반복문의 다음 반복으로 즉시 제어를 전달합니다

바로 예시 들어갑니다 먼저 for문에서 countinue문입니다

```c#
for(int i = 0; i < 3; i++)
{
    if(i == 1)
    {
        continue;
    }
    Debug.Log(i);
}
```
i값이 1과 같은 조건에 맞을경우 다음명령문을 넘기고 바로 반복자 섹션으로 이동합니다

0부터 출력되고 조건에 맞는 1은 넘겨서 출력되지 않고 2부터 3, 4 순으로 출력됩니다

다음은 while문에서 continue문입니다
```c#
int i = 0;

while( i < 3)
{
    i++;
    
    if(i == 1)
    {
        continue;
    }
    Debug.Log(i);
}
```
이 경우에는 조건문 앞에 i++를 먼저 연산해주므로 1부터 시작하고

조건에 맞는 1은 출력되지 않고 2부터 출력되고 3, 4, 점점 증가됩니다

[BenKim님의 블로그](https://velog.io/@praconfi/for%EB%AC%B8%EA%B3%BC-while%EB%AC%B8%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90) 자료 for문과 while문의 차이는 먼저

for문은 반복횟수가 정해진 경우, 주로 배열과 함께 많이 사용합니다

예시
```c#
int sum = 0;
for(int i=0; i<10; i++)
{
    sum +=i;
}
Debug.Log(sum);
```

while문을 사용하는 경우는 무한루프나 특정 조건에 만족할 때까지 반복하는 경우

주로 파일을 읽고 쓰는데 많이 사용된다

예시
```c#
int sum = 0;
i = 1;
while(i <= 10)
{
    sum += i;
    i++
}
Debug.Log(sum);
```


## 오늘 정리를 마치며

이번에도 하루종일 이론정리를 해봤는데 저번보다는 영상 템포도 빨라지고

영상에 예시를 많이 활용하셔서 이런 글보다는 영상을 직접 보시는게 좋을듯합니다

계속해서 작성해보겠습니다~