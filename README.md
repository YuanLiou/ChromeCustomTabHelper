# ChromeCustomTabHelper
Convenient helper class to launch web page through Google [Chrome Custom Tab](https://developer.chrome.com/multidevice/android/customtabs).

[![](https://jitpack.io/v/YuanLiou/ChromeCustomTabHelper.svg)](https://jitpack.io/#YuanLiou/ChromeCustomTabHelper)

### How to install

1. Add in the root `build.gradle` at the end of repositories:
```groovy
  allprojects {
    repositories {
      ...
      maven { url 'https://jitpack.io' }
    }
  }
```

2. Add the dependency
```groovy
  implementation 'com.github.YuanLiou:ChromeCustomTabHelper:1.0'
```

### How to use

1. Create a new object for `ChromeCustomTabHelper`
```kotlin
    private val chromeCustomTabHelper = ChromeCustomTabsHelper() 
```

2. Warm up the custom tab service in the `onResume()` state of Activity or Fragment <br/>
   And don't forget to cool down in the `onStop()` state
```kotlin
    override fun onResume() {
        super.onResume()
        chromeCustomTabHelper.bindCustomTabsServices(this, url)
    }

    override fun onStop() {
        super.onStop()
        chromeCustomTabHelper.unbindCustomTabsServices(this)
    }
```

3. When it need to open web tab
```kotlin
    val builder = CustomTabsIntent.Builder()
    // here custom your tab styles and behavior
    val chromeCustomTabIntent = builder.build()
    ChromeCustomTabsHelper.openCustomTab(this, chromeCustomTabIntent, uri) { activity, uri ->
        // if chrome is not install, fallback to standard webview 
        // or just send an intent to someone can handle
        val intent = Intent(Intent.ACTION_VIEW)
        intent.data = uri
        startActivity(intent)
    }
```

That's it！









