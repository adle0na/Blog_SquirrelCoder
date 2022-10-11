<!-- Heading -->
#  스물한번째 도토리

<!-- Quote -->
> ## 언리얼 C++ 스크립팅을 위한 학습
>
> ### 홍정모의 따라 배우는 C++

마찬가지로 인프런 유료강의 홍정모의 따라 배우는 C++를 참고합니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

세번째 내용으로 변수와 기본적인 자료형 대해 자세히 학습해봅니다

<br>


## 변수와 기본적인 자료형

### 기본 자료형 소개

자료형은 여러가지가 있고 각각은 메모리에 저장되는데 사이즈도 다르며 저장되는 방식도 다르다

c++에서는 문자열은 char를 사용합니다

정수형은 integer로 int를 사용하는데 signed 와 unsigned가 있습니다

unsigned가 빠르다는 속도의 차이가 있고 디테일하게는 다루지 않겠습니다

singed int 는 여러 타입이 있는데 사용할때는 signed는 생략되어 적지 않습니다

char short int long longlong 등이 있습니다

unsigned int형은 생략을 할 수 없어

unsigned char, unsigned short, unsinged long, unsigned long long 와 같이 사용합니다

auto는 c#의 var처럼 자동으로 형을 결정해준다

그리고 sizeof(변수) 이렇게 하면 변수의 크기를 값으로 사용 가능합니다

또한 기존의 int x = 3; 과 같이 자료형 변수명 대입자 값 순서가 아니어도

자료형 변수명(값) 순서로 int a(123); 해도 같은 기능을 합니다

이를 direct initialization이라고 합니다

다른 방식으로는 int b { 123 }; 과같이 중괄호를 사용할 수 도 있습니다

이는 uniform initialization이라고 합니다

같은 형식으로 한번에 여러 변수를 선언 할 수도 있습니다 ex) int k, l, m;

이 방법을 사용 할때는 중간에 다른 형을 넣으면 안됩니다

그리고 뭔가 초기화 하는것처럼 보일 수 있어서 권장하지 않는 방법입니다

요즘은 코딩 스타일이 많이 바뀌어서 변수를 맨위에 모두 선언하고 코딩하는 방식이 아닌

사용할때마다 따로 선언해주는 느낌으로 많이 사용 한다고 합니다

이는 디버깅이 편해지고, 리팩토링 하기가 편한 장점이 있습니다

### 정수형 (Integers)

여러가지 기능들을 살펴봤지만 진짜 중요한것은 형마다 사이즈에 제한이 있고

넘어가면 문제가 생긴다는 점입니다 (이를 오버 플로우라고 합니다)

또 중요한것은 unsigned와 비교하여 그 차이점을 직접 아는것입니다

**홍정모 강사님의 과제 풀이 숫자 입력받아 홀수 짝수 표시 하기**
```c++
#include <iostream>

using namespace std;

int main()
{
    int num;

    cout << "정수를 입력하세요" << endl;

    cin >> num;

    if ((num % 2) == 0)
    {
        if (num == 0)
        {
            cout << num << " 을 제외한 다른 정수를 입력 해주세요" << endl;

            return 0;
        }
        cout << num << " 은(는) 짝수 입니다" << endl;
    }
    else
    {
        cout << num << " 은(는) 홀수 입니다" << endl;
    }
}
```

### c++ 11고정 너비 정수

int_fast8 8비트중 가장 빠른값을 출력합니다

int_least64 적어도 64비트를 갖는 타입입니다

### 무치형 (보이드, void)

함수를 선언할때 파라미터가 없을때 사용, 리턴 타입이 없는 경우에도 반드시 사용

보이드는 메모리를 차지하지 않기 때문에 자료형으로 선언할 수는 없습니다

하지만 포인터를 활용하여 사용하는 방법이 있다~ 는 방법만 알고 넘어갑니다

### 부동소수점 수 floating point numbers

부동소수점의 형 종류로는 float, double, long double 이 있습니다

사용할때 주의사항을 정리 합니다

소수점 뒤자리 표현을 생략할수록 값의 정확도는 떨어집니다

cout << std::setpercision(17); 와 같이 소수점 뒤로 원하는 만큼은 출력

내용 자체가 어렵다보니 더 깊은 내용은 나중에 다룹니다 개념만 챙겨갑시다

### 불리언 자료형 과 조건문 if

코드를 작성할때 true, false보다 0, 1로 치는게 훨씬 효율적이다

또한 0 이아니면 true로 인식한다

### 문자형 char type

아스키 값에 대해 설명합니다

char 형을 사용할때 일반 정수는 그대로 한 글자를 사용할땐 ''를

여러 문자를 사용할떈 ""를 사용합니다

```c++
char c1(65);
// 문자형이기 때문에 코드표에 의해 A로 출력됩니다
char c2('A');
// 마찬가지로 A가 출력됩니다
int(c1);
// 캐스팅하여 int로 형변환 했기 때문에 65가 출력됩니다

static_cast<char>(65) << endl;
// 문자형인 65값을 반환하므로 A 출력
static_cast<int>('A') << endl;
// 문자열 A값의 정수 값을 반환하므로 65 출력
```
위의 static_cast<자료형>(값) 형식을 사용하면 컴파일러가 읽는데 좀더 수월하다고 합니다

번거로운 코딩이지만 협업할때 다른 개발자가 봤을때 캐스팅한지 구분을 확실히 하기위해선 좋은 방법입니다

cin으로 문자 하나를 받는 코드를 작성한 경우 입력값을 abc로 한 경우

a는 출력이 되지만 bc는 버퍼에 남아 입력을 대기합니다

### 리터럴 상수 literal constants

````c++
float pi = 3.14f;

int i = -1234u;
// 값 뒤에 u를 붙이면 unsigned 값이 됩니다 근데 강제로 바꾸는거라 추천하진 않습니다
// 차라리 캐스팅으로 명확히 보여주는것이 좋습니다
````
그리고 10진수 8진수 16진수에 대해 설명해주십니다

```c++
int x = 012;
// 앞에 0을 붙이면 8진수로 인식하여 10을 출력합니다
int x = 0xF;
// 마찬가지로 0x를 붙이면 16진수로 인식하여 15가 출력됩니다
int x = 0b1011'1111'1010;
// 2진수를 표기할때는 구분하기 쉬우라고 ''를 중간에 넣어도 오류가 없습니다
// 2진수 외에도 10진수에도 사용가능합니다
```

코드 작성시에 리터럴로 다음과 같이 적으면 당장은 돌아가지만 장기적으로 안좋습니다

```c++
int num_items = 123;
int price = num_items * 10;
// 10 값은 변경하게되면 연계되는 다른값과 안맞을수도있고 무슨값인지도 모릅니다
// 따라서 알아보기 쉽도록 아래와 같이 작성하는것이 좋습니다

const int price_per_item = 10;
int num_items = 123;
int price = num_items * price_per_item;
// 이렇게 되면 10이 뭘 뜻하는지 명확하게 알 수 있게 됩니다

```
### 심볼릭 상수 symbolic constants

상수의 두번째 종류 심볼릭 입니다 예시로 진행합니다

```c++
int main()
{
    using namespace std;
    
    // double gravity{9.8};
    // 임의로 변경하지 않았으면 하는 값은 앞에 const를 붙여 수정하면 안되는 단어로 표시합니다
    const double gravity{9.8};
    
    return 0;
}
```

다른 예시입니다 다른 사용자가 변경하면 안되는 파라미터를 건드릴 수 없도록

```c++
void printNumber(const int& my_number)
{
    // my_number = 456;
    // const로 지정해뒀기 때문에 이 구문에서는 오류가 발생합니다
    
    int n = my_number;
    
    cout << my_number << endl;
}
```
다른 예시입니다 컴파일 할때 이미 결정되는 컴파일 타임 상수와 런타임 상수를 봅니다
```c++
int main()
{
    const int my_const(123);
    // 컴파일을 안해도 값이 123으로 정해져 있는 컴파일 타임 상수
    
    int number;
    cin >> number;
    
    const int special_number(number);
    // 컴파일을 하고 입력을 받아야 값이 정해지는 런타임 상수
    
    
    // 두가지의 명확한 구분을 위해 있는 기능인 constexpr을 사용하면
    
    constexpr int my_const(123);
    
    // constexpr int special_number(number);
    // 이 구문은 런타임 상수이기 때문에 오류가 발생합니다
    const int special_number(number);
    
    // 명확한 구분이 됩니다
   
```

또한 const가 여기저기 많이 쓰일경우 따로 한곳에 모아서 사용하는 방법도 있는데요

.h 파일을 생성해서 거기에 const 값들을 모두 몰아서 적어줍니다

```c++
#pragma once

namespace constants
{
	constexpr double pi(3.141592);
	
	constexpr double avogardro(6.0221413e23);
	
	constexpr double moon_gravity(9.8 / 6.0);
	// ...
}
```

그리고 메인 cpp 파일에서 받아서 사용해줍니다

```c++
#include <iostream>
#include "Myconstant.h"

using namespace std;

int main()
{
	double radius;

	cin >> radius;

	double circumference = 2.0 * radius * constants::pi;

	cout << circumference << endl;

	return 0;
}

```

## 이번 과정을 마치며

아직 뭔가를 만든다는 느낌은 없지만 기초가 매우 튼튼하게 쌓여 가는듯 합니다

차근차근 언젠가는 활용할 날을 기다리며 계속 강의를 들어봅니다