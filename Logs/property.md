# Property
- 프로퍼티 선언시 아래와 같이 사용
```
UPROPERTY( A, B, ... , key = value)
Type Var;
```
 
 ### 자주 쓰이는 프로퍼티<br>([프로퍼티 지정자](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-uproperties#propertyspecifiers))
  ```EditAnywhere``` : 에디터 패널에서 편집 가능
  <br>```BlueprintReadWrite``` : 블루프린트에서 읽기/쓰기 가능
  <br>```VisibleAnywhere``` : 에디터에서 값을 볼 수 있되 편집 불가능
  <br>```BlueprintReadOnly``` : 블루프린트에서 읽기 가능
  <br>```EditDefaultsOnly``` : 클래스 __디폴트값__ 에서만 편집 가능
  <br>```Category = "Category"``` : 디테일 패널에서 그룹화