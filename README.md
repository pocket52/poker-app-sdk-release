![unnamed](https://user-images.githubusercontent.com/66310516/90481524-8c41a600-e14f-11ea-8f97-785327478df4.png)
# Pocket52 Poker SDK Docs

This Document contains POCKET 52’s POKER SDK’s Documentation.

Please go to [Releases](https://github.com/pocket52/poker-app-sdk-release/releases) to be updated with the latest version.

### Setup

Import the .aar file into your android project using.. File-->New Module-->Aar project 

Ensure applicationId in defaultConfig in your main app build.gradle

```java
defaultConfig {
       applicationId "your package name"
     .
     .
     .
}
```

## Dependencies

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
        implementation "com.badlogicgames.gdx:gdx-freetype:$gdxVersion"
        natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-armeabi"
        natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-armeabi-v7a"
        natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-arm64-v8a"
        natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-x86"
        natives "com.badlogicgames.gdx:gdx-freetype-platform:$gdxVersion:natives-x86_64"
        implementation 'com.jakewharton.rxrelay2:rxrelay:2.1.0'
        implementation "io.reactivex.rxjava2:rxandroid:$rxandroidVersion"
        implementation "io.reactivex.rxjava2:rxjava:$rxjavaVersion"
        implementation "com.amitshekhar.android:android-networking:$androidNetworkingLibVersion"
        implementation "com.amitshekhar.android:rx2-android-networking:$androidNetworkingLibVersion"
        implementation("com.android.support:recyclerview-v7:$supportLibVersion") {
            force true
        }
        implementation 'com.android.support.constraint:constraint-layout:1.1.3'
        implementation "android.arch.lifecycle:extensions:1.1.1"
        implementation "android.arch.lifecycle:viewmodel:1.1.1"
        implementation('io.socket:socket.io-client:0.8.3') {
            // excluding org.json which is provided by Android
            exclude group: 'org.json', module: 'json'
        }
        annotationProcessor 'com.bluelinelabs:logansquare-compiler:1.3.6'
        implementation 'com.bluelinelabs:logansquare:1.3.6'
        implementation("com.android.support:design:$supportLibVersion") {
            force true
        }
       
    }
   ```
   
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


## Proguard Rules 

```java
    
#region SDK rules
-verbose

-dontwarn android.support.**
-dontwarn com.badlogic.gdx.backends.android.AndroidFragmentApplication
-dontwarn com.badlogic.gdx.utils.GdxBuild
-dontwarn com.badlogic.gdx.physics.box2d.utils.Box2DBuild
-dontwarn com.badlogic.gdx.jnigen.BuildTarget*
-dontwarn com.badlogic.gdx.graphics.g2d.freetype.FreetypeBuild

-keep class com.badlogic.gdx.controllers.android.AndroidControllers
-keep class com.badlogic.gdx.backends.android.AndroidApplication
-keep class com.badlogic.gdx.backends.android.AndroidApplicationConfiguration
-keep class com.pocket52.application.P52Poker
-keep class com.pocket52.helper.NumberFormatter
-keep class com.pocket52.hld.table.IGameLifecycleListener


-keepclassmembers class com.pocket52.application.P52Poker {
   void    init(com.pocket52.application.Config);
   com.pocket52.application.P52Poker    get();
   void    disposeToken();
   void    openPokerRooms();
   void    closePokerRooms();
}

-keep class com.pocket52.application.Config {
*;
}
-keep class com.pocket52.application.IPokerListener {
*;
}
-keep class com.pocket52.application.ERROR {
*;
}
-keep class com.pocket52.application.MODE {
*;
}
-keep class com.pocket52.application.PrivateTableInfo {
*;
}

-keepnames class com.badlogic.gdx.backends.android.AndroidInput*
-keepclassmembers class com.badlogic.gdx.backends.android.AndroidInput* {
   <init>(com.badlogic.gdx.Application, android.content.Context, java.lang.Object, com.badlogic.gdx.backends.android.AndroidApplicationConfiguration);
}

-keepclassmembers class com.badlogic.gdx.physics.box2d.World {
   boolean contactFilter(long, long);
   void    beginContact(long);
   void    endContact(long);
   void    preSolve(long, long);
   void    postSolve(long, long);
   boolean reportFixture(long);
   float   reportRayFixture(long, float, float, float, float, float);
}
#endregion

#region okHttp rules (used by picasso)
# JSR 305 annotations are for embedding nullability information.
-dontwarn javax.annotation.**

# A resource is loaded with a relative path so the package of this class must be preserved.
-keepnames class okhttp3.internal.publicsuffix.PublicSuffixDatabase

# Animal Sniffer compileOnly dependency to ensure APIs are compatible with older versions of Java.
-dontwarn org.codehaus.mojo.animal_sniffer.*

# OkHttp platform used only on JVM and when Conscrypt dependency is available.
-dontwarn okhttp3.internal.platform.ConscryptPlatform
#endregion

#region LoganSquare
-keep class com.bluelinelabs.logansquare.** { *; }
-keep @com.bluelinelabs.logansquare.annotation.JsonObject class *
-keep class **$$JsonObjectMapper { *; }
#endregion

#region Branch
-dontwarn com.android.installreferrer.api.**
-dontwarn com.crashlytics.android.answers.shim.**
-dontwarn com.google.firebase.appindexing.**
#endregion
-keep class android.arch.** { *; }

```


## Initialization
   Initialization of the SDK is necessary to use any functionality.
   
   ```java
     P52Poker.get().init(config);
   ```

## Opening PokerRooms
   ```java
     P52Poker.get().openPokerRooms();       
   ```

## Closing PokerRooms
This will close Poker Rooms Activity, Game View Activity and call disposeToken()
   ```java
     P52Poker.get().closePokerRooms();       
   ```

## DisposeToken
   ```java
     P52Poker.get().disposeToken();       
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
     */
    public void init(Config config);

    /**
     * Opens Poker Rooms Activity in a NEW TASK
     */
    public void openPokerRooms();
    
    /**
     * Closes Poker Rooms Activity, Games View Activity and calls disposeToken()
     */
    public void closePokerRooms();
    
    /**
     * Dispose P52 User Auth Token
     */
    public void disposeToken();
}
  ```

### Config

 ```java

/**
 * {@code P52Poker SDK Config class, used for initialization}
 *
 * @author Name:    Romi Chandra,
 * Company: Nirdesa Networks Pvt Ltd,
 * Email:   romi@pocket52.com.
 * @version 1.0
 * @since 04, December, 2019
 */
public class Config {

    private String assetsDirectoryName;

    /**
     * Application Context
     */
    private Context context;

    /**
     * P52 User Auth Token
     */
    private String authToken;

    /**
     * Mode to run on TEST/PROD servers
     */
    private MODE mode = MODE.TEST;

    /**
     * FTUE Url
     */
    private String ftueUrl;


    /**
     * SDK Events Listener
     */
    private IPokerListener pokerListener;

    /**
     * Private Table Information
     * This is for deep links, which helps to join the Private Table.
     * Optional
     */
    private PrivateTableInfo privateTableInfo;


    /**
     * @param context (Mandatory) Application Context
     * @param authToken (Mandatory)
     * @param mode (Mandatory) Mode to run on TEST/PROD servers
     * @param ftueUrl (Optional/Mandatory) Mandatory if we need to show FTUE from SDK
     * @param assetsDirectoryName (Mandatory)
     * @param pokerListener (Mandatory) to listen about Poker Activity
     */
    public Config(Context context, String authToken, MODE mode, String ftueUrl, String assetsDirectoryName, IPokerListener pokerListener) {
        this.context = context;
        this.authToken = authToken;
        this.mode = mode;
        this.ftueUrl = ftueUrl;
        this.pokerListener = pokerListener;
        this.assetsDirectoryName = assetsDirectoryName;
    }

    /**
     * @param context (Mandatory) Application Context
     * @param authToken (Mandatory)
     * @param mode (Mandatory) Mode to run on TEST/PROD servers
     * @param ftueUrl (Optional/Mandatory) Mandatory if we need to show FTUE from SDK
     * @param assetsDirectoryName (Mandatory)
     * @param pokerListener (Mandatory) to listen about Poker Activity
     * @param privateTableInfo (Optional/Mandatory) pass the private table Info to join the table
     */
    public Config(Context context, String authToken, MODE mode, String ftueUrl, String assetsDirectoryName, IPokerListener pokerListener, PrivateTableInfo privateTableInfo) {
        this.context = context;
        this.authToken = authToken;
        this.mode = mode;
        this.ftueUrl = ftueUrl;
        this.pokerListener = pokerListener;
        this.assetsDirectoryName = assetsDirectoryName;
        this.privateTableInfo = privateTableInfo;
    }

    public Config (Config config) {
        this.context = config.context;
        this.authToken = config.authToken;
        this.mode = config.mode;
        this.pokerListener = config.pokerListener;
        this.ftueUrl = config.ftueUrl;
        this.assetsDirectoryName = config.assetsDirectoryName;
        this.privateTableInfo = config.privateTableInfo;
    }

    public Context getContext() {
        return context;
    }

    public void setContext(Context context) {
        this.context = context;
    }

    public MODE getMode() {
        return mode;
    }

    public void setMode(MODE mode) {
        this.mode = mode;
    }

    public String getAuthToken() {
        return authToken;
    }

    public void setAuthToken(String authToken) {
        this.authToken = authToken;
    }

    public IPokerListener getPokerListener() {
        return pokerListener;
    }

    public String getFtueUrl() {
        return ftueUrl;
    }

    public void setFtueUrl(String ftueUrl) {
        this.ftueUrl = ftueUrl;
    }

    public void setPokerListener(IPokerListener pokerListener) {
        this.pokerListener = pokerListener;
    }

    public String getAssetsDirectoryName() {
        return assetsDirectoryName;
    }

    public void setAssetsDirectoryName(String assetsDirectoryName) {
        this.assetsDirectoryName = assetsDirectoryName;
    }

    public PrivateTableInfo getPrivateTableInfo() {
        return privateTableInfo;
    }

    public void setPrivateTableInfo(PrivateTableInfo privateTableInfo) {
        this.privateTableInfo = privateTableInfo;
    }
}

```

### PrivateTableInfo

 ```java

/**
 * {@code P52Poker SDK Config class, used for initialization}
 *
 * @author Name:    Nikhil Rai,
 * Company: Nirdesa Networks Pvt Ltd,
 * @version 1.0
 * @since 04, December, 2019
 */
public class PrivateTableInfo {
    private String privateTablePin;
    private String pvtOwnerId;
    private String pvtExpiryDate;

    /**
     * @param privateTablePin is a pin which helps player to join the Private Table.
     */
    public PrivateTableInfo(String privateTablePin) {
        this(privateTablePin, null, null);
    }

    /**
     * @param privateTablePin is a pin which helps player to join the Private Table.
     * @param privateTableOwnerName Name or ID of player, who generated private Table.
     */
    public PrivateTableInfo(String privateTablePin, String privateTableOwnerName) {
        this(privateTablePin, privateTableOwnerName, null);
    }

    /**
     * @param privateTablePin is a pin which helps player to join the Private Table.
     * @param privateTableOwnerName Optional : Name or ID of player, who generated private Table.
     * @param privateTableExpiryDate Optional : pass expiry date if we need to show on UI.
     */
    public PrivateTableInfo(String privateTablePin, String privateTableOwnerName, String privateTableExpiryDate) {
        this.privateTablePin = privateTablePin;
        this.pvtOwnerId = privateTableOwnerName;
        this.pvtExpiryDate = privateTableExpiryDate;
    }

    public String getPrivateTablePin() {
        return privateTablePin;
    }

    public String getPvtOwnerId() {
        return pvtOwnerId;
    }

    public String getPvtExpiryDate() {
        return pvtExpiryDate;
    }
}

 ```

### Errors

Following errors are passed through onError callback of IPokerListener.java

 ```java

public enum ERROR {
    INSUFFICIENT_BALANCE,
    INVALID_TOKEN,
    INVALID_APPLICATION_CONTEXT,
    INVALID_MODE,
    LOGGED_OUT,
    IDLE_LOBBY,
    EXIT_LOBBY,
    LOBBY_DESTROYED
}

```




