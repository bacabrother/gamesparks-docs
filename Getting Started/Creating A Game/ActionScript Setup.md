
# ActionScript Setup

## Introduction

The previous tutorial [Creating a Game](../Creating A Game.html), took you through the beginning steps within the GameSparks platform. Now you can move forward and link your GameSparks game with your developing ActionScript project. This tutorial will show you how to set up your ActionScript project and establish a connection between the GS module and the Portal. *Setting up Your ActionScript Project*

  * Create an ActionScript project.
  * Create a new folder for your project and name it 'lib'.
  * Download the GameSparks SWC file, drop it in the _'lib'_ folder, right click it and then Add to library.
  * Make sure you're using the latest [Adobe Flash](https://get.adobe.com/flashplayer) version.
*Using GameSparks API*

  * Import the GameSparks API.
  * Find your Service URL in the Test Harness and the Secret key in the Overview page of the Portal.
  * Make your first function which establishes a connection between the GS module and the Portal.
  * Create the Logger and Availability call back functions. These functions are necessary for debugging.
  * Build your ActionScript interface with a button to make the connection work correctly and a Logger to debug what's happening in the background.
  * Play your game and attempt to make a connection.
[wpdm_file id=33 title="true" ]

## *Setting up Your ActionScript Project*

Start by creating a project for ActionScript. For the following tutorials we will be developing a Flex 3 project.

![l](img/AS/1.png)

Create a new folder and name it _'lib'_*.*

![l](img/AS/2.png)

Download and find the* gamesparks-as3-sdk .SWC* file. Then drop the SWC file into the _'lib'_ folder.

![l](img/AS/3.png)

Make sure you add the *.SWC* file to the library by right-clicking it and selecting the '*Add to library'* option. This will allow you to use the GameSparks library for your game.
![l](img/AS/4.png)

Right-click on your game,  and from the context menu, click on *Properties* and make sure you're using the latest Flash player.
![l](img/AS/5.gif)
 

## *Using GameSparks API*

 

Import the GameSparks API as well as other libraries using:

```
import com.gamesparks.*;  
import com.gamesparks.api.messages.*;  
import com.gamesparks.api.requests.*;  
import com.gamesparks.api.responses.*;  
import com.gamesparks.api.types.*;  
import com.gamesparks.sockets.*;  
import flash.events.MouseEvent;  
import mx.controls.Alert;  
import mx.controls.TextArea;    
import flash.utils.setInterval;  
```

![l](img/AS/6.png)

The first function you will need to make allows you to connect your game to the Portal. To do this you must connect using the *service URL* and *API Secret*.You will find the* API Secret* on the Overview page.
![l](img/AS/7.png)

The *Service URL* is located in the Test Harness.
![l](img/AS/8.png)

Now you can make your first function. This uses the URL and Key to connect to the Portal. Name this function *ConnectToPortal* and initiate the connection using: gs.setAvailabilityCallback().setLogger().setUrl("").setApiSecret("").connect();

  * setAvailabilityCallback(FunctionNameHere) calls the given function when the GS module sends feedback from the connection or disconnection to the Portal.
  * setLogger(FunctionNameHere) calls the given function when the GS module sends general feedback.
  * setUrl("Url") and setApiSeret("Secret") connects the GS module to the given URL using the given Secret key.
  * connect() fires the request to connect the GS module to the Portal as well as calling the Availability call back function set and logging it.

```
    		private function ConnectToPortal():void
    			{
    				gs.setAvailabilityCallback(availabilityCallback).setUrl("wss://preview.gamesparks.net/ws/293711ZXWjA9").setApiSecret("DgnYnPUE2D0RetwKAy5XPUxxxN7pl36e").connect();
    			}
```

The second function, *Logger *will be used to debug the GameSparks logic and then check the availability of the connection to the Portal. After making them, set them for use as the Logger and *setAvailabilityCallback*.

```
    	public function logger(text:String):void
    			{
    				 logArea.text += "n" + text;
    				 logArea.scroller.verticalScrollBar.value = logArea.scroller.verticalScrollBar.maximum;
    			}

    			public function availabilityCallback(isAvailable : Boolean):void{

    				logger("availabilityCallback " + isAvailable);

    				if (isAvailable)

    				{

    				}					
    				else
    				{

    				}
    			}
```

A button has already been created to call the *ConnectToPortal* function. Once the GS module is connected to the Portal, the alert message will pop up as feedback. In the log you should see *'availabilityCallback.true'*.  

![l](img/AS/9.png)

If you set the logger using *gs.setLogger()* the log will look like this. This shows you more feedback, but it also sends a high amount of spam to the Logger.  

![l](img/AS/10.png)