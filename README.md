# Unreal_BP

    블루프린트를 이용한 언리얼학습

# Actor / Pawn / Character

|클래스|설명|
|-|-|
|Actor|- 레벨(월드)에 배치되거나 스폰될 수 있는 오브젝트의 기본 클래스
||- ActorComponent의 컬렉션을 가질 수 있으며, 이를 통해 Actor가 어떻게 움직이는지, 렌더링되는지 등을 제어할 수 있다.|
|Pawn|- AI, Player를 조종하는 오브젝트로 Controller를 사용한다.|
|Character|- 사람형 캐릭터 구현을 위한 Pawn으로 기본적인 Colider, Mesh, Movement를 포함하므로 점프 이동 중력 충돌등을 따로 구현하지 않아도 된다.|

# Controller
Pawn을 조종하기 위한 클래스이다.

입력을 통해 Pawn을 조종하는 PlayerController, AI로직을 통해 Pawn을 조종하는 AIController 등이 있다.

주로 사용하게 될 PlayerController 클래스는 아래와 같이 Player, HUD, Camera를 가지고 있어 입력에의한 Pawn 조작뿐 아니라 UI, 카메라 조작도 가능하다.
```
UPROPERTY()
TObjectPtr<UPlayer> Player;

UPROPERTY()
TObjectPtr<AHUD> MyHUD;

UPROPERTY(BlueprintReadOnly, Category=PlayerController)
TObjectPtr<APlayerCameraManager> PlayerCameraManager;
```
# Enhanced Input System
중요 포인트
- player controller
- input action
- input mapping component

![인풋확인](images/Enhanced_Input.png)


# Player Move 구현

![간단한움직임](images/Simple_Move.png)