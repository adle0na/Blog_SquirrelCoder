<!-- Heading -->
#  열일곱번째 도토리

<!-- Quote -->
> ## C++ 학습
> 
> ### 입출력과 변수

이번 학습은 유튜브 두들낙서님의 C++ 강의를 참고합니다, [두들낙서](https://www.youtube.com/watch?v=nbkpd0JLoJM&list=PLlJhQXcLQBJqywc5dweQ75GBRubzPxhAk)
를 참고합니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

취업 후 둘째날입니다

유니티로 입사했지만 어쩌다보니 언리얼부터 다루게 되어

C++를 배우고자 합니다 C#도 완벽히 마스터 못한 상태에서 시작하는거라 불안하지만

걱정 부터 앞서면 아무것도 못하죠! 바로 시작합니다

<br>

### 섹션1 종합 문제

섹션1 입출력과 변수는 기초적인 내용으로 시간관계상 종합문제만 체크하고 넘어가려고 합니다

문제 1. 두 숫자를 입력받아서 그 숫자드르이 합을 출력하는 프로그램을 만들어 봅니다

```c++
#include <stdio.h>

int main()
{
    // 변수 두개 정의
    int a, b;
    // 입력 받을 값 두가지 ""안의 값 출력, d안에 들어갈 값 &로 주소설정하여 a, b 설정 
    scanf("%d%d", &a, &b);
    // 합한 변수 값 출력
    printf("%d\n", a + b);
}
```

여기 코드를 치는것은 어렵지 않으나 직접 Visual studio에 디버그를 하려고하니

가장 기본적인 scanf 구문에서 오류가 발생했습니다

버전이 달라지면서 scanf 함수에 보안문제를 제기하는데

_CRT_SECURE_NO_WARNINGS 구문을 전처리기에 입력함으로써 오류를 해결했습니다

문제 2. 체중과 키를 입력받아서 체질량 지수를 구하는 프로그램을 만들어 봅니다

```c++
#include <stdio.h>

int main()
{
    float height, weight;

    printf("체중을 입력하세요(kg) : ");
    scanf("%f", &weight);
    printf("키를 입력하세요(cm) : ");
    scanf("%f", &height);

    float bmi = (weight / (height * height)) * 10000;

    printf("BMI : %.1f\n", bmi);
}
```
여러가지 시행착오로 인해 키의 단위를 cm로 입력 받아도 bmi 계산의 결과값을

정상적으로 받을 수 있게 되었습니다

문제 3. 알파벳을 입력받아서 그 다음 알파벳을 출력하는 프로그램을 만들어 보세요

```c++
#include <stdio.h>

int main()
{
	 char alpha;

	 scanf("%c", &alpha);

	 char nextalpha = alpha + 1;

	 printf("%c", nextalpha);
}
```
대학교때 했던 C언어 기본 문법에 대해 다시 복습한 기분이었습니다

시간이 없으니 바로 다음 학습으로 넘어가도록 합니다

### 섹션2 종합문제

2부 연산자와 제어문 부분도 문제를 풀며 빠르게 넘어가보도록 하겠습니다

문제1. 시험 점수따라 등급나누기
```c++
#include <stdio.h>

int main()
{
	int score;

	scanf("%d", &score);
	
	if ( score >= 90 )
		printf("A 등급");
	else if (score < 90 && score >= 80)
		printf("B 등급");
	else if (score < 80 && score >= 70)
		printf("C 등급");
	else if (score < 70 && score >= 60)
		printf("D 등급");
	else
		printf("E 등급");
}
```
최대한 간결하게 적어봤지만 뭔가 맘에들지 않습니다 일단 복습하는 단계이니 이정도로 넘어갑니다

문제2. 자연수를 입력받아 그 수의 약수를 출력

```c++
#include <stdio.h>

int main()
{
	int number;

	scanf("%d", &number);
	
	for (int i = 1; i <= number; i++)
	{
		if (number % i == 0)
		{
			printf("%d, ", i);
		}
	}
}
```
제머리로는 이문제를 못풀었습니다 그래도 답을보니 이해가 됐습니다

for문으로 반복하여 인수를 1부터 체크하고

입력받은 숫자를 1부터 하나씩 나눠보며 그 숫자의 나머지가 0일 경우가

그 숫자의 약수라는 뜻이므로 그때만 조건문으로 출력을 해줍니다

문제3. 숫자를 입력받아 그수까지 반복 출력하는데 일의자리가 3, 6, 9 라면 *로 출력

```c++
#include <stdio.h>

int main()
{
	int number;

	scanf("%d", &number);
	
	for (int i = 1; i <= number; i++)
	{
		int oneNumber = i % 10;

		if (oneNumber == 3 || oneNumber == 6 || oneNumber == 9)
			printf("* ");
		else
			printf("%d ", i);
	}
}
```
이번에도 for문 활용까진 도달했지만 1의 자리수만 어떻게 사용할지를 고민했지만 실패했습니다

정답은 인수를 10으로 나눈 나머지 값을 확인하는 것이었고

그값이 3, 6, 9 일때만 *로 출력하고 그렇지 않은 경우엔 그대로 인수를 입력받은 수까지 반복하여

출력하면 원하는 정답이 나옵니다

문제3. 숫자를 입력받아 그수를 자리수로하여 홀수를 반복 출력

```c++
#include <stdio.h>

int main()
{
	int number;

	scanf("%d", &number);
	
	for (int i = 1; i <= number; i++)
	{
		for (int k = 1; k <= i; k++)
		{
			printf("%d ", 2 * k - 1);
		}
		printf("\n");
	}
}
```

이번에도 이중 for문인것까진 예측을 했지만 2n-1의 개념을 떠올리지 못했습니다

1을 어떻게 하면 출력할까 고민했는데 저런 방법이 있었네요

우선 수학적인 문제는 천천히 극복 해보도록하고 코드에 집중하겠습니다

### 섹션3 배열과 포인터

**20강 배열**

드디어 어렵다는 포인터를 배울 차례입니다

먼저 배열 개념을 빠르게 학습하고 포인터를 배워보도록 합니다

int a[i]; 를 입력하면 i를 인수로 가지는 배열 a를 생성합니다

배열 안에는 주소를 가지고 변수들이 들어갑니다

기본적인 구조를 보면

```c++
#include <stdio.h>

int main()
{
    // arr[?] ?는 배열의 길이인데 현재 5로 되어있지만 안적어도 알아서 인식한다
    int arr[5] = { 3, 1, 4, 1, 5 };
    
    for ( int i = 0; i <= 4; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\n");
}
```

추가로 sizeof(arr) 이런식으로 쓰면 배열의 길이 값을 반환한다

**21강 배열을 활용해보자**

```c++
#include <stdio.h>

int main()
{
    int n;
    int arr[100];
    
    printf("입력할 숫자의 개수 입력 : ");
    // 배열 크기를 입력합니다
    scanf("%d", &n);
    // i 0부터 시작해서 n보다 작은 동안만 반복, ++
    for (int i = 0; i < n; i++)
    {
        // 배열 인수를 입력 받습니다
        scanf("%d", &arr[i]);
    }
}
```

```c++
#include <stdio.h>

int main()
{
    int n;
    int arr[100];
    
    printf("입력할 숫자의 개수 입력 : ");
    scanf("%d", &n);
    for(int i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    
    // 최대값은 값 1칸의 배열
    int max = arr[0];
    // 최대값 체크 n 값 하나씩 올려가며
    for (int i = 1; i < n; i++)
    {
        // 최대값 체크가 끝나면 최대값 변수에 해당 배열 값 삽입
        if(max < arr[i]) max = arr[i];
    }
    
    // 계산이 끝난 최대값 출력
    printf("%d\n", max);
    
}

```

**22강 2차원 배열**

```c++
#include <stdio.h>

int main()
{
    int arr[3][4] =
    {
        {1, 2, 3, 4}
        {5, 6, 7, 8}
        {9, 10, 11, 12}
    }
}
```

```c++
#include <stdio.h>

int main()
{
	int p[10][10];

	// i 0부터 9까지 반복
	for (int i = 0; i < 10; i++)
	{
		// j 도 같은 작업
		for (int j = 0; j <= i; j++)
		{
			if (j == 0 || j == i)
			{
				p[i][j] = 1;
			}
			else
			{
				p[i][j] = p[i - 1][j - 1] + p[i - 1][j];
			}
			printf("%d ", p[i][j]);
		}
		printf("\n");
	}
}
```

**23강 문자열**




## 이번 과정을 마치며

새로운 협업 방식인 SVN을 배웠습니다

이제 누군가 SVN 써봤어요? 라고 물어본다면 녜???? 하고 얼타지 않을 수 있습니다

