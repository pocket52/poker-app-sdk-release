![unnamed](https://user-images.githubusercontent.com/66310516/90481524-8c41a600-e14f-11ea-8f97-785327478df4.png)
# Pocket52 Poker SDK Docs for Unity Plugin

This Document contains POCKET 52’s POKER SDK’s Documentation with Unity Plugin.

Please go to [Releases](https://github.com/pocket52/poker-app-sdk-release/releases) to be updated with the latest version of the client.

### Setup

1. Download Poker SDK (.aar file) and Dependencies (.jar / .aar) files
2. Create an "Android" folder. (Path:  Client-Project/Assets/Plugin/Android)
3. Insert the .aar file into your Android folder. 
4. Extract the dependencies folder and find all files
5. Insert all the dependencies files (all .jar / .aar files) into your Android folder.
6. Initialize Poker SDK with help of the init() function of "P52Poker" class.
7. To open Poker Rooms call openPokerRooms() function of "P52Poker" class.
8. To close Poker Rooms call closePokerRooms() function of "P52Poker" class.





### Dependencies 

Download and extract all the dependencies and insert them into Android folder. (Path:  Client-Project/Assets/Plugin/Android)




### Initialization
   The initialization of the SDK is necessary to use any functionality.
   
   ```java
     //Java Code
     P52Poker.get().init(config);
     
   ```
   ```C#
      //C# Code
      
      // Declaration
      AndroidJavaClass pokerClass;
      AndroidJavaObject pokerObject;
      AndroidJavaObject configObject;
      IPokerListener listener;  //IPokerListener is a local class which inherits SDK IPokerListener interface
      
      //Initialization 
      pokerClass = new AndroidJavaClass("com.pocket52.application.P52Poker");
      pokerObject = pokerClass.CallStatic<AndroidJavaObject>("get"); 
      listener = new IPokerListener();
      
      //Find Application Context
      AndroidJavaClass unityPlayer = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
      AndroidJavaObject activity = unityPlayer.GetStatic<AndroidJavaObject>("currentActivity");
      AndroidJavaObject context = activity.Call<AndroidJavaObject>("getApplicationContext");
      
      //find auth token from API and share with SDK
      string token = "user auth-token sample String";
      
      //Mode is an enum, for Stage/PP use TEST and for Production use PROD
      AndroidJavaObject mode = new AndroidJavaClass("com.pocket52.application.MODE").GetStatic<AndroidJavaObject>("TEST");
      
      //Initialization of Config Object
      configObject = new AndroidJavaObject("com.pocket52.application.Config", context, token, mode, listener);
      
      pokerObject.Call("init", configObject);
   
   ```
   
   ```C#
   //C# Code (Create a local IPokerListener class)
   
   /**
       * 
       * {@note this Class will be managed by Client to handle the SDK errors, all the errors are constant.
       *      Client will be notified by onError() callback. 
       *      Client will get the name of errors with help of [error.Call<string>("name")].
       * }
   */
   public class IPokerListener : AndroidJavaProxy {

	//Replace with full Java name for IPokerListener interface
     public IPokerListener() : base("com.pocket52.application.IPokerListener") { }
     

     public void onError(AndroidJavaObject error) {
     	Debug.Log("P52Poker  onError(): " );
     	Debug.Log("P52Poker  onError(): " + error.Call<string>("name") );
     }
}
   
   ```
   
   
   
   

## Opening PokerRooms
   ```java
   //Java Code
     P52Poker.get().openPokerRooms();       
   ```
   
   ```C#
   //C# Code
   pokerObject.Call("openPokerRooms");
   ```
   
   

## Closing PokerRooms
This will close Poker Rooms Activity, Game View Activity and call disposeToken()
   ```java
   //Java Code
     P52Poker.get().closePokerRooms();       
   ```
   ```C#
   //C# Code
   pokerObject.Call("closePokerRooms");
   ```
   

## DisposeToken
   ```java
   //Java Code
     P52Poker.get().disposeToken();       
   ```
   ```C#
   //C# Code
      pokerObject.Call("disposeToken");
   ```




### Proguard Rules 

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
     * @param assetsDirectoryName (Optional/Madatory) path Madatory if assets are not in SDK
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
     * @param pokerListener (Mandatory) to listen about Poker Activity
     */
    public Config(Context context, String authToken, MODE mode, IPokerListener pokerListener) {
        this(context, authToken, mode, null, null, pokerListener);
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


    public IPokerListener getPokerListener() {
        return pokerListener;
    }

    public String getFtueUrl() {
        return ftueUrl;
    }

    public String getAssetsDirectoryName() {
        return assetsDirectoryName;
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

###




