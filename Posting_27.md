<!-- Heading -->
#  스물네번째 도토리

<!-- Quote -->
> ## 유니티 최적화 Batch 줄이기 학습
>
> ### [유니티 TIPS] 유니티 최적화를 위한 필수 기본기! Batching 방법 소개 영상

유튜브 Unity Korea의 골드메탈님의 강의 내용입니다

<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

<br>

취직하고 쭉 못올리다가 오랫만에 업로드하네요

<br>

## Batch란 무엇인가?

### Draw Call

CPU에서 읽어들인 데이터를 GPU로 전달하여 그려내는 작업이 Draw Call

### SetPass Call

Draw Call로 CPU가 GPU로 명령을 내릴때 따라오는 값을 Command Buffer 라고 한다

그중에 그래픽 계열 (Material,Shader 등) 을 묶어 놓은것이 SetPass Call

이것을 그래픽뿐만 아니라 전부 함께 넘기는것이 Batch라고 합니다

## Batch에 해당되는 컴포넌트들

### Sprite Renderer

### Mesh Renderer

### Line Renderer

### Trail Renderer

### Particle System

우선 각각 다른 Material을 가진 오브젝트들은

Material이 다르기때문에 Batch 수가 그만큼 그대로 존재합니다

따라서 Atlas로 Texture를 하나로 합친후에 하나의 Material을 만든후에 UV좌표를 수정하여 하나의 Material로

만들면 Batch수는 그대로지만 SetPass Call은 1개만 사용하게 됩니다

## Dynamic Batching (동적 배칭)

우선 Preference로 가서 Core Render Pipeline에서

Additional Properties에 Visibility를 All Visible로

Project Settings에 Rendering 항목을보면 Render Pipeline Asset으로 확인 할 수 있음

(글보단 영상이 더 자세하니 링크 참조 해주세요)

Dynamic Batcing을 실행하면 Saved by batching에 한개를 제외한 나머지 오브젝트 수 만큼

Saved by batching 됐다고 뜹니다 Batch 카운트도 1개네요

주의해야할점은 정점 속성을 900개 이상 가지거나 225개 이상의 정점을 포함하는 Mesh에는 사용이 불가능 합니다

근데 Sprite Atlas는 이미 동적 배칭이다

## Static Batching (정적 배칭)

마찬가지로 설정에서 Static Batching을 켜주고 확인을 해보면 Batch Count는 확실히 줄어있지만

여러 매시들의 정점을 하나로 통합하였기 때문에

정적 배칭이므로 오브젝트가 움직이지 않습니다

## SRP Batching

이번에도 설정에서 SRP Batcher를 선택한 후 확인 해보면 Batch Count는 그대로지만

SetPass Call은 줄어있습니다 그런데 놀라운건 오브젝트들이 각각 다른 Material을 쓰고있다는 거죠

단! 여기에는 조건이 붙습니다 Material이 달라도 하나의 셰이더만을 사용해야 한다는거죠

그리고 셰이더를 선택하면 인스펙터 화면에서 SRP Batcher의 사용 가능 여부를 볼 수 있습니다

## GPU Instancing

이번엔 극도로 줄일 수 있는 방법입니다 이번엔 줄일 셰이더의 SRP Batcher를 끄고 (SRP가 호환하지 않는다면 안꺼도 된다)

줄일 셰이더에 Advanced Options에 Enable GPU Instancing을 체크하면 놀랍게도 Batch Count가 1입니다

CPu가 하나의 Mesh만 읽어서 그걸 GPU에 넘기고 GPU는 메모리 안에서 저장된 값으로 동일한 Mesh를 그려나가는 방식입니다

대부분의 일을 GPU가 하게 되는거죠 근데 정말 수많은 Mesh를 만들어도 Count가 1은 아니고 어느정도 허용치를 넘어가면

Count가 1씩 증가하게 됩니다

## 이번 과정을 마치며

모바일은 최적화가 생명이니 이것저것 더 알아봐야겠어요


