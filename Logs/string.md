# 문자열
문자열 인코딩에는 `TEXT()` 매크로를 사용
|클래스|개요|
|-|-|
|```FName```|- 데이터 테이블에 한 번만 저장된다.<br>- 대소문자를 구별하지 않는다.<br>- 변경할 수 없다.|
|```FText```|- 텍스트 현지화 지원을 위한 주요 컴포넌트.<br>- 외부 API를 인터페이스에 표시하는 작업 등에 유용.|
|```FString```|- 조작 가능한 유일한 스트링 클래스.<br>- 검색, 변경, 비교 가능하지만 그만큼 무겁다.|
### [문자열 클래스변환](https://dev.epicgames.com/documentation/en-us/unreal-engine/string-handling-in-unreal-engine#conversions)

### FName
생성 <br>```FName TestName = FName(TEXT("TestFName"));```<br><br>
변환 From FName<br>```TestString = TestName.ToString();```<br>```TestText = FText::FromName(TestName);```<br><br>
변환 To FName<br>```TestName = FName(*TestString);```<br>```FText -> FString -> FName```<br><br>
비교<br>`==` 연산자 사용 -> true/false<br>`TestName.Compare(OtherName);` 함수 사용 -> -1 / 0 / 1

### FText
텍스트 포맷, 숫자 및 시간 텍스트 생성 등에 유용<br>
```FText::GetEmpty()``` ```FText()```를 통해 빈 FText를 만들 수 있음<br>

변환<br>
```AsCultureInvariant``` : 현지화되지 않는 FText인스턴스 생성<br>
```FormString``` : 기존 FString 에서 FText 인스턴스 생성<br>
```FromName``` : 기존 FName에서 FText 인스턴스 생성, FName.ToString() 출력에서 FromString 을 호출하는것과 같음

비교<br>
```EqualTo``` : true/false<br>
```CompareTo``` : -1 / 0 / 1<br>