<!-- Heading -->
#  스물두번째 도토리

<!-- Quote -->
> ## 언리얼 C++ 스크립팅을 위한 학습
>
> ### 홍정모의 따라 배우는 C++

마찬가지로 인프런 유료강의 홍정모의 따라 배우는 C++를 참고합니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

4번째 내용입니다 연산자들에 대해 배워봅니다

<br>

## 연산자들

### 연산자 우선순위와 결합 법칙

한 식에 여러가지 연산이 있으면 어떤 계산을 먼저 할까에 대한 내용입니다

우선 기존에 알고 있던대로 곱하기 * 와 나누기/ 의 우선 순위가 +, - 보다 높으며

Associativity 라는 내용을 다루게 됩니다

우선 순위가 같은 순위를 만났을때 왼쪽부터 계산하는것을 말합니다

### 산술 연산자 arithmetic operators

단항 연산자는 단순히

- 기호를 더하는 개념입니다 +는 잘쓰이지 않죠

나머지 계산 %(모듈러스)는 정수 나머지와 실수 나머지의 결과가 다릅니다 예를 들면

```c++
int x = 7;
inx y = 4;

cout << x / y << endl;
cout << float(x) / y << endl;
cout << x / float(y) << endl;
cout << float(x) / float(y) << endl;

// 위의 경우 첫번째를 제외하고 1.75의 결과가 출력됩니다
// 계산시에 하나라도 실수일 경우 실수로 출력되는 것입니다

```

음수와의 연산시에는 왼쪽 부호에 따라 출력 값이 정해집니다

둘다 음수라고 양수가 출력되진 않더라구요

물론 곱연산은 둘다 음수면 양수가 나옵니다

이건 C#도 마찬가지였던 연산인데

z += y; 는 z = z + y; 의 기능을합니다

제일 핵심적인 내용은 **정수 나누기와 실수 나누기의 결과가 다르다** 입니다

### 증감 연산자 increment decrement operators

증감 연산자는 전위와 후위 연산이 있습니다

x++, ++x, --x, x--

전위 연산은 출력하면 1이 추가된 값이 나오지만 후위 연산은 출력한 값은 그대로입니다

후위 연산은 값이 더해지기만 하고 출력은 다음 값에 나오기 때문입니다

### sizeof, 쉼표 연산자, 조건부 연산자

먼저 sizeof는 데이터의 크기 값을 반환하는 연산자입니다

```c++
#include <iostream>

using namespace std;
{
    float a;
    
    cout << sizeof (float);
    // 자료형의 크기를 나타냅니다
    cout << a;
    // 연산자 이기 때문에 괄호가 없어도 변수의 크기를 반환합니다
    
    return 0;
}
```

**comma operator**

```c++
#include <iosteam>

using namespace std;

int main()
{
    int x = 3;
    int y = 10;
    int z = (++x, ++y);
    
    cout << x << " " << y << " " << z << endl;
    // z의 출력값은 11이 나오게 되는데
    /*
    ++x;
    ++y;
    int z = y;
    와 같은 기능을 하기 떄문입니다
    */
    return 0;
}

```

한가지 더 예를 보자면

```c++
int a = 1, b = 10;
int z;

z = (++a, a + b);
// 여기서 z의 출력값은 a 후위증감으로 2와 10값을 더해 12를 출력합니다
```

if문을 사용할때는 const를 붙일 수 없기 때문에 삼항연산자를 통해 코드를 작성합니다

**잘못된 예**
```c++
int main()
{
	bool onSale = true;

	const int price;
	// 조건부 연산자 값이 const가 되버리면 에러가 발생합니다

	if (onSale)
		price = 10;
	else
		price = 100;

	cout << price << endl;

	return 0;
}
```

**옳은 예**
```c++
int main()
{
	bool onSale = true;

    const int price = (onSale == true) ? 10 : 100;
    // onSale 조건이 true 면 10을 false면 100을 반환합니다
    
	cout << price << endl;

	return 0;
}
```

### 관계 연산자 Relational Operators

정수 끼리의 크기 관계 연산은 큰 문제가 없으나 소수 연산이 들어가면 문제가 생깁니다 부동소수점 개념이죠

```c++
int main()
{
	double d1(100 - 99.99); // 0.001
	double d2(10 - 9.99); // 0.001

	if (d1 == d2)
		cout << "equal" << endl;
	else
		cout << "Not equal" << endl;

	return 0;
}
```

자 그럼 저 두수의 오차만큼 작은 차이일 경우 같다고 출력하도록 해봅니다

```c++
int main()
{
	double d1(100 - 99.99); // 0.001
	double d2(10 - 9.99); // 0.001

    // 오차 값의 범위 설정
    const double epsilon = 1e-10;

	if (std::abs(d1-d2) < epsilon)
		cout << "Approximately equal" << endl;
	else
		cout << "Not equal" << endl;

	return 0;
}
```

### 논리 연산자 logical operators

이번 강의도 C#과 같은 개념의 !=, &&, || 와같은 내용들이지만

이것을 할 줄몰라 if를 여러개로 쪼개서 쓰면 영향 범위가 다르기 때문에 반드시 논리 연산자 사용을 권장 합니다

다른내용 말고 실질적으로 문제가 발생할 수 있는 구간을 보겠습니다

```c++
int main()
{
    int x = 2;
    int y = 2;
    
    if (x == 1 && y++ == 2)
    {  
        // do something
    }
     
    cout << y << endl;
    // x가 1이면 논리식 대로 3이 나오지만 2인경우엔 2가 출력됩니다
    // 논리 연산은 &&의 경우 좌항인 x == 1 이 아니면 그대로 연산을 끝내버리기 때문입니다
    // &&는 둘다 true일 경우만 true를 반환하기 때문에 이런일이 발생합니다
    // 근데 이런것도 의도적으로 이용할 수도 있습니다
   
    return 0;
}
```

헉 수학시간에나 듣던 드모르간 법칙의 등장입니다

```c++
int main()
{
    bool x = true;
    bool y = false;
    
    // 드모르간 법칩
    !(x && y);
    // = !x || !y; 괄호를 없애면 &&가 ||로 ||가 &&로 바뀝니다 
    return 0;
}
```

그리고 좀더 복잡한 XOR의 경우 C++에는 없기 때문에

if(  a != b )의 형식으로 사용합니다

좀더 복잡한 개념을 보겠습니다

```c++
bool v1 = true;
bool v2 = false;
bool v3 = false;

bool r1 = v1 || v2 && v3;
// 이경우를 보면 원래는 좌항인 v1 || v2부터 계산이 되야 하지만 논리 연산자의 중요도가 다르기 때문에
// 우항인 v2 && v3가 먼저 계산되어 r3와 같은 값이 나옵니다

bool r2 = (v1 || v2) && v3;
bool r3 = v1 || (v2 && v3);

cout << r1 << endl;
cout << r2 << endl;
cout << r3<< endl;

// 출력하면 1, 0, 1 순으로 값이 출력됩니다

return 0;
```


## 이번 과정을 마치며

아직 뭔가를 만든다는 느낌은 없지만 기초가 매우 튼튼하게 쌓여 가는듯 합니다

차근차근 언젠가는 활용할 날을 기다리며 계속 강의를 들어봅니다