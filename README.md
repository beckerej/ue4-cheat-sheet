# Unreal Engine 4 Cheat Sheet

Inspired by docs.unrealengine.com

## Properties & Constructors
### Tick()
```
PrimaryActorTick.bCanEverTick // set to true in constructor to call Tick() every frame.
```
### Set Property
```
public:
  UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Damage")
    int32 TotalDamage;

  UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="Damage")
    float DamageTimeInSeconds;
```
Setting defaults:
```
AMyActor::AMyActor() :
    TotalDamage(200),
    DamageTimeInSeconds(1.f)
{
}
```
