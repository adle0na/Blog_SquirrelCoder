<!-- Heading -->
#  아홉번째 도토리

<!-- Quote -->
> ## 이론 정리
> 
> ### 33, 34, 35 강

이번 이론 자료는 Unity C# 이론
NullReferenceException, this 키워드, static 한정
순서로 진행 됩니다 자료 출처는 유튜브 눈코딩 입니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

개인 사정으로 물류 알바를 3주정도 뛰다 왔습니다

다시 취직을 위해 블로그 업로드와 개인 공부를 꾸준히 맘 잡고 해보겠습니다

그리고 썸네일에 노출되는 단어를 수정 해봤습니다

<br>


### 33편 점연산자 NullReferenceException

아무것도 참조하고 있지 않은 참조 변수에서 맴버에 엑세스 하려고 하면 NullReferenceException 오류가 발생 합니다

Exception은 애플리케이션 실행 중에 발생하는 오류를 나타냅니다

참조가 없는 변수의 맴버를 액세스 하려고 했기 때문에

NullReferenceException이 발생 합니다.

###따라해보기

```c#
namespace step33
{
    class Program
    {
        static void Main(string[] args)
        {
            Car car;
            
            car = new Car("싼타페");
            Console.WriteLine(car.name); // 싼타페 출력
            
            car = new Car("쏘렌토");
            Console.WriteLine(car.name); // 쏘렌토 출력
            
            car = null;
            Console.WriteLine(car.name); // Null 오류
        }
    }
}
```
위부분에서 오류가 발생하는 이유는 car 변수에 null을 넣어서가 아니라

null참조 car변수의 맴버 엑세스를 시도 했기 때문에 오류가 발생합니다

<hr>

### 34편 This 키워드

클래스의 현재 인스턴스를 가리키는 키워드 입니다

다음은 this 키워드의 일반적인 사용법입니다

동일한 이름의 매개변수와 맴버변수를 구분합니다
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
맴버 엑세스 연산자를 사용해 맴버에 접근 할 수 있습니다

###따라해보기

이번엔 두 캐릭터가 전투를 한다고 가정 해봅니다

```c#
class Character
{
    public string name;
    public int damage;
    public int hp;
    public int maxHp;
}
```
여기에 캐릭터 생성시 필드 초기화를 위해 생성자 메서드를 정의합니다

```c#
class Character
{
    public string name;
    public int damage;
    public int hp;
    public int maxHp;
    
    Character(string name, int damage, int maxHp)
    {
        this.name = name;
        this.damage = damage;
        this.maxHp = maxHp;
        this.hp = this.maxHp;
    }
 }
```
그 이후 공격하는 기능과 피해를 받는 기능을 메서드로 정의합니다.

```c#
class Character
{
    public string name;
    public int damage;
    public int hp;
    public int maxHp;
    
    public Character(string name, int damage, int maxHp)
    {
        this.name = name;
        this.damage = damage;
        this.maxHp = maxHp;
        this.hp = this.maxHp;
    }
   
    public void Attack(Character target)
    {
        Console.WriteLine("{0}이(가) {1}을(를) 공격합니다. ", this.name, target.name);
        target.Hit(this.damage);
    }
    public void Hit(int damage)
    {
        Console.WriteLine("{0}이(가) {1}만큼 피해를 받았습니다. ", this.name, damage);
        this.hp -= damage;
    }
 }
```

이 후로는 전투를 실행해보는 코드입니다
```c#
namespace Step34
{
    class Program
    {
        static void Main(string[] args)
        {
            Character hong = new Character("홍길동", 3, 10);
            Character lim  = new Character("임꺽정", 2, 12);
            
            Console.WriteLine("name: {0},  damage: {1}, hp: {2}/{3}", hong.name, hong.damage, hong.hp, hong.maxHp);
            Console.WriteLine("name: {0},  damage: {1}, hp: {2}/{3}", lim.name, lim.damage, lim.hp, lim.maxHp);
        }
    }
}
```
이를 실행하면

name: 홍길동, damage: 3, hp: 10/10

name: 임꺽정, damage: 2, hp: 12/12

홍길동이(가) 임꺽정을(를) 공격합니다.

임꺽정이(가) 3만큼 피해를 받았습니다.

로 최종 출력됩니다


### 35편 static 한정자

특정 개체가 아니라 형식 자체에 속하는 정적 맴버를 정의 할 수 있습니다

정적 맴버는 프로그램이 실행되는 동안 수명이 유지 됩니다.

정적 맴버는 항상 클래스 이름으로 엑세스 됩니다

생성된 인스턴스의 수와 상관 없이 정적 맴버는 항상 한 개 만 있습니다

정적 메서드는 비정적 필드 및 메서드에 엑세스 할 수 없습니다

정적 메서드에서 비정적 필드에 접근 할 수 없습니다

![image description](https://imgur.com/QzJktlg.png)


이 때문에 그동안 Main메서드에서 비정적 메서드를 호출 하거나

맴버에 엑세스 하기 위해 static을 붙여 왔던 것입니다

또한 정적 맴버는 클래스 이름으로 엑세스 해야 합니다

![image description](https://imgur.com/PdGsTPe.png)

이제 정적 변수를 정의해봅니다.

변수 타입 앞에 static 한정자를 붙여줍니다

![image description](https://imgur.com/AaxemvB.png)

이후 반환 타입 앞에 static 한정자를 붙여줍니다

정적 생성자는 정적 필드를 초기화 하거나 특정 작업을 한번만 수행 해야 하는데 사용됩니다
![image description](https://imgur.com/Uto7t5y.png)

**정적 생성자는 엑세스 한정자를 사용할 수 없으며 매개변수를 정의할 수 없습니다**


###따라해보기

```c#
namespace Step35
{
    class program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
밑은 자동 완성된 생성자 입니다
```c#
namespace Step35
{
    public class CallCenter
    {
        // 정적 맴버 변수
        public static string number = "1588 - 0000";
        
        // 인스턴스 맴버 변수
        public int extensionNumber; // 내선 번호
    
        // 정적 생성자
        static CallCenter()
        {
            // 정적 생성자에서 정적 필드 (맴버변수) 초기화 가능
            CallCenter.number = "1588-0000";
            Console.WriteLine("콜센터 정적 생성자");
        }
        // 인스턴스 생성자
        public CallCenter(int extensionNumber) // 매개변수로 내선번호 전달
        {
            // this키워드를 사용해 클래스의 현재 인스턴스의 맴버변수에 접근 ( 맴버 엑세스 연산자 사용 .점 연산자)
            this.extensionNumber = extensionNumber;
            
            Console.WriteLine("콜센터 인스턴스 생성자");
            Console.WriteLine("내선번호 : {0}," this.extensionNumber);
        }
        
        // 정적 맴버 메서드
        public static void Call()
        {
            Console.WriteLine("상담 가능한 상담사를 찾고있습니다.");
        }
        
        public void CallExtensionNumber() {
            Console.WriteLine("내선번호 ({0})로 전화를 겁니다.", this.extensionNumber);
            }
    }
}
```
다른 콜센터 인스턴스를 생성하고 다른 변수에 할당 합니다
```c#
namespace Step35
{
    class program
    {
        static void Main(string[] args)
        {
            var center1 = new CallCenter(201);
            var center2 = new CallCenter(202);
            
            Console.WriteLine(CallCenter.number);
            
            // 정적 메서드 호출
            CallCenter.Call();
            
            // 인스턴스 메서드 호출
            center1.CallExtensionNumber(); // 변수에 할당된 CallCenter인스턴스의 맴버 메서드 호출
            center2.CallExtensionNumber();
            
        }
    }
}
```


## 이번장을 마치며

오랫만에 다시 공부를 하니 기초적인것도 기억이 안나 처음부터 차근차근 다시 봐야겠네요