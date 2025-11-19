# Delegate

임의 오브젝트의 멤버 함수에 동적으로 바인딩.<br>
Delegate오브젝트는 복사해도 안전하며, 값 참조를 전달해야한다.<br>
SingleCast, MultiCast, Dynamic 을 사용할 수 있다.

### 선언
|시그니처|매크로|
|-|-|
|```void Function()```|```DECLARE_DELEGATE( DeleagteName )```|
|```void Function( <Param1> )```|```DECLARE_DELEGATE_OneParam( DelegateName, Param1Type )```|
|```void Function( <Param1>, <Param2> )```|```DECLARE_DELEGATE_TwoParams( DelegateName, Param1Type, Param2Type )```|
|```void Function( <Param1>, <Param2>, ... )```|```DECLARE_DELEGATE_<Num>Params( DelegateName, Param1Type, Param2Type, ... )```|
|```<ReturnValueType> Function()```|```DECLARE_DELEGATE( RetValType, DeleagteName )```|
|```<ReturnValueType> Function( <Param1> )```|```DECLARE_DELEGATE_OneParam( RetValType, DelegateName, Param1Type )```|
|```<ReturnValueType> Function( <Param1>, <Param2> )```|```DECLARE_DELEGATE_TwoParams( RetValType, DelegateName, Param1Type, Param2Type )```|
|```<ReturnValueType> Function( <Param1>, <Param2>, ... )```|```DECLARE_DELEGATE_<Num>Params( RetValType, DelegateName, Param1Type, Param2Type, ... )```|

### 바인딩

바인딩 함수의 종류에 따라 레퍼런스의 강도나, 안전성의 차이가 존재함, <b>사용할 때 유의</b>
|함수|설명|
|-|-|
|```Bind()```|기본 델리게이트 오브젝트에 바인딩|
|```BindStatic()```|raw C++포인터 글로벌 함수 델리게이트를 바인딩|
|```BindRaw()```|raw C++ 포인터 델리게이트에 바인딩, 레퍼런스 사용X -> Execute() 호출시 유의 해야함|
|```BindSP()```| (SP = SharedPtr) 공유 포인터와 기반 멤버 함수 델리게이트에 바인딩 -> 약한 레퍼런스유지, ExcuteIfBound()로 호출|
|```BindUObject()```|UObject기반 멤버 함수 델리게이트를 바인딩, 약한 레퍼런스를 유지, ExecuteIfBound()로 호출|
|```UnBind()```|바인딩 해제|

#### 추가 기능
```
//바인딩 하며 페이로드 데이터를 가팅 전해줄 수 있다.
// 이렇게 사용하면 델리게이트를 불러낼 때 아래 파라미터가 바인딩된 함수에 전달됨
MyDelegate.BindRaw(&MyFunction, 22, true );
```

### 실행
```
Execute(); // 함수를 실행 함수

ExecuteIfBound(); // 함수를 확인하고 존재하면 실행

IsBound(); // 함수 실행시 안전한지 확인하는 함수
```