# Unreal Container

### TArray

가장 간단한 컨테이너, 요소타입, 선택적 얼로케이터(생략가능) 두 가지 프로퍼티로 정의한다.
```TArray<int32> IntArray;```

- 초기화
```
IntArray.Init(10, 3);

//[10,10,10]
```
- 배열 끝에 생성<br>
  Add(Push) : 배열에 복사(이동)<br>
  Emplace : 실행인자를 사용한 새 인스턴스 생성
```
TArray<FString> StrArray
StrArray.Add(TEXT("Text1"));
StrArray.Emplace(TEXT("Text2"));

//["Text1","Text2"]
```
- 여러 요소 추가
```
FString TempArray = {TEXT("Text3"), TEXT("Text4")};
StrArray.Append(TempArray, ARRAY_COUNT(TempArray));

//["Text1","Text2","Text3","Text4"]
```
- 중복없이 Add
```
StrArray.AddUnique(TEXT("!"));
StrArray.AddUnique(TEXT("!"));

//["Text1","Text2","Text3","Text4","!"]
```
- 삽입
```
StrArray.Insert(TEXT("Text5"), 1);
//["Text1","Text5","Text2","Text3","Text4","!"]
```
- 요소 숫자 설정
```
StrArray.SetNum(8);
//["Text1","Text5","Text2","Text3","Text4","!","",""]
```

### TMap




### TSet




