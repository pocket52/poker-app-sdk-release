# Pocket52 Poker SDK Docs

This Document contains POCKET 52’s POKER SDK’s Documentation.

### Setup

This SDK requires a user auth key to be run.

## Initialization
   Initialize the SDK by user's authToken.   
   Initialization of the SDK is necessary to use any functionality.
   
     ```java
     P52Poker.init(token);
     ```

## Opening PokerRoomsActivity
   This activity contains Poker Rooms.
   
   Launch this activity in SINGLE_TASK Mode
   ```java
     Intent intent = new Intent(getApplicationContext(),A.class);
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
     * @param p52AuthToken authToken provided by Pocket52 Game Server 
     * {@note The authToken is refreshed internally, at a specified rate and cannot be configured at runtime.}
     *
     */
     public void init(String p52AuthToken);

}
```



