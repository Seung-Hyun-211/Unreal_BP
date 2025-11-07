# TArray

- 제거<br>Remove 동일한 모든 요소를 제거<br>RemoveSingle 처음 일치한 요소 제거<br>RemoveAt 인덱스로 제거
```
TArray<int32> valArr;
int32 temp[] = {1,2,3,4,5,1,2,3,4,5};
valArr.Append(temp, ARRAY_COUNT(temp));

valArr.Remove(2);// 1,3,4,5,1,3,4,5

valArr.RemoveSingle(1);// 3,4,5,1,3,4,5

valArr.RemoveAt(2);// 3,4,1,3,4,5
```
RemoveAll 함수를 통한 제거
```
valArr.RemoveAll([](int32 value){return (value % 3) == 0; });
```
RemoveSwap, RemoveAtSwap, RemoveAtAll 빠른 대신 작업후의 요소 순서가 바뀌어 있음

Empty
```
vallArr.Empty(); // vallArr == []
```

- Operator

배열은 엄역하게 요소를 가지기 때문에 깊게 복사됨 -> 복사로 생성하는 새 배열은 자체적인 사본을 만듦
```
TArray<int32> arr1;
arr1.Add(0);
arr1.Add(1);
arr1.Add(2);

auto arr2 = arr1;
arr2[1] = 4;

```