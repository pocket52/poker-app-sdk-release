# Pocket52 Poker SDK Docs

This Document contains POCKET 52’s POKER SDK’s Documentation.

### Setup

This SDK requires a user auth key to run.

Import the .aar file into your android project using.. File-->New Module-->Aar project
Import the .jar file into your android project inside libs folder.


## Dependencies

For reference you can use the following ext:


```java
ext {
    appName = "Pocket52"
    gdxVersion = '1.9.8'
    roboVMVersion = '2.3.3'
    box2DLightsVersion = '1.4'
    ashleyVersion = '1.7.0'
    aiVersion = '1.8.0'
    butterknifeVersion = '8.4.0'
    daggerVersion = '2.13'
    rxandroidVersion = '2.0.1'
    rxjavaVersion = '2.1.8'
    androidNetworkingLibVersion = '1.0.2'
    crashreporterVersion = '1.0.9'
    supportLibVersion = '28.0.0'
}
```

Include the following dependencies in your main app build.gradle file.

```java
    configurations { natives }

    dependencies {
    implementation "com.badlogicgames.gdx:gdx-backend-android:$gdxVersion"
    natives "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-armeabi"
    natives "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-armeabi-v7a"
    natives "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-arm64-v8a"
    natives "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-x86"
    natives "com.badlogicgames.gdx:gdx-platform:$gdxVersion:natives-x86_64"

    implementation "com.badlogicgames.gdx:gdx:$gdxVersion"
    implementation "com.badlogicgames.gdx:gdx-freetype:$gdxVersion"

    implementation "com.badlogicgames.gdx:gdx-freetype:$gdxVersion"
    natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-armeabi"
    natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-armeabi-v7a"
    natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-arm64-v8a"
    natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-x86"
    natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-x86_64"

    implementation ('com.android.support:appcompat-v7:28.0.0') {
        force true
    }

    implementation 'com.android.support.constraint:constraint-layout:1.1.3'

    implementation 'com.jakewharton.rxrelay2:rxrelay:2.1.0'

    implementation "io.reactivex.rxjava2:rxandroid:$rxandroidVersion"
    implementation "io.reactivex.rxjava2:rxjava:$rxjavaVersion"

    implementation "com.amitshekhar.android:android-networking:$androidNetworkingLibVersion"
    implementation "com.amitshekhar.android:rx2-android-networking:$androidNetworkingLibVersion"
    implementation 'com.squareup.picasso:picasso:2.71828'

    implementation("com.android.support:recyclerview-v7:$supportLibVersion") {
        force true
    }
    implementation 'com.android.volley:volley:1.1.0'

    implementation('io.socket:socket.io-client:0.8.3') {
        // excluding org.json which is provided by Android
        exclude group: 'org.json', module: 'json'
    }
    annotationProcessor 'com.bluelinelabs:logansquare-compiler:1.3.6'
    implementation 'com.bluelinelabs:logansquare:1.3.6'
    implementation ("com.android.support:design:$supportLibVersion")
    implementation 'com.facebook.shimmer:shimmer:0.3.0'
    implementation 'com.tbuonomo.andrui:viewpagerdotsindicator:2.1.2'
    implementation 'io.branch.sdk.android:library:3.+'
    }
   ```

## Initialization
   Initialize the SDK by user's authToken.   
   Initialization of the SDK is necessary to use any functionality.
   
   ```java
     P52Poker.init(getApplicationContext(), token);
   ```

## Opening PokerRoomsActivity
   This activity contains Poker Rooms.
   
   Launch this activity in SINGLE_TASK Mode
   ```java
     Intent intent = new Intent(getApplicationContext(), PokerRoomsActivity.class);
     intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
     startActivity(intent);       
   ```
  

### P52Poker

 ```java
/**
* Pocket52 Poker SDK Main Class.
* {@note This is a singleton class which is based on Bill Pugh Singleton Implementation.
*          It's thread safe to a good extent, but doesn't guarantee single instance
*          against reflection.
* }
*/
public class P52Poker { 

      /**
     * Initializes Pocket52 Poker SDK.
     * Call this method as early as possible, preferably in your Main Application class.
     *
     * Initialization of the SDK is necessary to leverage any other functionality in the SDK.
     *
     *
     * @param context The Application Context.
     * @param p52AuthToken authToken provided by Pocket52 Game Server
     * {@note The authToken is refreshed internally, at a specified rate and cannot be configured at runtime.}
     *
     */
    public void init(Context context, String p52AuthToken)

}
```



