# Actor / Pawn / Character
|클래스|설명|
|-|-|
|Actor|- 레벨(월드)에 배치되거나 스폰될 수 있는 오브젝트의 기본 클래스<br>- ActorComponent의 컬렉션을 가질 수 있으며, 이를 통해 Actor가 어떻게 움직이는지, 렌더링되는지 등을 제어할 수 있다.|
|Pawn|AI, Player를 조종하는 오브젝트로 Controller를 사용한다.|
|Character|사람형 캐릭터 구현을 위한 Pawn으로 기본적인 Colider, Mesh, Movement를 포함하므로 점프 이동 중력 충돌등을 따로 구현하지 않아도 된다.|

### GameMode에서 BP Pawn 생성하기
원하는 경로의 Pawn 클래스를 불러온다.
```
static ConstructorHelpers::FClassFinder<APawn> PlayerPawnBPClass(
	TEXT("/Game/BP_MyPlayer"));

if (PlayerPawnBPClass.Class != nullptr)
{
	DefaultPawnClass = PlayerPawnBPClass.Class;
}
else
{
	DefaultPawnClass = AMyPlayer::StaticClass();
}
```