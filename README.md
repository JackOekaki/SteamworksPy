# SteamworksForPython
Howdy!  This is a branch of Easimer's SteamworksForPython in an attempt to bring a fully-functional Python module for Steam out for the public.

Feel free to fork or contribute to this module.

# Some Notes
While I am still tinkering away with this, here are some things to note:

- You will need the Steamworks SDK
- You will most likely need a Steamworks account, with a valid AppID, to use more advanced functions (set achievements, set stats, etc.)
- You will need to be logged into Steam for anything to function, obviously.  As it assumes the game is run from Steam itself and is online.

# To Do
- Add in more features from the Steamworks SDK
- Create a Mac version

# How To
1. Download this repo and unpack
2. Download and unpack the Steamworks SDK
3. Move the Steam header (steam) folder from /sdk/public/ into the unpacked repo for compiling
4. Move the Steam API file from /sdk/redistributable_bin into the unpacked repo
  - For Linux, find libsteam_api.so
  - For Windows, find steam_api.dll or steam_api64.dll as well as steam_api.lib or steam_api64.lib
5. Create the new DLL or SO file
  - For Linux:
    - Run the makefile from the repo
    - Alternately, you could just run something like gcc -o SteamworksPy.so -shared -fPIC steampy.cpp -lsteam_api
  - For Windows:
    - Create a new DLL project in Visual Studio
    - New > Project
    - Templates > Visual C++ > Win32 > Win32 Project
    - Follow the wizard and pick the DLL Application Type
    - Add steampy.cpp to Source Files and steam_api.h from /steam/ folder to Header Files
    - Go to Project > Properties in the toolbar
    - Under C/C++ > Precompiled Headers, turn off Precompiled Header option
    - Under Linker > Input, add steam_api.lib or steam_api64.lib to Additional Dependenices
    - Clean and build
6. Move the steamworks.py and new compiled SteamworkPy.so or SteamworksPy.dll from the unpacked repo into your project
  - You may also want to move over the libsteam_api.so as well
7. Add the following to your to your main file or whichever file you plan on calling Steam from:
```
from steamworks import *
#Initialize Steam
Steam.Init()
```
From here you should be able to call various functions of the steamworks.py.  A list of available functions is listed below; take a closer look at the steamworks.py for a better understanding.  In addition, you should be able to read the Steamworks API documentation to see what all is available and cross-reference with the steamworks.py!

# Features / Functions
1. Init()
  - Starts up the Steam API
2. GetDLCCount()
  - Get the total number of DLC installed for this game
3. IsDlcInstalled()
  - Is a particular DLC installed for this game
  - You must pass the DLC's AppID
4. GetFriendCount()
  - Get the number of friends the user has
5. GetPlayerName()
  - Get the user's name
6. GetPersonaState()
  - Get the user's current state
7. IsEnabled()
  - Check whether or not Steam Music is enabled
8. IsPlaying()
  - Is Steam Music currently playing something
9. GetVolume()
  - Get the system's current volume level
10. Pause()
  - Pause whatever Steam Music is playing currently
11. Play()
  - Play whatever track Steam Music is on
12. PlayNext()
  - Play the next track in Steam Music
13. PlayPrevious()
  - Play the previous track in Steam Music
14. SetVolume()
  - Set the system's volume
  - Must pass a float between 0.0 and 1.0
15. GetPlayerID()
  - Get the user's Steam ID number
  - Currently just returns 0
16. ClearAchievement()
  - Clear the specified achievement from the user
  - Must pass achievement's name in Steam (eg. STEAM_ACHIEVE_1)
17. GetAchievement()
  - Find whether or not the specified achievement is earned
  - Must pass achievement's name in Steam (eg. STEAM_ACHIEVE_1)
18. GetStatFloat()
  - Get value of specified float statistic
  - Must pass statistic's name in Steam (eg. TOTAL_GAMES)
19. GetStatInt()
  - Get value of specified integer statistic
  - Must pass statistic's name in Steam (eg. TOTAL_GAMES)
20. ResetAllStats()
  - Resets all of the user's statistics, perhaps also achievements
21. RequestCurrentStats()
  - Pulls all of the user's statistics and achievements
  - Should be called before calling any Get stats/achievement functions
22. SetAchievement()
  - Set a particular achievement for the user
  - Must pass achievement's name in Steam (eg. STEAM_ACHIEVE_1)
23. SetStat()
  - Set a particular statistic for the user
  - Must pass statistics's name and value in Steam (eg. TOTAL_GAMES, 4)
24. StoreStats()
  - Sends all the statistics and achievements to Steam servers
25. GetCurrentBatteryPower()
  - Get the user's battery power level
26. GetIPCountry()
  - Get the two-digit code for the user's IP address
27. GetSecondsSinceAppActive()
  - Get the number of seconds since the game started up
28. GetSecondsSinceComputerActive()
  - Get the number of seconds since the user's computer was started
29. GetServerRealTime()
  - Get the time from the server, probably
30. IsOverlayEnabled()
  - Is the Steam overlay enabled
31. IsSteamRunningInVR()
  - Is Steam's VR service running

# More To Come
I am still digging through the code and trying to get more functions like setting achievements and stats, but these definitely require a Steamworks account and AppID.  Without your game on Steam, I don't think you can really use those functions but I haven't actually tested it yet.  Some things like controller might not be necessary as Python can usually handle these; though they may have more to do with the new Steam Controller.  Some functions in the API are more complicated and I cannot seem to get them functioning.
