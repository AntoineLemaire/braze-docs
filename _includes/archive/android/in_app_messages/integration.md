# Integration {#in-app-messaging-integration}

## Step 1: Braze In-App Message Manager Registration

In-App Message display is managed by the [`BrazeInAppMessageManager`][34] class. Every activity in your app must be registered with the `BrazeInAppMessageManager` to allow it to add in-app message views to the view hierarchy. There are two ways to accomplish this:

### Activity Lifecycle Callback Integration (Recommended)

The [Activity Lifecycle Callback Integration][59] handles in-app message registration automatically, no extra integration is required. This is the recommended integration for handling in-app message registration.

### Manual In-App Message Registration

A manual in-app message registration requires 3 steps.

{% alert warning %}
If you did the activity lifecycle integration, then you should *not* do a manual in-app message integration.
{% endalert %}

In your [`Application.onCreate()`][82], call [`ensureSubscribedToInAppMessageEvents()`][69].

{% tabs %}
{% tab JAVA %}

```java
BrazeInAppMessageManager.getInstance().ensureSubscribedToInAppMessageEvents(context);
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
BrazeInAppMessageManager.getInstance().ensureSubscribedToInAppMessageEvents(context)
```

{% endtab %}
{% endtabs %}

In every activity where in-app messages can be shown, [`registerInAppMessageManager()`][80] should be called in that activity's `onResume()`.

{% tabs %}
{% tab JAVA %}

```java
@Override
public void onResume() {
  super.onResume();
  // Registers the BrazeInAppMessageManager for the current Activity. This Activity will now listen for
  // in-app messages from Braze.
  BrazeInAppMessageManager.getInstance().registerInAppMessageManager(activity);
}
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
public override fun onResume() {
  super.onResume()
  // Registers the BrazeInAppMessageManager for the current Activity. This Activity will now listen for
  // in-app messages from Braze.
  BrazeInAppMessageManager.getInstance().registerInAppMessageManager(this)
}
```

{% endtab %}
{% endtabs %}

In every activity where [`registerInAppMessageManager()`][80] was called, [`unregisterInAppMessageManager()`][81] should be called in that activity's `onPause()`.

{% tabs %}
{% tab JAVA %}

```java
@Override
public void onPause() {
  super.onPause();
  // Unregisters the BrazeInAppMessageManager for the current Activity.
  BrazeInAppMessageManager.getInstance().unregisterInAppMessageManager(activity);
}
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
public override fun onPause() {
  super.onPause()
  // Unregisters the BrazeInAppMessageManager.
  BrazeInAppMessageManager.getInstance().unregisterInAppMessageManager(this)
}
```

{% endtab %}
{% endtabs %}

## Step 2: (Optional) In-App Message Manager Blacklist

In your integration, you may require that certain Activities in your app should not show In-App Messages. The [Activity Lifecycle Callback Integration][59] provides an easy way to accomplish this.

The following example code adds two Activities to the In-App Message registration blacklist, `SplashActivity` and `SettingsActivity`.

{% tabs %}
{% tab JAVA %}

```java
public class MyApplication extends Application {
  @Override
  public void onCreate() {
    super.onCreate();
    Set<Class> inAppMessageBlacklist = new HashSet<>();
    inAppMessageBlacklist.add(SplashActivity.class);
    inAppMessageBlacklist.add(SettingsActivity.class);
    registerActivityLifecycleCallbacks(new BrazeActivityLifecycleCallbackListener(inAppMessageBlacklist));
  }
}
```

{% endtab %}
{% tab KOTLIN %}

```kotlin
class MyApplication : Application() {
  override fun onCreate() {
    super.onCreate()
    val inAppMessageBlacklist = HashSet<Class<*>>()
    inAppMessageBlacklist.add(SplashActivity::class.java)
    inAppMessageBlacklist.add(SettingsActivity::class.java)
    registerActivityLifecycleCallbacks(BrazeActivityLifecycleCallbackListener(inAppMessageBlacklist))
  }
}
```

{% endtab %}
{% endtabs %}

> See the [`BrazeActivityLifecycleCallbackListener`][83] constructor javadocs for more information.

[34]: https://appboy.github.io/appboy-android-sdk/javadocs/com/braze/ui/inappmessage/BrazeInAppMessageManager.html
[69]: https://appboy.github.io/appboy-android-sdk/javadocs/com/braze/ui/inappmessage/BrazeInAppMessageManager.html#ensureSubscribedToInAppMessageEvents-android.content.Context-
[80]: https://appboy.github.io/appboy-android-sdk/javadocs/com/braze/ui/inappmessage/BrazeInAppMessageManager.html#registerInAppMessageManager-android.app.Activity-
[81]: https://appboy.github.io/appboy-android-sdk/javadocs/com/braze/ui/inappmessage/BrazeInAppMessageManager.html#unregisterInAppMessageManager-android.app.Activity-
[82]: https://developer.android.com/reference/android/app/Application.html#onCreate()
[83]: https://appboy.github.io/appboy-android-sdk/javadocs/com/braze/BrazeActivityLifecycleCallbackListener.html#BrazeActivityLifecycleCallbackListener-java.util.Set-
