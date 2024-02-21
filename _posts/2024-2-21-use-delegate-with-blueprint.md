---
author: John
tags: UE c++
---

Firstly, declare it with dynamic multicast:
```cpp
	DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FElevatorReadyToGoSignature, int, ElevatorIdx);
```
Then, make sure to use `BlueprintAssignable` in the specifier:

```cpp
UPROPERTY(BlueprintAssignable, Category = "Elevator")
		FElevatorArrivalSignature ArrivalDelegates;
```

I made a full example with my [Elevator System](https://github.com/cuckon/UE5-ElevatorSystem/blob/master/Elevator/ElevatorBase.h).