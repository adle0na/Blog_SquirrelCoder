<!-- Heading -->
#  네번째 도토리

<!-- Quote -->
> ## FPS 총기 구현
<br>
안녕하세요 코드 지식이 모자라 다람쥐가 도토리 모으듯이 여기저기서 긁어 모아 사용하다가

숨겨 놓은 도토리 까먹듯이 맨날 자료 못찾아서 뒤적거리는 다람쥐코더입니다

이번엔 FPS 게임의 꽃! 총기를 구현 해보겠습니다

총마다 여러개 스크립트 쓰기 귀찮았는데 마침 스크립트 하나로 모든 총기 구현 가능한

예제 영상을 찾았습니다ㅎ 여기에 추가로 저격총 이펙트를 추가해서 모든 총기를 구현 해보겠습니다


<br>

이 포스팅은 해외 유튜브 Dave 님의 **[하나의 스크립트로 모든 총기 구현](https://youtu.be/bqNW08Tac0Y)**
강의 영상을 참고 하였습니다

<br>
바로 코드 들어갑니다

<hr>
<!-- Numbered list -->

##총기 스크립트



```c#
using TMPro;
using System;
using System.Collections;
using UnityEngine;
using Random = UnityEngine.Random;

public class GunSystem : MonoBehaviour
{
    #region Variables
    
    // Gun stats
    public int gunDamage;
    public float timeBetweenShooting, spread, range, reloadTime, timeBetweenShots;
    public int magazineSize, bulletsPerTap;
    public bool allowButtonHold;
    public GameObject scopeOverlay;
    public GameObject weaponCamera;
    public Camera mainCamera;
    
    // SniperScope
    public float scopedFOV = 15f;
    
    private int bulletsLeft, bulletsShot;
    private float normalFOV;

    private bool shooting, readyToShoot, reloading;
    private bool isScoped = false;
    
    // Rigidbody는 마우스 흔들림 때문에 임시로 빼주었습니다
    //private Rigidbody gunRb;
    
    // Reference
    public Camera fpsCam;
    public Transform attackPoint;
    public RaycastHit rayHit;
    public LayerMask whatIsEnemy;
    public Animator animator;
    
    // Graphics ( Without Sound ) 소리도 추가 예정
    public CamShake camShake;
    public float camShakeMagnitude, camShakeDuration;
    public GameObject muzzleFlash, bulletHoleGraphic;
    public TextMeshProUGUI text;
    #endregion
    
    private void Awake()
    {
        //gunRb = GetComponent<Rigidbody>();
        bulletsLeft = magazineSize;
        readyToShoot = true;
    }
    private void Update()
    {
        GunInput();
        
        // SetText
        text.SetText(bulletsLeft + " / " + magazineSize);

        if (Input.GetButtonDown("Fire2"))
        {
            isScoped = !isScoped;
            animator.SetBool("Scoped", isScoped);

            if (isScoped)
            {
                StartCoroutine(OnScoped());
            }
            else
            {
                OnUnscoped();
            }
                
        }
    }

    #region Functions
    
    private void GunInput()
    {
        if (allowButtonHold)
        {
            shooting = Input.GetKey(KeyCode.Mouse0);
        }
        else shooting = Input.GetKeyDown(KeyCode.Mouse0);

        if (Input.GetKeyDown(KeyCode.R) && bulletsLeft < magazineSize && !reloading)
        {
            Reload();
        }
        
        // Shoot
        if (readyToShoot && shooting && !reloading && bulletsLeft > 0)
        {
            bulletsShot = bulletsPerTap;
            Shoot();
        }
    }

    private void Shoot()
    {
        readyToShoot = false;
        
        // Spread
        float x = Random.Range(-spread, spread);
        float y = Random.Range(-spread, spread);
        /*if (gunRb.velocity.magnitude > 0)
        {
            spread = spread * 1.5f;
        }
        else spread = spread;*/
        
        // Calculate Direction with Spread
        Vector3 direction = fpsCam.transform.forward + new Vector3(x, y, 0);
        
        // RayCast
        if (Physics.Raycast(fpsCam.transform.position, fpsCam.transform.forward, out rayHit, range, whatIsEnemy))
        {
            Debug.Log(rayHit.collider.name);

            if (rayHit.collider.CompareTag("Enemy"))
            {
                Debug.Log("Enemy Shot!");
                // Null Reference ShootingAi, TakeDamage 아직 적의 체력과 총알 데미지를 넣지 않아서 Log만 출력합니다
                //rayHit.collider.GetComponent<ShootingAi>().TakeDamage(gunDamage);
            }
        }
        
        // ShakeCamera
        camShake.Shake(camShakeMagnitude, camShakeDuration);
        
        // Graphics
        Instantiate(bulletHoleGraphic, rayHit.point, Quaternion.Euler(0, 100, 0));
        Instantiate(muzzleFlash, attackPoint.position, Quaternion.identity);
        
        bulletsLeft--;
        bulletsShot--;
        
        Invoke("ResetShot", timeBetweenShooting);

        if (bulletsShot > 0 && bulletsLeft > 0)
        {
            Invoke("Shoot", timeBetweenShooting);
        }
    }
    
    private void ResetShot()
    {
        readyToShoot = true;
    }
    private void Reload()
    {
        reloading = true;
        Invoke("ReloadFinished", reloadTime);
    }

    private void ReloadFinished()
    {
        bulletsLeft = magazineSize;
        reloading = false;
    }

    #region Sniper Scope 저격기능
    
    void OnUnscoped()
    {
        scopeOverlay.SetActive(false);
        weaponCamera.SetActive(true);

        mainCamera.fieldOfView = normalFOV;
    }

    IEnumerator OnScoped()
    {
        yield return new WaitForSeconds(.15f);
        
        scopeOverlay.SetActive(true);
        weaponCamera.SetActive(false);
        normalFOV = mainCamera.fieldOfView;
        mainCamera.fieldOfView = scopedFOV;
    }
    #endregion
    
    #endregion
}
```
스크립트 구현이 끝나고 나서 총기별로 값을 수정해주면 됩니다

연사력 좋은 총
<!-- Image -->
![image description](https://i.imgur.com/JLTrEnG.png)

샷건
<!-- Image -->
![image description](https://i.imgur.com/8XyeyNa.png)

저격총은 제가 직접 값을 넣었습니다 필요하면 직접 수정 해보도록 합시다
<!-- Image -->
![image description](https://i.imgur.com/3U7kzum.png)

저격총 이펙트는 다른 강의영상을 참고 하였는데 이번에도 해외 유튜버 [Brackeys님 Sniper_Effect 영상](https://youtu.be/adcKX1c-kag) 을 보시면
단 20분만에 무료 에셋과 함께 완성 가능합니다

총알 발사시에 흔들리는 카메라 움직임도 [Brackeys님 CameraShake영상](https://youtu.be/9A9yj8KnM8c) 을 참고 하시면 됩니다



총기 이펙트를 넣고 나니 발생한 오류는 [Unity오류 문서](https://docs.unity3d.com/Packages/com.unity.postprocessing@2.3/manual/Installation.html)
를 참고하여 해결 했습니다 버전 오류라고 하니 수정 해줍시다 추가로 수정 하고 나면 Library하위 폴더 전부가 깃 데스크 로컬체인지에 걸리는데 Ignore 기능으로
무시 해주셔야 커밋 하는데 문제가 안생깁니다 추가로 생기는 오류는 댓글을 달아주세요

<hr>

# 후기

완성하고 나니 드디어 뭔가 만들어지는 느낌 입니다 코로나 양성이 떠버려서 작업속도가 느려졌는데 얼른 회복하고
다음엔 디테일 추가 작업으로 총기를 마무리하고 적AI나 스테이지 제작 작업을 해보겠습니다
