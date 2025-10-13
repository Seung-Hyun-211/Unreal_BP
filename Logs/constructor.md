# ConstructorHelpers / LoadClass

ConstructorHelpers : 주로 객체 생성자에서 사용되는 구조체<br>
경로가 존재하지 않으면오류남<br>FClassFinder, FObjctFinderOptional 함수 사용
```
static ConstructorHelpers::FObjectFinder<ObjName>OutObject(TEXT(" 경 로 "));

if(OutObject.Succeeded()) //불러왔을 경우
{...}
```

LoadClass : 클래스가 필요한 시점에 사용되는 오브젝트 로드함수<br>
잘못된 경우 nullptr을 반환
```
void AMyPlayerController::BeginPlay()
{
	UClass* WidgetBPClass = LoadClass<UUserWidget>(nullptr, TEXT("/Game/Level/TestWidget"));
	if (WidgetBPClass)
	{
		UUserWidget* MyWidget = CreateWidget<UUserWidget>(this, WidgetBPClass);
		if (MyWidget)
		{
			MyWidget->AddToViewport();
		}
	}
}
```