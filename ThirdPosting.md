<!-- Heading -->
#  세번째 도토리

<!-- Quote -->
> ## FPS 플레이어 조작
<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

오늘은 게임의 꽃! FPS 1인칭 게임의 조작 기능을 구현해 보려고 합니다

이번에도 케이디님의 예제에서 플레이어 조작만 야금야금 긁어와서 알뜰하게 사용하려고 합니다.

1편에서는 기초 조작, 2편에서는 숙이기 점프 달리기등의 조작도 다룹니다

<br>

이 포스팅은 유튜브 케이디 님의 **[3D_FPS_Survival_Defence](https://www.youtube.com/channel/UC9w-j0OqNzdtOqiYj4lDHmg)**
강의 영상을 참고 하였습니다

<br>
바로 코드 들어갑니다

<hr>
<!-- Numbered list -->

##플레이어 조작

영상에 없는 #region 기능은 제가 정리 하려고 따로 사용 했습니다
~~(깔끔한척)~~

```c#
using System.Collections;
using System.Collections.Generic;
using System.Runtime.InteropServices.ComTypes;
using System.Threading;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    #region Variables
    
    // Editable Variables
    // 다루는 변수는 알아보기 좋은 명확한 이름을 지어줍니다
    // SrializeField, 직렬화하여 private변수를 수정 가능하게 해 줍니다
    [SerializeField] private float walkSpeed;

    [SerializeField] private float runSpeed;
    
    [SerializeField] private float lookSensitivity;

    [SerializeField] private float cameraRotationLimit;
    
    [SerializeField] private float crouchSpeed;
        
    [SerializeField] private float crouchPosY;
    
    [SerializeField] private float jumpForce;
    
    [SerializeField] private Camera theCamera;
    
    // 직렬화를 사용하지 않는 변수는 따로 정리해 줍니다.
    private float applySpeed;
    private float currentCameraRotationX = 0f;
    private float originPosY;
    private float applyCrouchPosY;
    
    private bool isRun = false;
    private bool isCrouch = false;
    private bool isGround = true;
    
    private Rigidbody playerRb;
    private CapsuleCollider capsuleCollider;
    
    #endregion
    
    void Start()
    {
        capsuleCollider = GetComponent<CapsuleCollider>();
        playerRb = GetComponent<Rigidbody>();
        applySpeed = walkSpeed;
        originPosY = theCamera.transform.localPosition.y;
        applyCrouchPosY = originPosY;
    }

    void Update()
    {
        IsGround();
        TryJump();
        TryRun();
        TryCrouch();
        Move();
        CameraRotation();
        CharactorRotation();
    }
    
    #region Functions
    
    // 달리기 입력 함수 입니다
    // LeftShift키를 누르면 달리기 함수를 실행하며 놓을 경우 실행 취소 함수를 호출합니다
    private void TryRun()
    {
        if (Input.GetKey(KeyCode.LeftShift))
        {
            Running();
        }

        if (Input.GetKeyUp(KeyCode.LeftShift))
        {
            RunningCancle();
        }

    }
    
    // 숙이기 입력 함수입니다 LeftContrl키를 눌러 숙이기 함수를 실행합니다
    // 저는 추가로 땅에있을때만 가능하도록 설정 했습니다
    private void TryCrouch()
    {
        if (Input.GetKeyDown(KeyCode.LeftControl) && isGround)
        {
            Crouch();
        }
    }
    // 앞서 실행한 숙이기 입력 함수에서 사용되는 숙이기 함수 입니다
    private void Crouch()
    {
        // 이렇게 선언하면 ON OFF 동작을 하는 Toggle 기능을 합니다
        isCrouch = !isCrouch;
        
        // 숙이기 상태일땐 지정 속도 값을 사용 합니다
        if (isCrouch)
        {
            applySpeed = crouchSpeed;
            applyCrouchPosY = crouchPosY;
        }
        // 그렇지 않은 상태엔 일반 이동속도 값을 사용 합니다
        else
        {
            applySpeed = walkSpeed;
            applyCrouchPosY = originPosY;
        }
        
        // 코루틴 함수로 상태 체크
        StartCoroutine(CrouchCoroutine());
    }

    // 숙이기 기능 코루틴 함수
    IEnumerator CrouchCoroutine()
    {
        float _posY = theCamera.transform.localPosition.y;
        int count = 0;
        // 반복문을 사용하여 일반 시야 높이와 숙인 상태의 시야 높이가 다를때를 추적합니다 
        while (_posY != applyCrouchPosY)
        {
            count++;
            // 숙이기 동작을 즉시 실행하면 어색하므로 Mathf.Lerp를 사용하여 천천히 동작시켜줍니다
            _posY = Mathf.Lerp(_posY, applyCrouchPosY, 0.2f);
            theCamera.transform.localPosition = new Vector3(0, _posY, 0);
            if (count < 15)
                break;
            yield return null;
            // 그리고 지정 높이에 도달하면 종료합니다
        }
        // 새로 받는 카메라의 위치는 Y축값만 받습니다
        theCamera.transform.localPosition = new Vector3(0, applyCrouchPosY, 0f);
    }
    
    // Raycast 기능으로 땅을 확인합니다 여기서 특이한 점은 bounds.extents를 사용해서
    // 캡슐 콜라이더 사이즈의 절반을 기준으로 확인합니다
    private void IsGround()
    {
        isGround = Physics.Raycast
            (transform.position, Vector3.down, capsuleCollider.bounds.extents.y + 0.1f);
    }
    
    // 점프 입력 함수입니다 땅에 착지해 있고 Space키를 입력 받으면 Jump함수를 호출합니다 
    private void TryJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && isGround)
        {
            Jump();
        }
    }
    // 점프 기능 함수
    private void Jump()
    {
        // 숙이기 상태면 !Crouch를 반환하여 점프 상태로 변경 해줍니다
        if(isCrouch)
           Crouch();
        
        // 점프는 jumpForce값 만큼 위로 위치 변경 해줍니다
        playerRb.velocity = transform.up * jumpForce;
    }
    
    // 달리기 실행 함수입니다
    private void Running()
    {   
        // 숙이기 상태면 !Crouch를 반환하여 달리기 상태로 변경 해줍니다
        if(isCrouch)
            Crouch();
        isRun = true;
        // 지정 속도값을 달리기 속도로 지정 해줍니다
        applySpeed = runSpeed;
    }
    // 달리기 취소 함수입니다
    private void RunningCancle()
    {
        // 달리기 상태를 false상태로 바꿔주고
        isRun = false;
        // 지정 속도값을 걷는 속도로 지정 해줍니다
        applySpeed = walkSpeed;
    }
    
    // 기초 움직임
    private void Move()
    {
        // 상하 좌우 키 입력 체크
        float _moveDirx = Input.GetAxisRaw("Horizontal");
        float _moveDirz = Input.GetAxisRaw("Vertical");
        
        // 상하 좌우 이동 구현
        Vector3 _moveHorizontal = transform.right * _moveDirx;
        Vector3 _moveVertical = transform.forward * _moveDirz;

        Vector3 _velocity = (_moveHorizontal + _moveVertical).normalized * applySpeed;
        
        // 플레이어의 Rb를 이동 시킴
        playerRb.MovePosition(transform.position + _velocity * Time.deltaTime);
    }

    // 카메라 회전 기능
    private void CameraRotation()
    {   
        // 마우스의 상하(Y)값을 입력습니다
        // 카메라 각도는 입력받은 방향과 시야 민감도를 곱하여 조정합니다
        float _xRotation = Input.GetAxisRaw("Mouse Y");
        float _cameraRotationX = _xRotation * lookSensitivity;

        // 이부분은 카메라 각도 계산 함수인데 저는 아직 이해 못하겠습니다ㅎㅎ
        currentCameraRotationX -= _cameraRotationX;
        currentCameraRotationX = Mathf.Clamp
            (currentCameraRotationX, -cameraRotationLimit, cameraRotationLimit);

        theCamera.transform.localEulerAngles = new Vector3(currentCameraRotationX, 0f, 0f);
    }
    
    // 이번엔 캐릭터의 방향도 마우스 X값으로 조정 해줍니다
    private void CharactorRotation()
    {
        float _yRotation = Input.GetAxisRaw("Mouse X");

        Vector3 _charactorRotationY = new Vector3(0f, _yRotation, 0f) * lookSensitivity;
        playerRb.MoveRotation(playerRb.rotation * Quaternion.Euler(_charactorRotationY));
    }
    #endregion
}
```

<hr>

# 후기

이렇게 케이디님의 예제 1, 2강을 통해 FPS 기초 조작을 배웠습니다

FPS뿐만 아니라 다른 장르의 게임에서의 조작도 조금만 수정하면 사용 가능하니

잘 기억해두고 꺼내먹도록 합시다

다음엔 FPS의 꽃! 총기 구현 강좌를 들어 보겠습니다

