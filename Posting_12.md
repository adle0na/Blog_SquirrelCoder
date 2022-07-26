<!-- Heading -->
#  열번째 도토리

<!-- Quote -->
> ## 기초 복습
> 
> ### 고박사 유니티 입문 기초편 (1/3)

이번 강의 내용은 유튜브 고박사님의 인프런 무료 강의 유니티 기초 자료입니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

3주 일하고 오니 제일 중요한 기본적인 부분들이 헷깔려서 확실하게

제일 중요한 기초 탄탄하게 다지고 시작할려고 합니다

<br>


### 유니티 기초

이 장은 유니티 엔진 설치, 기본적인 에디터 인터페이스, 게임 오브젝트와 컴포넌트, 스크립트 개요

그리고 콘솔 뷰에 데이터 출력하기 까지 마지막으로 유니티 이벤트 함수에 대해 다룹니다

**유니티 엔진 설치**

이 파트는 일단 넘어가겠습니다 제가 설치하는것 에서 문제를 느꼈던 적은 없어서요

**유니티 에디터 인터페이스**

툴바 인터페이스
![image description](https://imgur.com/8rfEOoN.png)

씬뷰에서 조작법
![image description](https://imgur.com/s35gVyc.png)

Hierarchy창에서는 계층 구조로 부모 자식의 구조를 설정할 수 있음

프로젝트 뷰에서 사용 가능한 확장자의 종류
![image description](https://imgur.com/kTSdKtv.png)

콘솔뷰는 필요한 정보의 출력이나 빌드되기전 에디터상에서 확인용으로 쓰인다

<br>

**게임오브젝트, 컴포넌트**

씬에 관하여 정리한 내용
![image description](https://imgur.com/iZLoIRI.png)

게임 오브젝트와 컴포넌트는 묶어서 설명 합니다

2D일땐 Sprite Renderer 컴포넌트 3D일땐 Mesh Renderer 컴포넌트 를 각각 사용하여 화면에 출력합니다

Audio Source 컴포넌트 : AudioClip 변수에 등록된 사운드 에셋을 재생 합니다

변수에 바로 넣어두면 시작하자 마자 재생하게 됩니다

그리고 행동의 조건과 컨트롤은 직접 제작하게 될 C#스크립트 파일을 통해 실행 됩니다

![image description](https://imgur.com/9b8Cbd0.png)

에셋은 프로젝트 내부에서 사용하는 모든 리소스를 지칭하는 단위입니다

(Audio, 3D Model, Animation, Texture, Script, Prefab, Etc...)

다음은 프리팹입니다 자세한 내용은 다른 강의에서 살펴보도록 합니다

![image description](https://imgur.com/pnsnvS7.png)

그리고 계속해서 Project, Scene, GameObject, Component, Asset의 관계에 대해 설명 해 주십니다

그 이후로 Unity 3D 좌표체계로 넘어가는데 Unity3D는 왼손 좌표계를 사용합니다

3D와 2D의 기초 구성, Effect와 Audio등을 간단하게 소개하고 넘어갑니다

다음은 Camera & Light입니다

Camera컴포넌트는 게임월드를 보는 우리의 눈역할을 하며

Audio Listener 컴포넌트는 소리를 듣는 귀역할을 하게됩니다

Camera컴포넌트의 세부 내용으로 들어가면

Clear Flags가 있는데

오브젝트가 존재하지 않는 빈 배경을 어떻게 채울지 결정하며

2D 게임은 Solid Color, 3D 게임은 Skybox를 사용합니다
"
Background는 Clear Flags가 "Solid Color"일 때 배경화면의 색상을 나타내는 변수입니다

만약 Clear Flags가 Depth only나 Don't Clear 상태일 경우

오브젝트가 움직일때마다 잔상이 남게 됩니다

그리고 Camera 옵션중 Projection이 Othgraphic이면 2D 느낌 Perspective면 3D 느낌이 납니다

Clipping Planes

![image description](https://imgur.com/MWNKCw9.png)

Viewport Rect를 x, y (0,0), w, h (0.5, 1)로 절반만 값을 주면

카메라가 본것을 그리고 나머지 절반은 그려지는 것이 없기 때문에 검정 화면이 절반 출력된다

Light

현실에서의 빛 역할을 하게 된다

추가 팁 - 완벽한 암흑 공간을 만들고 싶을 경우

![image description](https://imgur.com/7eGBhDl.png)

<br>

Light의 Type 종류

Directional Light - 모든 오브젝트에게 동일한 방향으로 빛을 제공

Point Light - 구 형태로 방사되는 빛, 전구, 모닥불등으로 쓰인다

Spot Light - 변수에 설정된 값만큼 원뿔 형태로 퍼져나가는 빛, 오브젝트 강조나 가로등 같은 곳에 쓰인다

Area Light - 오브젝트의 위치를 기준 전방 방향으로만 방출된다, Baked모드에서만 사용 가능하다

카메라가 Baked 모드일때 오브젝트의 static 옵션을 Contribute GI로 해주어야하며

Window -> Randering -> Lighting Settings에서 "Generate Lighting"으로 빛 데이터 Baked하기

<br>

카메라의 Mode

![image description](https://imgur.com/HVHADdM.png)

그외에도 Intensity와 Shadow Type등이 있으며

Cookie & Cookie Size 기능은

빛의 모양을 원하는 Texture 모양, Size의 빛을 생성합니다

<br>

2D 게임 오브젝트와, 3D 게임 오브젝트 내용은

Sprite 이미지 제작과 3차원 Cube, Sphere 오브젝트를 다루는 내용이라 넘어가겠습니다

<br>

**스크립트 개요, 콘솔 뷰에 데이터 출력**

유니티에서 사용하는 C# 스크립트의 역할은

스크립트가 컴포넌트로 종속된 게임 오브젝트에 주어지는 각종 명령을 제어합니다

게임 내에서 사용되는 여러 오브젝트들을 생성, 삭제 및 관리합니다

게임 전체 또는 일부를 관리하는 게임 내 시스템 구현입니다

기본적인 스크립트 구조는

맨위에 Namespace들을 나타낸 Using 공간이 있고

그 아래 클래스 이름과 부모 클래스를 정의하고

그리고 중괄호 안쪽에 클래스의 내용을 작성하게 됩니다

클래스는 컴포넌트를 나타내는 단위이기도 하며 각종 기능을 작동하는 공간입니다

MonoBehaviour는 유니티에서 기본적으로 제공되는 클래스입니다

그 이후로는 들여쓰기, 주석, 디버깅 출력 등의 기초를 알려 주셨습니다

+ Hierarchy View에 있는 게임오브젝트(컴포넌트)를 수정할 때는 플레이를 반드시 종료 할것

<br>

**이벤트 함수**

조건에 따라 자동으로 실행되는 함수이며 이번 강의에서 다루는 이벤트 함수는 다음과 같습니다

초기화를 위한 이벤트 함수 : Awake(), Start(), OnEnable()

업데이트를 위한 이벤트 함수 : Update(), LateUpdate(), FixedUpdate()

오브젝트 파괴를 위한 이벤트 함수 : OnDestroy()

종료를 위한 이벤트 함수 : OnApplicationQuit(), OnDisable()

~~(다 아는 것들이군요)~~

빈 오브젝트를 생성하고 테스트용으로 생성한 스크립트를 넣습니다

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EventFunctionsTest : MonoBehavior
{
    private void Awake( // 여기에 들어가는건 매개 변수 )
    {
        Debug.Log("Awake 함수가 실행 되었습니다.");
    }
}
```
처음에 생성하고 나면 Start()와 Update()가 있는데 싹 지우고 시작합니다

Awake() 함수는 게임오브젝트가 활성화 되어 있을 때 1회 호출 됩니다

(컴포넌트가 비활성화 상태여도 게임 오브젝트가 활성화 되어 있으면 호출 된다)

데이터를 초기화 하는 용도로 사용됩니다

<br>

Start() 함수는 현재 씬에서 게임오브젝트와 컴포넌트가 모두 활성화 되어 있을때 1회 호출되며

마찬가지로 데이터를 초기화 하는 용도로 사용됩니다

추가로 다른점은 첫번째 업데이트 함수가 실행되기 직전에 호출됩니다

초기화 함수 호출 순서 Awake() -> OnEnable() -> Start()

<br>

OnEnable 함수는 컴포넌트가 비활성화 되었다가 활성화 될 때 마다 1회 호출됩니다

다음으로는 Update() 이벤트 함수의 종류입니다

Update() 함수는 씬이 실행되면 컴포넌트가 활성화 된 동안 매 프레임마다 호출 됩니다

(FPS 60은 Update함수가 1초에 60번 호출된다는 뜻)

<br>

LateUpdate() 함수는 현재 씬에 존재하는 모든 게임 오브젝트의 Update() 함수가 1회 실행된 후에 실행됩니다

업데이트 함수의 호출순서 Update() -> LateUpdate()

<br>

FixedUpdate() 함수는 프레임의 영향을 받지 않고 일정한 간격으로 호출됩니다

Edit -> Project Settings - Time 옵션의 Fixed Timestep 변수로 조절 가능합니다

(기본 값은 0.02로 0.02초에 1번 호출된다는 뜻으로 1초에 50번이다)

<br>

OnDestroy() 함수는 게임오브젝트가 파괴될 때 1회 호출되며

씬이 변경되거나 게임이 종료될 때에도 오브젝트가 파괴되기 때문에 호출됩니다

<br>

다음으로는 OnApplicationQuit() 함수는 게임이 종료될 때 1회 호출됩니다

유니티 에디터에서는 플레이를 중지할 때 호출 됩니다

<br>

OnDisable() 함수는 OnEnable() 함수와 반대로 컴포넌트가 활성화 되었다가 비활성화 될 때 마다 1회 호출 됩니다

## 이번장을 마치며

대부분 알았던 것들이지만 기초가 제일 중요하기에 자세히 하나하나 정독하며 들었습니다

몰랐던 것들도 있었고 아는것들도 확실하게 확인하게 되었습니다

역시 자만은 금물입니다
