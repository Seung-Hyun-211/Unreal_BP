```
USTRUCT(Atomic, BlueprintType)
struct FItem : FTableRowBase //FTableRowBase를 통해 데이터테이블에서 사용가능
{
	GENERATED_USTRUCT_BODY()

public:
	UPROPERTY(EditAnywhere,BlueprintReadWrite)
	EItemType type;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	int imgNum;
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	FString itemName;
};
```

![dataTable](../images/struct_dataTable.png)