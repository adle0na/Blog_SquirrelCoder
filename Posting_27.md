<!-- Heading -->
#  스물다섯번째 도토리

<!-- Quote -->
> ## [C#과 유니티로 만드는 MMORPG 게임 개발 시리즈] Part2: 자료구조와 알고리즘
>
> ### 섹션1 선형 자료 기초

Rookis님의 인프런 유료 강의를 들으며 작성한 글입니다.

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

다니던 회사가 폐업을 하게되어 자유의 몸이 되었습니다!

실업급여 기간 동안 이직 준비와 그동안 못들었던 강의를 들으며 해보고 싶었던 기능들을

구현할 예정입니다. 블로그 업로드 빈도가 드디어 좀 생기겠네요

<br>

## 배열, 동적 배열, 연결 리스트

이전 강의들과 여기까지 수강은 했는데 출퇴근길에 들어서 동적 배열 구현 연습부터 작성합니다!

## 동적 배열 구현 연습

C++ 에서는 Vector를 사용하지만 C#에서는 List(동적 배열) 혹은 LinkedList(연결 리스트)를 사용합니다

기능을 비교해보면 LinkedList는 중간 삽입 작업이 용이 하다고 합니다.

동적 배열이 같는 장점은 배열 사이즈를 유동적으로 늘리거나 줄일 수 있습니다.

근데 예를들어 맵사이즈 같은 경우엔 변화가 거의 없으니 기본형태인 배열이 합리적입니다.

~~(기초가 없는 저는 그냥 그런거 모르고 다 List썼습니다...)~~

동적 배열이나 연결 리스트를 사용할땐 우선 먼저 초기화를 고려 합니다.

class Board
{
    public int[] _data = new int[25]; // 배열
    public List<int> _data2 = new List<int>(); // 동적 배열
    public LinkedList<int> _data3 = new LinkedList<int>(); // 연결 리스트

    public void Initialize()
    {
        _data2.Add(101);
        _data2.Add(102);
        _data2.Add(103);
        _data2.Add(104);

        int temp = _data2[2];
    }
}

아주 기초적인 내용인데 우선 리스트는 0부터 시작하기 때문에 _data2 리스트의 index가 2인 값은 103이 됩니다.

값을 넣어봤으니 빼는것도 해봅니다

class Board
{
    public int[] _data = new int[25]; // 배열
    public List<int> _data2 = new List<int>(); // 동적 배열
    public LinkedList<int> _data3 = new LinkedList<int>(); // 연결 리스트

    public void Initialize()
    {
        _data2.Add(101);
        _data2.Add(102);
        _data2.Add(103);
        _data2.Add(104);

        int temp = _data2[2];

        _data2.RemoveAt(2);
    }
}

이번에도 마찬가지로 예를들어 List에 RemoveAt(2)을 사용하게되면 index가 2이므로

3번째 데이터가 사라지게 됩니다.

빠른 이해를 위해 다른 동적 배열을 구현 해봅니다.

class MyList<T>
{
    const int DEFAULT_SIZE = 1;

    T[] _data = newT[1];

    public int Count = 0; // 실제로 사용중인 데이터 개수
    public int Capacity {get {return _data.Length;}} // 예약된 데이터 개수
}

지금은 _data 배열의 크기와 Capacity 값이 같도록 해준다

이코드에서 _data 배열에 데이터를 추가하는 것은 매우 번거롭다.

class MyList<T>
{
    const int DEFAULT_SIZE = 1;
    T[] _data = newT[DEFAULT_SIZE];

    public int Count = 0; // 실제로 사용중인 데이터 개수
    public int Capacity {get {return _data.Length;}} // 예약된 데이터 개수

    public void Add(T item)
    {
        // 먼저 배열에 공간이 남아 있는지 확인
        if(Count >= Capacity)
        {
            // 배열의 크기를 늘려서 공간 확보
            T[] newArray = new T[Count * 2];

            // 기존 데이터를 
            for(int i = 0; i < Count; i++>)
                newArray[i] = _data[i];

            _data = newAAray
        }
        
        // 확보된 공간에 데이터를 넣어준다
        _data[Count] = item;
        Count++;
    }
}

아니 그동안 편하게 List만 주구장창 써온 이유가 있었네요 일반 배열은 동적 배열인 List와

다르게 정적이기 때문에 배열의 크기를 조절하게 될경우 굉장히 번거로운 과정을 거칩니다.

### 갑자기 생긴 궁금증

저는 멍청해서 지금까지 그냥 다 List를 사용했는데 그렇다면 저렇게 번거로운 일반 배열을

사용해야 할때는 언제고 장점은 무엇일까? 빠른 답을 얻기 위해 GPT에게 물어봤습니다.

메모리 사용량: 일반 배열은 List에 비해 적은 메모리를 사용합니다. List는 내부적으로 배열을 기반으로 하지만, 더 많은 메타데이터를 관리하기 위해 추가 메모리를 사용합니다.

속도: 일반 배열은 List에 비해 더 빠릅니다. List는 요소를 추가하거나 제거할 때 동적으로 크기를 조절하고 복사해야 할 수 있으므로, 배열보다 느릴 수 있습니다.

크기 변경: 배열은 한 번 생성되면 크기를 변경할 수 없지만, List는 동적으로 크기를 조절할 수 있습니다. 따라서 크기가 변경되는 작업이 자주 발생하지 않는 경우에는 배열을 사용하는 것이 더 효율적입니다.

가독성: 배열은 간단하고 직관적입니다. List는 여러 가지 메서드를 제공하여 요소를 추가, 제거, 정렬 및 검색하는 등의 작업을 보다 쉽게 할 수 있습니다. 따라서 코드의 목적과 요구 사항에 따라 가독성을 고려하여 선택해야 합니다.

음 자세히 알려줬는데 제가 간단히 이해한 내용은 배열의 크기 조절을 할일이 없는 경우

메모리 사용량, 속도에서 이득을 보기 위해 사용하네요

~~(그치만 요즘 컴퓨터는 너무 성능이 좋아서 List 다 때려박아도 잘 돌아갔었군요)~~

그리고 간단한 팁이지만 정적 배열에서 값을 관리할때

public T this[int index]
{
    get { return _data[index];}
    Set { _data[index] = value}
}

이런식으로 하면 get으로는 this[] 안에 인덱스 번호만 넣으면 해당하는 값을 리턴 받고

set으로는 해당하는 인덱스의 값을 value로 지정할 수 있네요

~~(이거랑 완전 같진 않지만 List충인 저는 그냥 List[i]값 디버그로 봤어요)~~

정적 배열에서 값을 빼줄때는

public void RemoveAt(int index)
{
    // 해당하는 인덱스의 값의 뒤에 값들을 한칸씩 땡긴 후
    for(int i = 0; index; i < Count - 1; i++)
        _data[i] = _data[Count + 1];

    // 맨끝의 값을 default값으로 대체합니다
    _data[Count - 1] = default(T);

    Count--;
}

근데 이 코드의 결과가 101 102 103 104 105 가 정적 배열로 있을때

103을 빼게 되면 결국 101 102 104 105 0 이런식으로 되는데

동적 배열인 List쓸때는 그냥 쏙 빼버리고 사이즈도 줄었었죠

~~(역시 감사할줄 아는것도 그 이유를 알아야 하네요 새삼 고맙다 List야...)~~

자 이번엔 방금 사용했던 정적배열을 관리하는 기능들을 동적배열에서도 똑같은 기능을 구현 해봅니다.

동적 배열에서 값 지정할때

int temp = _data2[2]; ~~(딸깍)~~

동적 배열에서 값 제거할때

int temp = _data2.RemoveAt(2); ~~(딸깍)~~

그리고 정적 배열의 시간 복잡도 보면

당연하게도 정적배열은 대부분 0(1) (방금 사용했던 코드는 예외)

for문을 한바퀴 사용하는 정적배열의 RemoveAt은 0(N) 의 시간복잡도를 가집니다.

### 갑자기 생긴 궁금증

위에서 딸깍 했던 리스트의 시간 복잡도는 안알려주셔서 찾아봤습니다.

List의 값을 수정하는 코드는 정적 배열과 마찬가지로 0(1) 이었고

List의 값을 제거하는 코드도 정적 배열고 마찬가지로 0(N) 이었습니다.

~~(이래서 그동안 그냥 List 때려박아도 문제 없었나..?)~~

## 연결 리스트 구현 연습

이번엔 앞서 언급했던 LinkedList를 다뤄봅니다.

class Room<T>
{
    public T Data;
    public Room<T> Next;
    public Room<T> Prev;
}

class RoomList<T>
{
    public Room<T> Head;
    public Room<T> Tail;
    public int Count = 0;

    public Room<T> AddLast(T data)
    {
        Room<T> newRoom = new Room<T>();
        newRoom.Data = data;

        // 만약 아직 방이 아예 없다면 새로 추가한 방을 첫번째 방으로 지정
        if(Head == null)
            Head = newRoom;

        // 기존의 마지막 방과 새로 추가되는 방을 연결
        if(Tail != null)
        {
            Tail.Next = newRoom;
            newRoom.Prev = Tail;
        }

        // 새로 추가되는 방을 마지막 방으로 지정
        Tail = newRoom;
        Count++;
        return newRoom;
    }

    public void Remove(Room<T> room)
    {
        // 기존의 첫번째 방의 다음방을 첫번째 방으로 지정 ex) 2 => 1
        if(Head == room)
            Head = Head.Next;

        // 기존의 마지막 이전의 방을 마지막 방으로 지정 ex) 끝번호 - 1 => 끝번호
        if(Tail == room)
            Tail = Tail.Prev;

        if(room.Prev != null)
            room.Prev.Next = room.Next;

        if(room.Next != null)
            room.Next.Prev = room.Prev;
    }
}

class Board
{
    public int[] _data = new int[25]; // 정적 배열
    public LinkedList<int> _data3 = new LinkedList<int>(); // 연결 리스트

    public void Initialize()
    {
        _data3.AddLast(101);
        _data3.AddLast(102);
        LinkedListNode<int> node = _data3.AddLast(103);
        _data3.AddLast(103);
        _data3.AddLast(104);

        _data3.Remove(node);
    }
}

코드를 보면 기존 Add가 아닌 AddLast를 쓰게되며

중간에는 node 라는걸 사용해서 관리를 하고 있는데

이는 LinkedList는 기존 배열과는 조금 다른 주소값으로 관리하고

쭉 이어주는 느낌이라서 처음 값과 끝 값을 항상 알고 있어야 한다

어딘가 끊어지면 그 값의 양옆을 연결 해주는 느낌이다.

### 갑자기 생긴 궁금증

LinkedList는 써본적이 없는데 언제 왜 쓰고 장단점이 무엇일까?

GPT에게 물어보니

LinkedList:

LinkedList는 각 요소가 자신의 이전 요소와 다음 요소를 가리키는 노드로 구성됩니다.
임의의 위치에서 요소의 삽입 및 삭제가 빠릅니다(O(1)).
인덱스 접근이 불가능하며 요소를 찾기 위해서는 리스트를 순회해야 합니다.
각 요소가 추가적인 포인터를 가지고 있어 메모리 사용량이 더 많습니다.
요소의 삽입 및 삭제가 빈번하고, 순회가 자주 필요하지 않은 경우에 적합합니다.

한번더 정리하면 주소 개념이기에 인덱스 접근이 불가능하고 그렇기 때문에

리스트를 순회해야 하는 단점이 있지만 하나의 요소를 직접 지정하여 삽입 삭제하는데

쓰인다고 합니다.

## 이번 과정을 마치며

이번에도 당연하게 써오던 것들이 왜 어떻게 편한지 알게 됐고 LinkedList는...

한번도 안써봤는데 나중에 삽입 삭제만 사용하는 배열을 사용할때 써봐야 겠습니다.