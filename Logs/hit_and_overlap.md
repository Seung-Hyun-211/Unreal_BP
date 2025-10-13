# Hit and Overlap
BeginPlay에서 Hit, Overlap을 수신하고자 하는 요소를 델리게이트에 추가한다.
```
void MyActor::BeginPlay()
{
    Super::BeginPlay();

    Box->OncomponentHit.AddDynamic(this, &MyActor::HitMesh);

    Box->OnComponentBeginOverlap.AddDynamic(this, &MyActor::OverlapBegin);
    Box->OnComponentEndOverlap.AddDynamic(this, &MyActor::OverlapEnd);
}

```
<br>


## Hit, Overlap Delegate로 받는 내용
```
/* Hit */
DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_FiveParams( 
    FComponentHitSignature, UPrimitiveComponent, OnComponentHit, UPrimitiveComponent*, HitComponent, AActor*, OtherActor, UPrimitiveComponent*, OtherComp, FVector, NormalImpulse, const FHitResult&, Hit );

/* BeginOverlap */
DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_SixParams( 
    FComponentBeginOverlapSignature, UPrimitiveComponent, OnComponentBeginOverlap, UPrimitiveComponent*, OverlappedComponent, AActor*, OtherActor, UPrimitiveComponent*, OtherComp, int32, OtherBodyIndex, bool, bFromSweep, const FHitResult &, SweepResult);

/* EndOverlap */
DECLARE_DYNAMIC_MULTICAST_SPARSE_DELEGATE_FourParams( 
    FComponentEndOverlapSignature, UPrimitiveComponent, OnComponentEndOverlap, UPrimitiveComponent*, OverlappedComponent, AActor*, OtherActor, UPrimitiveComponent*, OtherComp, int32, OtherBodyIndex);
```

각 AddDynamic할 함수들

__OnComponentHit__
<br>
```
UFUNCTION()
void HitMesh(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, FVector NormalImpulse, const FHitResult& Hit );
```
__OnComponentBeginOverlap__
<br>
```
UFUNCTION()
void OverlapBegin(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult);
```

__OnComponentEndOverlap__
<br>
```
UFUNCTION()
void OverlapEnd(UPrimitiveComponent* OverlappedComponent, AActor* OtherActor, UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);
```