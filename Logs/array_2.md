# TArray - Heap

TArray배열을 Heapify 함수를 통해 힙으로 전환할 수 있다. ``` heapArr.Heapify();```
<br>정렬은 이루어지지 않으며 위에서 아래로, 왼쪽에서 오른쪽으로 읽는다.

### 추가 및 제거
```
heapArray.HeapPush(4); // 배열의 마지막에 요소를 추가함.

HeapPop(topNode); // topNode에 최상위 노드를 반환함
HeapPopDiscard(); // 아무것도 반환하지 않음

heapArray.HeapRemoveAt(1); // 인덱스 요소를 배열에서 제거함
```

### 최상위 노드 확인
```heapArray.HeapTop()```

# Slack

```
array.GetSlack(); // 할당된 배열중 사용되지 않은 요소 수
array.Num();      // 사용된 요소 수
array.Max();      // 할당된 배열의 총 요소 수

//                  slack, num, max
array.Empty();    // 0  -  0  -  0 
array.Empty(5);   // 5  -  0  -  5

array.Add(3);     // 4  -  1  -  5
array.Reset(0);   // 5  -  0  -  5 
array.Reset(10);  // 10 -  0  -  10

array.Add(3);     // 4  -  1  -  5
array.Add(4);     // 3  -  2  -  5
array.Shrink();   // 0  -  2  -  2
```

### 원시 메모리

Add, Insert와 비슷하지만 생성자를 호출하지 않는다. -> 쓰레기값이 들어가 있음
```
intArray.AddUnInitialized(4);      // 초기화 하지 않은 빈 공간을 4개 추가
FMemory::Memcpy(IntArray.GetData(), dataArray, 4*sizeof(int32));


strArray.InsertUnInitialized(1, 4);// 초기화 하지 않은 빈 공간을 1번 인덱스부터 4개 추가
new ((void*)(strArray.GetData()+1))FString(TEXT("A"));

```

