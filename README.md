All the screens are located in the scenes directory.

Sign Up screen allows to choose an avatar from prebuilt models. Then the user is prompted to enter his email and choose username and password to sign up. After successful registration login screen is loaded. The behavior of this screen, as well as GUI, is managed using SelectCharStyled script 

Login screen is created by the script LoginScene located in the Script directory.
All account settings are stored on the Parse server. 
When performing login, current user settings are being downloaded from the Parse server 
and saved locally in user preferences.

Next, user enters the main menu screen; this scene is created by scripts/MainMenuGUI script.
Menu options are created as buttons and not menu items for better UI.
From the main menu user can either logout, or explore other screens. (Some are not finished, and "under construction" scene loads instead.)

----------------------------------------------------------------------------------------------------
											THE MAIN SCENE
----------------------------------------------------------------------------------------------------
For this scene a mall with two floors was developed.
On the first floor there is a cinema hall, one the second one - a restaurant ("Cafe Cafe"),
a cloth shop ("D&G") and a book store ("Camus"). All 3d models used for the mall are
located in the Mall directory, most of them use ready meshes. Textures and materials can be found in
Textures, Materials and MyTextures directories. 
The main scene is managed by GameManager script which can be found in the Script/Network directory.
This script is based on a Badumna game manager template for use in a Badumna-enabled Unity game. 
Badumna provides network services for multiplayer games: chat, updating of players' position and 
orientation etc. GameManager script performs player settings initializations and loads the Network 
script located in  Script/Network/Network.cs. Network script performs login to the Bodumna cloud 
(using ID PCSVN) and registers all replicable properties (player position, orientation, and animation). 

Then Network script joins the local player into the main scene.
(network state is updated regularly and passed to Badumna)
On this step the Scene script is invoked (Script/Network/Scene.cs). This script contains two
important methods for creating the local player and remote players. These methods are called by Badumna.
Players are represented by the Script/Network/Player script. Players have avatar configuration string,
position and orientation within the main scene (replicable entities), the scene they belong to and
animation controller. Animation controller is a script (Script/Network/ThirdPersonSimpleAnimation),
used for updating players animations depending on speed (now it supports walk, idle and run).

NOTES:
*	Currently animations used within the scene are not integrated.
	Animations are switched in the Script/Network/CharacterController/ThirdPersonController 
	and in the Script/Network/ThirdPersonSimpleAnimation scripts and defined on avatar prefabs
*	Currently camera doesn't follow the avatar.
*	Joystick is not integrated as well.

USAGE:
* 	To see the world using a prebuilt avatar run Mall.exe from the desktop 
* 	To see ExploreWorld screen from Android run IIMe-MainScene.apk (user "mos", password "mos")
* 	To view the project install unity, create a new project and copy all the files except to
	apk to the Assets folder.

----------------------------------------------------------------------------------------------------
								THE AVATAR CUSTOMIZATION SCENE
----------------------------------------------------------------------------------------------------
The main scene for customizing the avatar.

To implement it I've tried to create my own avatars, then used Mixamo pack, but then had problems created my own overlays/slots libraries.

For the lack of time(*) I decided to integrate UMA plugin, and wrote my own customization script, which implements custom GUI and behavior (including custom load/save and changing overlays). Avatar animator was changed as well.

There is still a minor bug in mesh renderers while changing shape after changing textures.
Another thing is that because of disintegration, I always load a prefab for not having prefs.

I put 2 apk for both Mixamo and UMA packs. Each has its pros and cons.

Additional documentation is available in comments through the code.

Initially we integrated Google analytics plugin, but later decided to remove it, as the application is disintegrated.

As free version of Unity was used, no assets bundles, LOD, and occlusion were available to improve performance. 

 -- UMA version is in GIT_Android directory, 2 APKs for Mixamo and UMA sign-up, main menu, and customizations are there too. Another APK file for explore world screen is in IIMe-APKs.
