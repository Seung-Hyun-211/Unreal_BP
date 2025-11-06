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

- 정렬
  <br>비교연산자 < 를 사용하여 정렬함FString은 대소문자 구분 없이 사전적으로 구분
  <br>매개변수에 함수를 넣어 사용할 수 있음
  <br>퀵정렬로 구현됨
```
StrArray.Sort();
```
```
//예) 길이를 비교하여 정렬
StrArray.Sort([](const FString& A, const FString& B){ return A.Len() < B.Len(); });
```
```
//머지소트 방식을 사용해서 순서를 보장해줌
//(퀵소트는 하나의 기준을 잡고 앞뒤로 재배치하기 때문에 동일한 요소의 순서를 보장하지 않음)
StrArray.StableSort();
```

- 쿼리
```
// Num 배열의 요소 갯수 를반환
int 32 count = StrArray.Num();

// GetData 요소에 대한 포인터를 반환
FString* StrPtr = StrArray.GetData();

// GetTypeSize 컨테이너 요소 크기
uint32 elementSize = StrArray.GetTypeSize(); // sizeof(FString)

//인덱스를 통한 요소 반환 ( 레퍼런스 타입 )
FString str = StrArray[1];

//IsValidIndex(-1) 유효한 인덱스 확인
bool valid01 = StrArray.IsValidIndex(-1); //false
bool valid02 = StrArray.IsValidIndex(10); //Num() 이상의 인덱스를 넣으면 false

//Last() Top()
StrArray.Last(); // == StrArray.Last(0);
StrArray.Last(1);// StrArray[StrArray.Num()-2];
StrArray.Top(); // 배열의 마지막 요소, 인덱스를 받지 않음

//포함
bool hello = StrArray.Contains(TEXT("Hello"));

//조건 람다 포함 
bool len5 = StrArray.ContainsByPredicate([](const FString& A){ return A.Len() == 5; }); //문자열 길이가 5인 요소가 있는가?

//찾기 -> Find : 찾은 첫 요소, FindLast : 찾은 마지막 요소, IndexOfByKey : (ElementType, KeyType)와 같은 요소의 키 타입에 대해 동작
int32 index;
if(StrArray.Find(TEXT("Hello"), index))
{ //찾았다. index에 요소의 인덱스를 반환받음
}
else
{ //못찾았다. index에 INDEX_NONE 값이 반환됨.
}

//조건 람다 찾기
int32 index = StrArray.FindByPredicate([](const FString& A){ return A.Contains(TEXT("r")); });

//포인터로 반환 찾지 못하면 nullptr 값이 반환, 람다도 가능
FString* rStrPtr = StrArray.FindByKey(TEXT("r"));

//필터
FString filter = StrArray.FilterByPredicate([](const FString& A){ return !A.IsEmpty() && A[0] < TEXT('M'); });
```