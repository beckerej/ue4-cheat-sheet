# Unreal Engine 4 Cheat Sheet

Inspired by docs.unrealengine.com

## Properties & Constructors
### Tick()
```
PrimaryActorTick.bCanEverTick // set to true in constructor to call Tick() every frame.
```
### Set Property
```c++
UCLASS()
class AMyActor : public AActor {
    GENERATED_BODY()

public:
  UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Damage")
    int32 TotalDamage;

  UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Damage")
    float DamageTimeInSeconds;
    ...
}
```
Setting defaults: (else set to `nullptr` by default).
```c++
AMyActor::AMyActor() {
    TotalDamage = 200;
}

AMyActor::AMyActor():TotalDamage(200) { }
```

Making calculated properties hot reload properly, you must hook into PostEditChangeProperty().
```c++
void AMyActor::PostInitProperties() {
    Super::PostInitProperties();
    CalculateValues();
}

void AMyActor::CalculateValues() {
    DamagePerSecond=TotalDamage/DamageTimeInSeconds;
}

#if WITH_EDITOR
void AMyActor::PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) {
    CalculateValues();
    Super::PostEditChangeProperty(PropertyChangedEvent);
}
#endif
```
Creating functions as `UFUNCTION` macro to expose it to UE4's reflection system. "The `BlueprintCallable` option exposes it to the Blueprints Virtual Machine."
```c++
UFUNCTION(BlueprintCallable, Category="Damage")
void CalculateValues();
```  
`UFUNCTION` ~ regular public callable relationship
`BlueprintImplementableEvent` ~ interface-like inheritence  
`BlueprintNativeEvent` ~ virtual-like inheritence where blueprint can override, must implement `<function name>_Implementation()` for default.
   
```c++
void AMyActor::CalledFromCpp_Implementation() { /* DEFAULT */ }
```
