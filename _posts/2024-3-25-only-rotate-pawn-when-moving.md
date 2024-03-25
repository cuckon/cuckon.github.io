---
author: John
tags: UE 3C
---
![](/assets/img/posts-202403/03-25-camera_rotation.gif)

Like shown in the above gif, there are instances that you want your character to stand still when it's not moving, while rotating to camera direction when in motion.

I found the fairly easy way to implement it is:

Firstly, set the `bUseControllerRotationYaw` to `false` at some point (I opt to do it in the construction method.)

Then, utilize the `bUseControllerDesiredRotation` toggle of CharacterMovement! Basically when this is `true` the CharacterMovementComponent will align its X axis to match the camera direction.

Here's my implementation:
```cpp
    GetCharacterMovement()->bUseControllerDesiredRotation = (
		GetCharacterMovement()->GetLastUpdateVelocity().Length() > 1   // moving
		&& CaughtByPlayers.IsEmpty()	// not caught
		&& !IsValid(CaughtPlayer) // caught any player
	);

	if (CaughtPlayer)
	{
		const FRotator Rotation = UKismetMathLibrary::FindLookAtRotation(
			GetActorLocation(), CaughtPlayer->GetActorLocation()
		);

		const FRotator DesiredRotation = FMath::RInterpTo(GetActorRotation(), Rotation, DeltaTime, AlignToCaughtRate);

		GetCharacterMovement()->MoveUpdatedComponent(
			FVector::ZeroVector, DesiredRotation,
			/*bSweep*/ false );
	}
```

Note that when `bUseControllerDesiredRotation` is `false`, you can use `GetCharacterMovement()->MoveUpdatedComponent` to tweak the character's rotation.