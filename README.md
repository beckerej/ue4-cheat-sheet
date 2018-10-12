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
Setting defaults: (else set to ```nullptr``` by default
```c++
AMyActor::AMyActor() {
    TotalDamage = 200;
}
AMyActor::AMyActor():TotalDamage(200) { }
```
