# Class

클래스는 읽는 사람을 염두하고 작성해야하므로 public을 먼저 선언

# 명명규칙
각 단어의 첫 번째 글자를 대문자로 사용<br>클래스 종류에 따른 접두사 설정<br>
|접두사|클래스|
|-|-|
|T|템플릿 클래스|
|U|UObject를 상속|
|A|AActor를 상속|
|S|SWidget를 상속|
|I|Interface|
|C|Concept|
|E|Enum|
|b|bool|
|F|그 외 대부분 non-UObject타입의 실용적 의미<br>초기 엔진 코드에서 유래되었으며 Fred 라는 이름을 붙히던 관습이 굳어진것|

# Const

```
//함수 실행인자가 함수에 의해 수정되지 않아 함수 실행인자를 const 포인터 또는 참조로 전달하는 경우
void SomeMutatingOperation(FThing& OutResult, const TArray<Int32>& InArray)
{
	//  OutResult 수정 O, InArray 수정 X
}

//메서드가 오브젝트를 수정하지 않아 const로 메서드의 플래그를 지정하는 경우
void FThing::SomeNonMutatingOperation() const
{
	// 호출한 FThing을 수정 X
}

//루프에서 컨테이너 수정을 하지 않아 const를 사용하여 컨테이너에 반복작업을 하는 경우
TArray<FString> StringArray;
for (const FString& : StringArray)
{
	// 루프의 바디는 StringArray를 수정 X.
}
```

# nullptr
```NULL``` 대신 ```nullptr``` 사용<br>

# auto
몇 가지 상황을 제외하고 ```auto```를 사용하지 말것<br>
초기화 하려는 타입은 항상 명시해야 한다.

auto를 사용 가능한 경우
- 변수에 람다를 바인딩해야 하는 경우.
- Iterator (반복자) 변수의 경우.
- template 코드에서 타입을 쉽게 식별할 수 없는 경우

