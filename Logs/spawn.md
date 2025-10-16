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

### Collision Handling Override

C++에서는  [FActorSpawnParameters](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/FActorSpawnParameters)에 포함되는 "Collision Handling Override" 항목은 생성위치에 다른 액터가 존재할 경우 충돌하게될 경우의 처리방식이다.
```
enum class ESpawnActorCollisionHandlingMethod : uint8
{
	/** Fall back to default settings. */
	Undefined								UMETA(DisplayName = "Default"),
	/** Actor will spawn in desired location, regardless of collisions. */
	AlwaysSpawn								UMETA(DisplayName = "Always Spawn, Ignore Collisions"),
	/** Actor will try to find a nearby non-colliding location (based on shape components), but will always spawn even if one cannot be found. */
	AdjustIfPossibleButAlwaysSpawn			UMETA(DisplayName = "Try To Adjust Location, But Always Spawn"),
	/** Actor will try to find a nearby non-colliding location (based on shape components), but will NOT spawn unless one is found. */
	AdjustIfPossibleButDontSpawnIfColliding	UMETA(DisplayName = "Try To Adjust Location, Don't Spawn If Still Colliding"),
	/** Actor will fail to spawn. */
	DontSpawnIfColliding					UMETA(DisplayName = "Do Not Spawn"),
};
```

BluePrint에서는 SpawnActor BP class 를통해 생성하며 생성할 클래스와 위치 등을 설정할 수 있다.

![액터생성](../images/SpawnActorBP.png)

