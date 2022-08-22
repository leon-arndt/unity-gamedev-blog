---
title: "Improving Unity Code Ergonomics"
date: 2022-05-18
---

# Improving Unity Ergonomics

## GameObjects
`gameObject.SetActive(false)` is a line of code you've probably read before. As an exercise: Open the largest Unity codebase you have access to and search for `.SetActive(` you will probably find hundreds or thousands of results depending on the size of the project, so, where's the problem?

It was not immediately obvious to me at first but `.SetActive(true)` and `SetActive(false)` have parameters which means that these parameters can be incorrect. Think about whether you have seen code which deactivated a GameObject but activated it instead. I have.

Suggested Solution:
`gameObject.Activate()` instead of `gameObject.SetActive(true)`
and `gameObject.Deactivate()` instead of `gameObject.SetActive(false)`.

Advantages of suggested Solution:
- shorter
- no parameter (replaced with a clear method name)


## MonoBehaviours
Just like GameObjects, MonoBehaviours benefit from shorter and more definite code, I generally also add a `monoBehaviour.Activate()` extension which 

## UI Button Example
Buttons commonly need click behavior. This is offered with a `Bind()` extension which removes all other listeners. This leads to a clearer usage:

Before:
```C#
public class ErrorView : MonoBehaviour
{
    [SerializeField] private TextMeshProUGUI bodyText;
    [SerializeField] private Button closeButton;

    private void Start()
    {
        closeButton.onClick.RemoveAllListeners();
        closeButton.onClick.AddListener(() =>
        {
            gameObject.SetActive(false);
        });
    }
}
```

becomes

After:
```C#
public class ErrorView : MonoBehaviour
{
    [SerializeField] private TextMeshProUGUI bodyText;
    [SerializeField] private Button closeButton;

    private void Start()
    {
        closeButton.Bind(this.Deactivate);
    }
}
```
## Try out my extension package
Add
`"com.larndt.ergonomic-extensions": "https://github.com/leon-arndt/UnityExtensions.git"` to `Packages/manifest.json`


That's it.