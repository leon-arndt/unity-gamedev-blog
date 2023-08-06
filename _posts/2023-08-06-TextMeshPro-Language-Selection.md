---
title: "TextMeshPro Language Selection"
date: 2023-08-06
---

# TextMeshPro Language Selection
A small improvement to https://docs.unity3d.com/Packages/com.unity.localization@1.3/manual/Scripting.html#make-a-basic-locale-selection-menu

It improves the Unity example in the following ways:
1. Support for TextMeshPro.
2. Shorter language names (no more culture codes).
3. Get component/required component structure which leads to a clear GameObject structure.


```C#
[RequireComponent(typeof(TMP_Dropdown))]
	public class LanguageSelectionView : MonoBehaviour
	{
		private IEnumerator Start()
		{
			yield return LocalizationSettings.InitializationOperation;
			var options = new List<TMP_Dropdown.OptionData>();
			int selected = 0;
			for (int i = 0; i < LocalizationSettings.AvailableLocales.Locales.Count; ++i)
			{
				var locale = LocalizationSettings.AvailableLocales.Locales[i];
				if (LocalizationSettings.SelectedLocale == locale)
				{
					selected = i;
				}

				options.Add(new TMP_Dropdown.OptionData(locale.Identifier.CultureInfo.EnglishName));
			}

			var dropdown = GetComponent<TMP_Dropdown>();
			dropdown.options = options;
			dropdown.value = selected;
			dropdown.onValueChanged.AddListener(LocaleSelected);
		}

		static void LocaleSelected(int index)
		{
			LocalizationSettings.SelectedLocale = LocalizationSettings.AvailableLocales.Locales[index];
		}
```