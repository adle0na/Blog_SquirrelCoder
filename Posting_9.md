
<!-- Heading -->
#  여덟번째 도토리

<!-- Quote -->
> ## 이론 정리
> 
> ### 33, 34, 35, 36, 37, 38 강
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

<br>.

바로 들어갑니다

<hr>
<!-- Numbered list -->

##33 점연산자, NullReferenceException

```c#
car.name
car.Move();
```
이와 같이 . 을 사용하여 형식 멤버에 액세스합니다

아무것도 참조하고 있지 않은 참조 변수에서 맴버에 액세스하려고 하면

NullReferenceException 오류가 발생합니다

그중 Exception 애플리케이션 실행 중에 발생하는 오류를 나타냅니다

```c#
class Program
{
    static void Main(string[] args)
    {
        // Car 인스턴스 생성후 문자열값을 생성자 매개변수로 전달 합니다
        Car car = new Car("캐스퍼");
        Debug.Log(car.name);
        
        car = null; // 이경우 Car클래스의 맴버변수 name이 기본값으로 초기화 됩니다
        Debug.Log(car.name);
    }
}
```
이경우 참조가 없는 변수의 맴버를 액세스 하려고 했기 때문에 NullReferenceExeption이 발생
```c#
class Program
{
    static void Main(string[] args)
    {
        Car car;
        
        car = new Car("캐스퍼");
        Debug.Log(car.name);
        car = new Car("테슬라");
        Debug.Log(car.name);
        // 이전에 만든 Car인스턴스는 참조가 없음으로 GC에 의해 메모리에서 해제 됩니다
        
        
```

<hr>

## 34편 this 키워드

클래스의 현재 인스턴스를 가리키는 키워드 입니다

this 키워드의 일반적인 사용방법

동일한 이름의 매개변수와 맴버변수를 구분합니다

맴버 엑세스 연산자를 사용해 맴버에 접근 할 수 있습니다
```c#
class Car
{
    string name;
    
    public Car(string name)
    {
        this.name = name;
    }
}
```
인스턴스를 다른 메서드에 매개변수로 전달 할 수 있습니다

예시로 두캐릭터가 전투를 하는 상황이라면

캐릭터 클래스를 지정하고 맴버변수로 이름과 공격력 그리고 체력을 정의합니다
```c#
class Character
{
    // 맴버변수 정의
    public string name;
    public int damage;
    public int hp;
    public int maxHp;
    
    // 생성자
    Character(string name, int damage, int maxHp)
    {
        //맴버 변수 초기화
        this.name = name;
        this.damage = damage;
        this.maxHP = maxHp;
        this.hp = this.maxHp;
    }
    // 공격하다
    public void Attack(Character target)
    {
        target.Hit(this.damage);
        Debug.Log("{0}이(가) {1}을(를) 공격합니다. ", this.name, target.name);
    }
    // 피해를 받다
    public void Hit(int damage)
    {
        this.hp -= damage;
        Debug.Log("{0}이(가) {1}만큼 피해를 받았습니다.", this.name, damage);
    }
}
```
공격하는 기능과 피해를 받는 기능을 메서드로 정의합니다

그리고 다음은 프로그램 클래스입니다
```c#
class Program
{
    static void Main(string[] args)
    {
        Character cat = new Character("고양이", 3, 10);
        character dog = new Character("강아지", 2, 12);
        
        Debug.Log("name: {0}, damage: {1}, hp: {2}/{3}", cat.name, cat,damage, cat.maxHp);
        Debug.Log("name: {0}, damage: {1}, hp: {2}/{3}", dog.name, dog,damage, dog.maxHp);
        
        cat.Attack(dog);
        // 공격이 끝나고 체력을 다시 호출합니다
        Debug.Log("name: {0}, damage: {1}, hp: {2}/{3}", dog.name, dog,damage, dog.maxHp);
    }
}
```
출력값은

name: 고양이, damage: 3, hp: 10/10

name: 강아지, damage: 2, hp: 12/12

고양이 이(가) 강아지 을(를) 공격합니다

강아지 이(가) 3만큼 피해를 받았습니다

name: 강아지, damage: 2, hp: 9/12

<hr>

##35 static 한정자

정적 맴버는 프로그램이 실행되는 동안 수명이 유지됩니다

정적 맴버는 항상 클래스 이름으로 엑세스 됩니다 생성된 인스턴스의 수와 상관 없이 정적 맴버는 항상 한개만 있습니다

정적 메서드는 비정적 필드 및 메서드에 엑세스 할 수 없습니다

코드예시
```c#
class Program
{
    int a;
    
    static void Main(string[] args)
    {
        a = 10; // 여기에 오류가 발생합니다
    }
}
```
또한 정적 메서드에서 비정적 메서드에 접근 할 수 없습니다

코드예시
```c#
class Program
{
    static void Main(string[] args)
    {
        Test(); // 이부분에 오류가 발생합니다
    }
    
    void Test()
    {
    
    }
}
```
이때문에

<hr>

##30편 클래스와 new 연산자

클래스는 객체를 생성하기 위해 변수와 메서드를 정의하는 틀 입니다

객체는 클래스로부터 생성된 메모리에 저장된 값을 의미합니다

객체는 고유한 속성을 가지며 클래스에서 정의한 기능을 수행할 수 있습니다

자동차 클래스를 정의하고 다양한 자동차 객체들을 생성해봅시다

클래스를 정의하는 방법입니다

```c#
class car
{
    public string name; // 속성, 필드, 맴버 변수
    
    void MoveForward() // 맴버 메서드
    {
        Debug.Log("{0}가 전진 합니다.", name);
    }
    // 맴버변수와 맴버 메서드를 합쳐 맴버라고 부릅니다
}
```
이렇게 생성된 클래스는 다른 클래스에서 호출가능합니다
```c#
class Program
{
    static void Main(string[] args)
    {
        // Car 인스턴스를 담는 변수 선언 후
        Car car;
        /// 변수에 값을 할당합니다 ( "=" 연산자는 오른쪽 값을 왼쪽 변수에 할당합니다)  
        /// 객체를 만들고 싶다면 new 키워드를 사용한다
        car = new Car();
        car.name = "캐스퍼";
        car.MoveForward();
        Debug.Log(car.name);
        
        // 그리고 새로운 Car객체도 생성해봅니다
        Car car2 = new Car();
        car2.name = "테슬라";
        car2.MoveForward();
        Debug.Log(car2.name);
    }
}
```
클래스로 부터 생성된 인스턴스 (객체)는 독립적입니다

생성된 객체는 **값** 이며 이 값을 인스턴스라 부른다

이것만 알아두세요 타임!

### 클래스는 사용자의 정의형식 

<hr>

##31편 생성자 메서드

class내부에 정의된 특수한 메서드

생성자는 이름이 해당 형식의 이름과 동일한 메서드입니다

메서드 이름과 매개 변수 목록만 포함되고 반환 형식은 포함되지 않습니다

일반 메서드는 정의 후 호출을 통해 실행됩니다

생성자 메서드는 객체 생성시 자동으로 호출 됩니다

생성자를 통해 맴버변수의 기본값을 설정 할 수 있습니다

매개변수가 있는 생성자

객체 생성시 값을 전달 할 수 있습니다

예를 들어 자동차 객체를 생성할 때 자동차 이름을 전달 할 수 있습니다

매개변수가 있는 생성자 메서드의 정의
```c#
class Car
{
    // 맴버 변수
    public string name;
    /// carName을 매개변수로 사용중
    /// 접근제한자를 적지 않으면 기본은 private 상태이므로 public을 지정해줍니다
    public Car(string carName)
    {
        name = carName;
    }
}
```
이렇게 하고 생성된 자동차 객체의 이름을 출력해보면
```c#
Car car = new Car("아이오닉");
Debug.Log(car.name);
```
아이오닉이 잘 출력됩니다

그리고 이것만 기억하세요 타임!

### 생성자는 클래스안에 정의된 특수한 메서드이다
### 반환 타입이 없으며 이름이 클래스명과 동일한 메서드이다
### 인스턴스가 생성된후 자동으로 호출된다
### 매개변수가 있는 생성자도 있다

~~(이번강의는 이것만 기억하세요가 좀 많네요;;)~~

<hr>
<!-- Numbered list -->

## 32편 맴버변수와 지역변수

맴버 변수 : 클래스에 정의된 변수

맴버 변수는 인스턴스가 메모리에 있는 동안 접근 가능합니다

지역변수 : 메서드에 정의된 변수

매개변수는 메서드에 정의된 변수이므로 지역 변수입니다

지역 변수는 메서드가 실행 되는 동안 접근 가능합니다

메서드가 호출되면 지역 변수들은 스택 메모리에 할당 됩니다

메서드 호출이 완료되면 지역 변수들은 스택 메모리에서 해제됩니다

생성된 인스턴스는 힙 메모리에 할당되며 맴버변수를 포함 합니다

인스턴스에 대한 참조가 없다면 가비지 컬렉터(GC)에 의해 자동 해제 됩니다

+ 가비지 컬렉션 : 메모리를 자동으로 관리해주는 메커니즘

Car car = new car();일때

변수 car는 힙 메모리에 있는 값의 주소를 참조합니다

Car car = null

null값은 당연히 참조 하지 않음을 의미합니다

## 오늘 정리를 마치며

이론이 역시나 지루하기 때문에 다른 예제 학습과 병행하는게 효율이 확실히 좋네요

현재 기준 59강이 끝인데 계속해서 작성해보겠습니다~