---
title: "ScriptableObject Systems"
date: 2022-05-18
---

Scriptable objects are perfect data containers because they can easily be shared as references between different MonoBehaviours. This is not a new idea, notable [
Ryan Hipple's Unite Austin 2017 talk](https://www.youtube.com/watch?v=raQ3iHhE_Kk) covers the topic.

Hipple's pillars are:
- Modular
- Editale
- Debugabble

In my own implementation I also strive for these goals by relying on ScriptableObjects which offer all of these pillars out-of-the-box. 

An example:
Recently I was working on a hobby project which required a Soft Currency system. In many games this is gold coins.

This soft currency system has some requirements:
- Changed from many places (e.g. shop, world object pickups)
- Displayed in many places (e.g. shop UI, the game hud, the lose screen)

An example implementation:
```C#
 [CreateAssetMenu(menuName = "IntSystem")]
    public class IntSystem : ScriptableObject
    {
        [SerializeField] private int defaultValue;
        private int currentAmount;

        private void OnEnable()
        {
            Reset();
        }

        public void Reset()
        {
            currentAmount = defaultValue;
        }

        public void Add(uint amount)
        {
            currentAmount += (int) amount;
        }

        public void Remove(uint amount)
        {
            currentAmount -= (int) amount;
        }
        
        public void Set(int amount)
        {
            currentAmount = amount;
        }

        public int Get()
        {
            return currentAmount;
        }
    }
```

A scriptable object can then be created and referenced wherever need, regardless of whether we are reading or writing into the system.

## Advantages over other systems
- Script Execution Order will be less of a problem than it would be with singletons MonoBehaviours.
- Simple: creating new systems assets is normally 1-2 clicks and then simply dragging the system into places where it is needed which is faster than coding a new system, like "SoftCurrencySystem" by hand

## Automatically installing services
The power of generics and ScriptableObject can be combined to create a very powerful and simple solution for creating easy-to-access services for games which can be used to define controller-like behavior (considering MVC) e.g. managing an inventory, handling shop requests, making network requests, etc.
An `IService` interface allows us to easily access these systems/services from anywhere, consider the following GameInstaller:

```C#
using System;
using System.Linq;
using UnityEngine;
using Object = UnityEngine.Object;

namespace Systems
{
    public static class GameInstaller
    {
	    private static Object[] _cachedServices;
	    private const string Path = "Systems";

	    public static T Get<T>() where T : ScriptableObject
	    {
		    return (T)_cachedServices.First(x => x is T);
	    }

        public static void StartAll()
        {
            var scriptableObjects = Resources.LoadAll(Path, typeof(ScriptableObject));
            foreach (var scriptableObject in scriptableObjects)
            {
                if (scriptableObject is IService service)
                {
                    service.Init();
                }
            }

            _cachedServices = scriptableObjects;
        }
    }
}
```

Which offers these systems some startup behavior which can be init by calling `StartAll()` at the beginning of the game, e.g. from some sort of GameManager.
Suddenly adding something to the inventory (regardless of whether it is from UI or some sort of other ScriptableObject) becomes trivial:

```C#
public override void OnBuy()
{
    GameInstaller.Get<InventoryService>().Add(data);
}
```

where the Inventory Service is

```C#
	[CreateAssetMenu(menuName = "ScriptableObjects/Services/" + nameof(InventoryService))]
	public class InventoryService : ScriptableObject
	{
        [SerializeField] private PersistentIntSystem softCurrencySystem;
		[SerializeField] private PersistentIntSystem hardCurrencySystem;

        public void Add(object reward)
		{
			...
		}
    }
```


## Limitations
This implementation is limited to int types, you may want to create a separate `FloatSystem` class or create your own generic `System` class which works with many different types.

ScriptableObjects need to be reset carefully during runtime. Commonly this happens in `Start()` or `OnEnable()` methods. If ScriptableObjects are not reset data which was used during testing may be pushed onto the git master branch and land in a release which can lead to players suddenly having a ton of game currency for example.

These systems will also not allow for more specific behavior (such as a sound being played each time the system value changes). For that an event could be used, or a new type of system class could be created, e.g. `HealthSystem` if health-specific behavior is needed.


