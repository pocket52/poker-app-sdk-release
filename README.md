# Pocket52 Poker SDK Docs

This Document contains POCKET 52’s POKER SDK’s Documentation.


### P52Poker

 ```java
/**
* Pocket52 Poker SDK Main Class.
* {@note This is a singleton class which is based on Bill Pugh Singleton Implementation.
*          It's thread safe to a good extent, but doesn't guarantee single instance
*          against reflection.
* }
*/
public class P52Poker { ... }
```

### Initialize SDK 

Call this method as early as possible, preferably in your Main Application class

 ```java
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
public void init(String p52AuthToken)
```


## LobbyPresenter
Can be injected or initialized

Presenter to fetch lobby data (listings, wallet balance, etc).

 ```java

/**
* {@link BaseLobbyUsecase<PokerRoomsEntity>} to fetch Poker Rooms 
* from Game Server
*
* This usecase is executed on {@link Schedulers#newThread()}
*
* This usecase calls the following callbacks for view:
*
* {@link View#onPokerRoomsSuccess(ArrayList)}
* {@link View#onPokerRoomsError(String)}
* 
* The callbacks are received on AndroidSchedulers#mainThread()
*/
public void getPokerRooms()

/**
* {@link BaseLobbyUsecase<UserBalances>} to fetch User Wallet Balances
*
* This usecase is executed on {@link Schedulers#newThread()}
*
* This usecase calls the following callbacks for view:
*
* {@link View#onUserBalanceSuccess(UserBalances)}
* {@link View#onUserBalanceError(String)}
*
*/
public void getUserBalances()

/**
* Opens a Table inside PokerGame.
*
* @param config TableConfig Entity
*/
public void openTable(final TableConfig config)

/**
* Allots a Table in a PokerRoom.
*
* @param entity PokerRoom Entity Model
*/
public void allotTable(final PokerRoomsEntity entity)

```


### LobbyPresenter.View

 ```java
/**
* LobbyPresenter View Interface.
* Used to communicate with the attached view for 
* corresponding usecase callbacks.
*/
public interface View extends LobbyBasePresenter.View {
   /**
    * Success Callback for {@link #getPokerRooms()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param tables ArrayList of {@link PokerRoomsEntity} models, comprising of available Poker Rooms.
    */
   void onPokerRoomsSuccess(ArrayList<PokerRoomsEntity> tables);

   /**
    * Error Callback for {@link #getPokerRooms()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param error returned error message.
    */
   void onPokerRoomsError(String error);

 /**
    * Success Callback for {@link #allotTable()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param config Config of the Alloted Table.
    */
   void onAllotTableSuccess(TableConfig config);

 /**
    * Error Callback for {@link #allotTable()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param error returned error message.
    */
   void onAllotTAbleError(String error);

    /**
    * Success Callback for {@link #getUserBalances()} ()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param data User's Poker Wallet Balances.
    */
    void onUserBalanceSuccess(UserBalances data);

    /**
    * Error Callback for {@link #getUserBalances()}
    * This Callback is received on {@link AndroidSchedulers#mainThread()}
    *
    *
    * @param error returned error message.
    */
    void onUserBalanceError(String error);

}


```

### IGameLifecycleListener

 ```java
 /**
* Poker Game Life Cycle Listener.
*
*/
public interface IGameLifecycleListener {

   /**
    * Called when the Game is Created for the first time.
    */
   void onGameCreated();

   /**
    * Called when the Game is paused.
    * This callback ensures the glContext has been detached for sure, in cases of:
    * App background/Foreground switch
    * Screen Lock/Unlocks
    * PIP Transformations
    *
    * {@note This is different from Android Activity#onPause()}
    */
   void onGamePaused();

   /**
    * Called when the Game is resumed.
    * This callback ensures the glContext has been re-attached for sure, in cases of:
    * App background/Foreground switch
    * Screen Lock/Unlocks
    * PIP Transformations
    *
    * {@note This is different from Android Activity#onResume()}
    */
   void onGameResumed();

   /**
    * Called when the Game is disposed.
    * This callback ensures all the textures used in Game to be disposed of.
    *
    *
    * {@note This method takes time to execute}
    */
   void onGameDisposed();
}

 
```




