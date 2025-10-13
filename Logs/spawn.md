# Spawn

Actor를 생성하기 위해서는 World에서 SpawnActor 함수를 사용해야 한다.

```
/* SpawnActor 함수
 * Spawn Actors with given transform and SpawnParameters
 * 
 * @param	Class					Class to Spawn
 * @param	Location				Location To Spawn
 * @param	Rotation				Rotation To Spawn
 * @param	SpawnParameters			Spawn Parameters
 *
 * @return	Actor that just spawned
*/

GetWorld()->SpawnActor( ... );
```

BluePrint에서는 SpawnActor BP class 를통해 생성하며 생성할 클래스와 위치 등을 설정할 수 있다.

![액터생성](../images/SpawnActorBP.png)

SpawnActorBP 에서 "Collision Handling Override" 항목은 생성위치에 다른 액터가 존재할 경우 충돌하게될 경우의 처리방식이다.
|선택 항목|설명|
|-|-|
|Always Spawn, Ignore Colisions|충돌 여부와 관계없이 무조건 생성|
|Try To Adjust Location, But Always Spawn|근처에 충돌하지 않을 수 있는 부분을 찾아 생성한다.<br>(찾지 못할 경우 기본 위치에서 생성)|
|Try To Adjust Location, Don't Spawn If Still Colliding|근처에 충돌하지 않을 수 있는 부분을 찾아 생성한다.<br>(찾지 못하면 액터를 생성하지 않는다.)|
|Do Not Spawn|다른 액터와 충돌시 무조건 생성하지 않는다.|