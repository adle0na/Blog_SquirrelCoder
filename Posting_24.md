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
### 이진수 Binary Numbers

10진수를 자세히보면

337 같은 경우 (10^2 * 3) + (10^1 * 3) + (10^0 * 7)로

2진수도 마찬가지로

0 > 1 > 10 처럼 자리수를 올리며 0을 붙입니다

이번엔 2진수를 10진수로로 변환해봅니다

10 = 2^1*1 + 2^0*0 = 2

11 = 2^1*1 + 2^0*1 = 3 

틈새 암기 integer 4byte

0101 1110 을 변환해봅니다

2^6*1 + 2^4*1 + 2^3*1 + 2^2*1 + 2^1*1

64 + 16 + 8 + 4 + 2

94가 나오네요 물론 계산기가 해주지만

우리는 직접 할필요는 없지만 개념만 알아갑시다

그 다음으로 10진수를 2진수로 바꿔봅시다

94를 다시 2진수로 바꾸기 ( 과제 )

94 / 2 -> 47 나머지 0

47 / 2 -> 23 나머지 1

23 / 2 -> 11 나머지 1

11 / 2 -> 5 나머지 1

5 / 2 -> 2 나머지 1

2 / 2 -> 1 나머지 0

1 / 2 -> 0 나머지 1

0101 1110

148을 예시로 바꿔봅니다

148 / 2 -> 74 나머지 0

74 / 2 -> 37 나머지 0

37 / 2 -> 18 나머지 1

18 / 2 -> 9 나머지 0

9 / 2 -> 4 나머지 1

4 / 2 -> 2 나머지 0

2 / 2 -> 1 나머지 0

1 / 2 -> 0 나머지 1

1001 0100 역순으로 정렬하고 칸을 나누면 이렇게 나옵니다

2^7*1 + 2^4*1 + 2^2*1

128 + 16 + 4 = 148 다시 나오네요

그리고 보수 개념이 나옵니다

1001 1110 을 보수로 받으면

0110 0001 인데 여기에 맨앞이 1인 음수이므로 1을 더합니다

0110 0010 비트 전환해보면 앞에 모든 자리에 1을 더하니 -98이 나오네요

부가적으로 signed 와 unsigned의 값이 다릅니다

**연습문제**

0100 1101 -> 10진수 변환

64 + 8 + 4 + 1 = 77 

93 -> 8비트 무부호 정수

93 / 2 -> 46 나머지 1

46 / 2 -> 23 나머지 0

23 / 2 -> 11 나머지 1

11 / 2 -> 5 나머지 1

5 / 2 -> 2 나머지 1

2 / 2 -> 1 나머지 0

1 / 2 -> 0 나머지 1

0101 1101

-93 -> 8비트 부호 정수

1010 0011

1010 0010 -> 무부호 10진수

128 + 32 + 2 = 162

1010 0010 -> 부호 10진수

0101 1110 -> 94

### 비트단위 연산자 Bitwise Operators

지금 까지의 int 나 float 등 타입단위 연산을 했지만

비트 단위는 그 반대로 컴퓨터 데이터적으로 값단위에 대한 연산입니다

메모리를 아끼기 위해 비트단위 연산자를 사용합니다

비트 단위 연산자는 총 6종류가 있습니다

// << left shift

// >> right shift

cout에서 쓰던 >> 와는 다른 개념입니다

~, &, |, ^
비트연산에서는 XOR 오퍼레이터는 있습니다

가장 많이 사용되는 부분은 비트 마스크입니다 빠른 게임을 위해선 필수 입니다

```C++
int main()
{
	unsigned int a = 1;

	cout << std::bitset<4>(a) << endl;

	return 0;
}
```
사용은 이런식으로 하며 출력값은 0001로 나옵니다

```c++
int main()
{
	unsigned int a = 1;

	cout << std::bitset<4>(a) << endl;

	unsigned int b = a << 1;

	cout << std::bitset<4>(b) << endl;

	return 0;
}
```

이번엔 b 변수를 선언하고 여기에 a를 << 1만큼 shift 해봅니다

출력 값은 0001에서 1칸밀린 0010으로 나옵니다

```c++
int main()
{
	unsigned int a = 1;

	cout << std::bitset<4>(a) << endl;

	unsigned int b = a << 4;

	cout << std::bitset<4>(b) << " " << b << endl;

	return 0;
}
```
이렇게 해서 0001인 a를 4칸 만큼 shift 하게되면 출력은 0000으로 나오지만

1칸 앞이 안보인거라 10진수로보면 16이 출력됩니다

이제 8비트로 해서 좀더 넓게 봐봅시다

```c++
int main()
{
	unsigned int a = 1;

	cout << std::bitset<8>(a) << endl;

	cout << std::bitset<8>(a << 1) << " " << (a << 1) << endl;
	cout << std::bitset<8>(a << 2) << " " << (a << 2) << endl;
	cout << std::bitset<8>(a << 3) << " " << (a << 3) << endl;
	cout << std::bitset<8>(a << 4) << " " << (a << 4) << endl;
	return 0;
}
```
이렇게 하면 출력값은 0000 0010 2, 0000 0100 4, 0000 1000 8, 0001 0000, 16 이 출력됩니다 

이번엔 반대로 >> right shit를 사용해 봅시다

```c++
int main()
{
	unsigned int a = 1024;

	cout << std::bitset<16>(a) << endl;

	cout << std::bitset<16>(a >> 1) << " " << (a >> 1) << endl;
	cout << std::bitset<16>(a >> 2) << " " << (a >> 2) << endl;
	cout << std::bitset<16>(a >> 3) << " " << (a >> 3) << endl;
	cout << std::bitset<16>(a >> 4) << " " << (a >> 4) << endl;
	return 0;
}
```
잘 볼 수 있도록 자리값을 16비트로하여 보면 출력이 이렇게 나옵니다

0000010000000000

0000001000000000 512

0000000100000000 256

0000000010000000 128

0000000001000000 64

정말 완벽하게 1을 한칸씩 밀어서 연산하는 모습입니다

그리고 비트연산에서 NOT은 ~를 사용합니다

그리고 나머지 연산들 정리 내용입니다

```c++
int main()
{
	unsigned int a = 0b1100;
	unsigned int b = 0b0110;

	cout << std::bitset<4>(a & b) << endl; // bitwise AND 둘다 1

	cout << std::bitset<4>(a | b) << endl; // bitwise OR 둘중 하나라도 1

	cout << std::bitset<4>(a ^ b) << endl; // bitwise XOR 둘다 1이면 0

	a &= b; // 이런 형태로 줄여서 사용 가능

	return 0;
}
```

다음은 연습 해보기 입니다

```c++
int main()
{
	unsigned int a = 5;
	unsigned int b = 12;

	cout << std::bitset<4>(a & b) << endl; // bitwise AND 둘다 1

	cout << std::bitset<4>(a | b) << endl; // bitwise OR 둘중 하나라도 1

	cout << std::bitset<4>(a ^ b) << endl; // bitwise XOR 둘다 1이면 0

	a &= b; // 이런 형태로 줄여서 사용 가능

	return 0;
}
```

5는 0101
12는 1100입니다

& AND = 0100 이 나올것이고

| OR = 1101 이 나올것이며

^ XOR = 1001 이 나올것입니다

다행히 정답이군요

### 비트 플래그, 비트 마스크 사용법 Bit flags, Bit masks

비트 연산 실사용법을 익혀봅시다

먼저 게임의 아이템을 만든다고 생각해봅시다

아이템을 이벤트의 파라미터로 사용하는경우 아이템이 12개라면 파라미터가 12개가 되버립니다

이제 사용하는 방식은 Array를 좀더 컴팩트한 방식으로 다루는 느낌입니다
```c++
int main()
{
	const unsigned char opt0 = 1 << 0;
	const unsigned char opt1 = 1 << 1;
	const unsigned char opt2 = 1 << 2;
	const unsigned char opt3 = 1 << 3;

	cout << bitset<8>(opt0) << endl;
	cout << bitset<8>(opt1) << endl;
	cout << bitset<8>(opt2) << endl;
	cout << bitset<8>(opt3) << endl;

	unsigned char items_flag = 0;
	cout << "No item" << bitset<8>(items_flag) << endl;

	// 0번 아이템 획득
	items_flag |= opt0;
	cout << "Item0 Obtained" << bitset<8>(items_flag) << endl;
	
	// 3번 아이템 획득
	items_flag |= opt3;
	cout << "Item3 Obtained" << bitset<8>(items_flag) << endl;

	// 3번 아이템 상실
	items_flag &= ~opt3;
	cout << "Item3 lost" << bitset<8>(items_flag) << endl;

	// 아이템 0번 소유 확인
	if (items_flag & opt0) { cout << "Has item1" << endl; }

	// 아이템 2, 3 획득
	items_flag |= (opt2 | opt3);
	cout << "Item2, 3 Obtained" << bitset<8>(items_flag) << endl;

	// 아이템 2번, 3번 상실
	if ((items_flag & opt2) && !(items_flag & opt1))
	{
		items_flag ^= (opt2 | opt3);
	}

	cout << bitset<8>(items_flag) << endl;

	return 0;
}
```
이렇게 해서 비트 플래그를 사용해 봤고 이번엔 비트 마스크를 사용해봅니다

비트 마스크는 보통 컬러테이블의 코드를 사용할때 활용됩니다

```c++
int main()
{
	// 앞의 두자리 0x뒤의 두자리 red, 두자리씩, green, blue
	const unsigned int red_mask = 0xFF0000;
	const unsigned int green_mask = 0x00FF00;
	const unsigned int blue_mask = 0x0000FF;

	cout << std::bitset<32>(red_mask) << endl;
	cout << std::bitset<32>(green_mask) << endl;
	cout << std::bitset<32>(blue_mask) << endl;

	unsigned int pixel_color = 0xDAA520;

	cout << std::bitset<32>(pixel_color) << endl;

	// 현재 컬러 값중 blue 부분은 다 0이기 때문에 0이 출력됩니다
	unsigned char green = pixel_color & green_mask;
	// blue 값은 출력 하면 32가 나옵니다
	unsigned char blue = pixel_color & blue_mask;

	cout << "green " << bitset<16>(green) << " " << int(green) << endl;

	cout << "blue " << bitset<8>(blue) << " " << int(blue) << endl;

	return 0;
}
```
솔직히 뭘들은건지 모르겠습니다 이부부분은 나중에 쓰게되면 다시 공부해야 할듯합니다ㅠㅠ

## 이번 과정을 마치며

슬슬 난이도가 생기는건지 강사님이 너무 디테일하게 해주시는건지 이해안가는 부분이 생기기 시작 했습니다ㅠㅠ

