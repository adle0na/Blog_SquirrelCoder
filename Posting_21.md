<!-- Heading -->
#  스무번째 도토리

<!-- Quote -->
> ## 언리얼 C++ 스크립팅을 위한 학습
>
> ### 홍정모의 따라 배우는 C++

이번 업로드는 인프런 유료강의 홍정모의 따라 배우는 C++를 참고합니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

두번째 내용으로 C++ 기초적인 사용법에 대해 자세히 학습해봅니다

<br>


## C++의 기초적인 사용법

### 프로그램의 구조

먼저 함수를 정의합니다

가장 기본인 main함수로 이것은 쉽게 바꿀순 없습니다

이 함수의 의미는 오퍼레이팅 시스템이 제일 먼저 찾는 함수로

기능 수행을 위한 프로그램을 제작할땐 main이라는 함수가 반드시 있어야 합니다

```c++

int main(void)
{
    // 여기에 간단히 연산식을 써보는 수업입니다
    int x = 5;
    x = 3;
    int y = x + 2;
    
    std:cout << 1 + 3 << std::endl;
    
    return0;
}

// #include처럼 앞에 #이 붙는 구문들을 전처리기라고 합니다
```

지금은 이런게 있다 정도로만 설명하시고 넘어갑니다 나중에 파트별로 자세하게 정리할 예정입니다

### 주석 Comments

주석은 컴파일러가 무시하게 하는 구문으로

```c++
// 하여 한줄만 주석다는 방법과

/*
이안을 모두 주석처리 방법이 있습니다 
*/
```

단축키 ctrl + k,c 를 입력하시면 해당 줄이 각각 주석처리 됩니다

프로그래밍을 하다보면 내코드를 봐도 내용을 알기 힘듭니다

따라서 주석을 달때는 남이 본다고 생각하면 잘안달게 되기 때문에

시행착오를 통해 나를 위해 설명을 한다고 생각하고 주석을 달면 좋습니다

특히 수학적으로 복잡한 코드는 어떤 자료를 참고했는지 어떻게 결과가 나오는지 적어두는것이 좋습니다

ex )

```c++
// 마법 물약을 먹으면 시야 거리가 0
sight = 0;
```

코드의 내용을 추론하느라 시간을 낭비할일을 줄이도록

주석을 잘다는 방법은 초보때 부터 고민을 해두어 습관화 하도록 합니다

### 변수와의 첫 만남

**객체 Object** 

현실에 있는 물체, 실존하는 물체

객체는 메모리에 담겨있습니다

그리고 담겨있는것을 사용하려면 이름이 있어야합니다

**변수 Variables**

내부적으로 작동하는 값

**Left-values, Right-values**

**초기화initialization, 대입assignment**

**초기화를 안 했을 때의 문제점**

항목은 이렇게 정리해주셨지만 자세한 내용은 코드를 보며 시작합니다

```c++
int main()
{
    // int 같은 경우 자료형으로 크기나 구조를 나타냅니다
    // 변수명은 보통 이름이라고 생각하면 됩니다
    int x = 123;
    // assignment는 대입으로 현재 x변수의 메모리 공간에 123값을 삽입하는 개념입니다
    // 대입연산자 라고도 부릅니다
    
    std::cout << x << std::endl;
    std::cout << &x << std::endl;
    
    // 위코드를 각각 출력하면 123과 00EFFE0C로 출력됩니다
    // &를 앞에 붙이면 실제로 변수의 메모리가 가진 주소값을 반환하기 때문입니다 
 
    int y;
    
    std::cout << y << std::endl;
    
    // 위 구문 같은경우 Warning으로 경고가 뜨지만 경고엔 너무 목메지 않는것이 좋습니다
    // 하지만 UnInitialize같은 기초적인 오류는 정리하는것이 좋습니다
   
   int x(123); // Initialization
   
   x = 5; // assignment
   
   return 0;
}
```

무서운 이야기를 해주셨습니다 디버그 했을때 오류가 발생했다가도

Release 를 하니 초기화가 안된 값을 0으로 하여 빌드가 되버립니다

이런 경우 어떻게 보면 배려이지만 프로그래밍이 복잡해지면 문제가 되기도 합니다

결국 이 이야기의 중요 내용은 변수는 초기화를 꼭 해야된다는 것입니다

### 입출력 스트림과의 첫만남 cin, cout

입출력 스트림을 사용하기 위해선 먼저 #include <iodstream> 을 적어주어야 합니다

```c++
int main()
{
    // 여기서 cout은 std라는 네임스페이스 안에 포함되어 있기 때문에 이렇게 작성합니다
    std::cout << "출력하고싶은 문자열" << std::endl; 
    // <<는 아웃풋오퍼레이터로도 불립니다 endl구문을 쓰지 않으면 줄바꿈을 하지 않고 붙여서 출력합니다
    
    std::cout << "abc" << "\t" << "def" << std::endl;
    // 이를 실행하게 되면 tap키를 누른것과 같이 공백과 함께 줄맞춤 기능을 사용해줍니다
    // 출력 값은 abc    def 와같이 나옵니다 실제로는 한칸으로 인식 됩니다
    // \n을 사용하면 endl과 비슷한 기능이지만 똑같지는 않습니다 이는 다음에 자세히 배웁니다
    
    using namespace std;
    // 드디어 위와같은 구문을 적게되면 std::를 사용하지 않아도 됩니다
    cout << "123" << endl;
    
    // 지금까지 cout이 출력이었다면 cin은 값을 입력하게됩니다
    
    int x = 1;
    
    cout << "Before your input, x was " << x << endl;
    
    cin >> x;
    
    cout << "Your input is " << x << endl;
    
    return 0;
    
}
```

그리고 이렇게 배운 cout과 cin은 네트워크 관련 코딩을 할때도 다시 사용할 수 있습니다

### 함수와의 첫 만남

```c++
#include <iostream>

using namespace std;

int main()
{
    cout << 1 + 2 << endl;
    cout << 3 + 4 << endl;
    cout << 8 + 13 << endl;
    
    return 0;
}
```
위와 같은 경우 같은 연산을 반복하고 있습니다

함수라는 것은 먼저 출력값의 데이터를 사용합니다

```c++
#include <iostream>

using namespace std;

// 먼저 함수의 이름은 자세하게 적어주는게 좋습니다
int addTwoNumbers(int num_a, int num_b)
{
    int sum = num_a + num_b;
    
    return sum;
}

int main()
{
    cout << addTwoNumbers(1, 2) << endl;
    cout << addTwoNumbers(3, 4) << endl;
    cout << addTwoNumbers(8, 13) << endl;
    
    return 0;
}
```

지금 과정은 오히려 함수화 한게 복잡해 보이지만 함수내의 기능이 복잡해지면 반드시 필요한 기능입니다

가령 저 연산의 기호를 +가 아니라 *으로 바꾼다면 위의 함수만 바꿔주면 동일한 기능을 하게 됩니다

또한 우클릭을 누르고 rename을 사용하면 해당 함수와 같은 이름을 모두 바꿔줍니다

다음은 중단점을 사용한 디버깅 방식입니다

왼쪽 디버그 할지점을 선택하고 F11을 눌러 진행하다보면 함수가 있는곳으로 넘어갑니다

이 개념을 잘 이해하면 재귀함수 부분에서 편해집니다

```c++
#include <iostream>

using namespace std;

// 리턴 값이 없음으로 함수 앞에 void 입력
void printHelloworld()
{
    cout << "Hello World" << endl;
    
    return;
    // 여기에 return을 적은 경우 반환하여 main함수로 돌아갑니다
}

int main()
{
    printHelloWorld();

    return 0;
}

```

C++에서는 함수안에서 함수를 정의 할 수 없습니다

### 키워드와 식별자 이름짓기

![image description](https://imgur.com/a/GEpUU1g.png)

C++은 우선 이러한 키워드들이 있고 변수명을 지을때 주의 하여야한다

변수 이름지을때 주의할 내용은 C#때와 동일하므로 넘어가겠습니다

### 지역 범위

```c++
#include <iostream>

int main()
{
    int x = 0;
    {
        // 함수명 없이 그냥 이렇게 영역 구분을 위한 중괄호를 사용해도 됩니다
        
        int x = 1;
    }
    {
        int x = 2;
        // 현재 지역변수로 사용되고 있기 때문에 메모리 주소가 다르고 중괄호 내에서만 인식합니다
    }
}
```

마찬가지로 함수내에서 선언한 변수는 그범위 내에서만 적용되며

밖에서 선언되게 되면 다른 메모리를 가진 값이 됩니다

```c++
#include <iostream>

using namespace std;

void doSomething(int x)
{
    x = 123;

    cout << x << endl;
}

int main()
{
    int x = 0;

    cout << x << endl;
    doSomething(x);
    cout << x << endl;

    return 0;
}
```
점검 문제의 출력은 0, 123, 0 이었습니다

먼저 main을 살펴보면 x = 0으로 선언되어있어 0이 출력되고

매개변수 x를 가진 doSomthing 함수를 보면 함수 내의 지역변수에서 x 값을 123으로 출력합니다

마지막으로 다시 main함수의 전역변수인 x를 출력하면 당연히 0이 출력됩니다

### 연산자와의 첫 만남

**Literal** 리터럴

**Operand** 피연산자

**단항, 이항, 삼항**

```c++
#include <iostream>

using namespace std;

int main()
{
    int x = 2;
    // assignment 대입연산자로 x 변수의 메모리 값에 2를 대입합니다
    
    // 여기서 1과 2는 리터럴 상수이고 +는 연산자입니다
    cout << 1 + 2 << endl;
    // 이러한 값들을 피연산자 Operand라고 합니다
    
    cout << "My Home" << endl;

    return 0;
}
```

단항 연산자 같은 경우 -x 한항을 가진 연산자이고

이항 연산자는 1 + 2 처럼 2개의 항을가진 연산자입니다

3개가 들어가면 삼항 연산자인데 조건 연산자로도 불리우며 C++의 유일한 삼항 연산자입니다

예시로 int y = ( x > 0 ) ? 1 : 2; 같은 경우

x 가 0보다 조건이 참일 경우 왼쪽값 1을 거짓일 경우 오른쪽값 2를 가지게 됩니다 

### 기본적인 서식 맞추기

우선 기본적인 입력 서식으로 탭, 줄바꿈을 언급하셨고

줄바꿈의 경우 , 나 <<로 구분이 되도록합니다

간단히 예쁘게 코딩하는 법의 기초를 알려주셨습니다

### 선언과 정의의 분리

```c++
#include <iostream>

using namespace std;

int main()
{
    cout << add(1, 2) << endl
    
    return 0;
}

int add(int a, int b)
{
    return a + b;
}

int multiply(int a, int b)
{
    return a * b;
}

int substract(int a, int b)
{
    return a - b;
}
```
위의 경우 컴파일러는 순서대로 읽기 때문에 오류가 발생합니다

따라서 정리를 하려면 아래와 같은 방식으로 하는것이 좋습니다

```c++
#include <iostream>

using namespace std;

// 이방식을 전방 선언이라고 합니다
int add(int a, int b);
int multiply(int a, int b);
int substract(int a, int b);

int main()
{
    cout << add(1, 2) << endl
    
    return 0;
}

// 이부분은 정의가 됩니다
int add(int a, int b)
{
    return a + b;
}

int multiply(int a, int b)
{
    return a * b;
}

int substract(int a, int b)
{
    return a - b;
}
```
### 헤더파일 만들기

지금 부터는 복잡해질 코드를 여러파일로 쪼개는 방법을 알아봅시다

메인 함수는 그대로 두고 밑의 함수들을 잘라서 사용해봅시다

아래는 따로 Calculate.cpp 파일을 제작하여 함수를 넣어둡니다

```c++

int add(int a, int b)
{
    return a + b;
}

int multiply(int a, int b)
{
    return a * b;
}

int substract(int a, int b)
{
    return a - b;
}

```

그리고 새로 calculate.h로 헤더파일을 생성하여 안에 선언을 해줍니다 

```c++
#pragma once

int add(int a, int b);

```

그리고 다시 메인 cpp 파일로 돌아가 맨위에 적어주면 인식하게 됩니다
```c++

#include <iostream>
#include "calculate.h"

using namespace std;

int main()
{
    cout << add(1, 2) << endl
    
    return 0;
}
```

만약 헤더파일의 위치를 변경할 경우

Solution Explorer에서 "Remove"를 눌러 지운후

로컬 폴더에서 드래그앤 드랍하여 새폴더를 생성하고 경로로 옮겨주려고 한다면

[ #include "폴더이름/calculate.h" ] 와같은 식으로 경로도 지정해주게 되면 정상 작동합니다

작업을 시작하기 전 가급적 .cpp파일과 .h파일은 구분 해두는것이 좋습니다

### 헤더 가드가 필요한 이유

먼저 LinKing error 대처법입니다

컴파일러가 읽지만 못하게 하도록 cpp파일을 Remove로 삭제하고 빌드하면 

파일을 찾지 못했다고 에러가 뜨게 되는데

로컬 폴더에서 드래그드랍하여 다시 인식 시켜주면 정상화 됩니다

이런 연결 오류는 개념적으로 많이 해보다 보면 익숙해 진다고 합니다

다시 헤더가드 내용으로 넘어가면

헤더파일을 새로 생성하면 #pragma once 라는 코드가 있는데 이것이 헤드가드입니다

헤더파일을 include 하다보면 중복 되는 경우가 있는데 이때 오류를 방지해주는것이

헤더가드로 중복된 경우 한번만 사용하게 합니다

### 네임스페이스 (명칭공간)

기능은 다르지만 같은 기능을 하는 함수를 만들고 싶은 경우 여러방법이 있지만

이번엔 네임스페이스를 사용하여 구분하는 방법을 알아 보도록 합니다

```c++
#include <iostream>

using namespace std;

namespace Var1
{
    int cal(int a, int b)
    {
        return a + b;
    }
}

int cal(int a, int b)
{
    return a * b;
}

int main()
{
    // 네임스페이스 안의 함수를 지정하여 사용하려면 네임스페이스와 :: 뒤에 함수를 사용합니다
    cout << Var1::cal(3, 5) << endl;
    cout << cal(3, 5) << endl;

    return 0;
}
```

또한 네임스페이스 안에 또 네임스페이스를 넣을 수 있습니다

마찬가지로 네임스페이스 옆에 :: 를 한번더 경로 지정하듯 사용하면 됩니다

계속 사용하는 std 같은 경우 코드를 들어가 보면 namespace 코드가 없는데

이는 전처리기를 사용한 매크로 기능이라는 개념만 가지고 다음 시간에 다뤄봅니다

### 전처리기와의 첫 만남

먼저 매크로의 사용법을 봅니다

```c++
#include <iostream>
using namespace std;

#define MY_NUMBER 9
// 매크로 이름은 대문자로 하는것이 좋습니다

int main()
{
    cout << MY_NUMBER << endl;
    
    return 0;
}
```

요즘은 매크로를 안쓰는 추세고 그냥 함수를 쓰는게 좋습니다

왜냐하면 이런 기능도 있기 때문입니다

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int main()
{
	cout << std::max(1 + 3, 2) << endl;
}
```

위와 같은 방법으로 간편하게 사용이 가능한 기능들이 있습니다

네임스페이스는 사용하는 해당 중괄호 안에 선언해주는 것이 좋습니다

## 이번 과정을 마치며

굉장히 자세하게 차근차근 알려주시는 느낌입니다 이 많은 강의를 들었지만

아직 연산자들을 다루지도 않네요 하지만 뭔가 천천히 늘어가는 기분입니다

꾸준히 학습해봐야겠네요