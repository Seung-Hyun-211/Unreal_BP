# TMap

### TMap

Key-Value 쌍(```TPair<KeyType, ValueType>```)이 하나의 요소로 취급된다.<br>
키는 고유하며 키가 동일한지 비교를 위해 ```operator ==``` 가 필요하다.

TMultiMap을 사용하면 여러 개의 동일한 키를 사용할 수 있다.

- 추가
```
TMap<int32, FString> numToString;

numToString.Add(1, TEXT("one"));
numToString.Add(2, TEXT("two"));
numToString.Add(3, TEXT("three"));

//만약 같은 키를 사용하는 값을 넣을 경우 대체됨
numToString.Add(2, TEXT("TWO"));
//[{1,"one"}, {2,"TWO"}, {3,"three"}]

//value 없이 키값만 넣을 수 있다.
numToString.Add(4); // value에는 valueType의 디폴트값
//[{1,"one"}, {2,"TWO"}, {3,"three"}, {4,""}]


//emplace 복사 및 이동 없이 바로 생성 가능
numToString2.Emplace(5,TEXT("five"));
```

- 이동
```
//Append로 요소들을 붙힐 수 있음 이후 otherMap.Reset() 호출됨
numToString.Append(numToString2);
//numToString  : [{1,"one"}, {2,"TWO"}, {3,"three"}, {4,""}, {5,"five"}]
//numToString2 : []

//MoveTemp로 기존맵을 지우고 옮길 수 있음
numToString.MoveTemp(numToString2); //numToString은 지워지고 numToString2로 채워짐

```

- 반복문 사용
```
for (auto& item : numToString)
{
    ...
}

//CreateIterator : 읽기, 쓰기
//CreateConstIterator : 읽기 전용
for (auto item = numToString.CreateConstIterator(); item; item++)
{
    ...
}
```
- 제거
```
//일반적인 제거, 제거된 수 반환
numToString.Remove(4);

//제거 및 값 반환
FString removed5 = numToString.FindAndRemoveChecked(5);

//제거 및 복사
FString removed6;
bool found = numToString.RemoveAndCopyValue(6, removed6);

//초기화
numToString.Empty(); // slack 조절 가능
numToString.Reset(); // slack 항상 최대
```


- 기타
```
FString stringTwo = numToString[2];

numToString[2] = "two";

int32 count = numToString.Num();

bool hasSeven = numToString.Contains(7);

//주소
FString* ptrThree = numToString.Find(3); // 없으면 nullptr
//원본
FString& findEight = numToString.FindOrAdd(8); // 없으면 디폴트값 반환 및 요소 추가
//사본
FString findNine = numToString.FindRef(9); // 없으면 디폴트값 반환 및 요소 추가

//키값 찾기 - 해쉬를 쓰지 않아 느려짐
const int32* keyOnePtr = numToString.FindKey(TEXT("one")); // 없으면 nullptr

//키만, 값만 추출(기존 배열은 버려짐)
TArray<int32> keys;
TArray<FString> values;

numToString.GenerateKeyArray(keys);
numToString.GenerateValueArray(values);

```

- 정렬
```
//KeySort, ValueSort
numToString.KeySort([](int32 A, int32 B){ return A>B; });
numToSTring.ValueSort([](FString A, FString B){ return ...; });
```

- Slack
```
numToString.Reserve(10); // invalid요소 10개가 됨
numToString.Shrink(); // 끝에서 모든 슬랙을 제거함 [1, -, -, 4, -, -] => [1, -, -, 4]
numToString.Compact(); // 모든 슬랙 제거 [1,4]
```

- [KeyFunction](https://dev.epicgames.com/documentation/ko-kr/unreal-engine/map-containers-in-unreal-engine#key-funcs)<br>
BaseKeyFuncs 를 상속받으면 키를 만들어서 사용할 수 있다.<br>
키가 가져야할 필수 스태틱 함수 ```GetSetKey```, ```Matches```, ```GetKeyHash```