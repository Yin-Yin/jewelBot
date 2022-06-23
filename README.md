# Jewel bot
A python script/bot/"ai" that plays match 3 games (Microsoft Jewels (classic), Bejeweled, Candy Crush, etc.)

The bot is optimized for this game (works best when it is dragged to half of the screen on a 16:10 display): Microsoft Jewels (Classic) found for example here https://games.ca.zone.msn.com/gameplayer/gameplayerHTML.aspx?game=msjewel or here https://kizi.com/games/microsoft-jewel 

It also works more or less with these games (although it was not optimized for them):
- https://www.match3games.com/game/Flat+Jewels (works pretty well, as the jewels are flat, can misinterpret some though)
- https://www.1001games.com/match-3/aquablitz (works quite well)
- https://www.match3games.com/game/Jewel+Monsters (works roughly)
- https://kizi.com/games/jewel-shuffle (should work better though)
- https://games.ca.zone.msn.com/gameplayer/gameplayerHTML.aspx?game=msjewelnew (not optimal as it can't click on the "next level" button and can not deal with the empty rows)
- https://arcadespot.com/game/bejeweled-hd/ (could work better)

# Requirements
- Python3
- Windows (AFAIK pyautogui, which is used for detecting the game area and clicking needs Windows, these can be replaced however)

Following external dependencies need to be installed (just install them with pip, for example `pip install pyautogui`)
- `numpy`
- `pyautogui`
- `PIL`
- `cv2`
- `keyboard`
- `mouse`

# Usage
You need to have the game open in a browser for the bot to detect it. Then have a command window open and run the script by typing `python2 jewels.py`. 
IMPORTANT: To quit the script, keep `q` pressed (hint: keep it pressed for one or two seconds for it to work) or move the mouse into one of the corners (this will trigger the pyautogui failsafe). (or if you are quick engough go to the console and press `ctrl + c`)

There are a few settings on top of the script (under `# CONFIG`) that can be used to change the bots behaviour and make it work with different games. 

The script can try to find the game area by finding the upper left and lower right corners of the game area. There are two screenshots in this folder, that it is looking for in the screen. They are `region_lower_right_corner.png` and `region_upper_left_corner.png`. As the background is different if the window is somewhere else, you might need to redo the screenshots. If it fails the program will ask you to place the mouse on these points to get the position. 
![jewels_game_state_corners](https://user-images.githubusercontent.com/13853689/174763686-90956574-cc0b-46c6-81f5-3e80f097cb27.png)

For debugging and to see where the programm takes it's color values from, put the `showBoardScreenshot = False` to `True`.

# How it works
- Determine the game area
- Get the colors from pixels of the objects 
- Match the RGB values to "colors"
- Get all the possible combinations on the board
- Choose the first move which affects the most jewels

# Improvements
So far the bot simply makes the first move that includes the most jewels. 
To get a higher score, these steps could be done: 
    - Improve the auto detection of colors by adding plus/minus a certan amounut of RGB values to get approximately the same color and match these.
    - Microsoft Jewels (Classic): Check the upper area for which jewels are there (these multiplier jewels) and then select the move which includes this color. 
    Implementation: should be fairly easy, as the colors are already in the dict with all possible moves, just need to determine which colors are needed
    - Microsoft Jewels (Classic): The bot cannot detect these special jewels that you get when you combine 5 in a row and which remove all of the jewels of the same color. That is a big point where it could be improved. Even better, choose these black, glowing ones to exchange it with. 
    Implementation: this would need more image recognition capabilities, as currently the bot sees them just as white


Generally the recognition of the board and the colors is not yet working in a lot of cases, this could be improved.

# Known Bugs
- can't detect these jewels that remove all of the same color. Sees them as white, which can result in the programm not continuing. 
- When 6 (?) jewels are combined there is a new jewel that glows very white in the middle. The programm cannot detect it, as it is white inside.
- Sometimes the color detection can be tricky. It helps to have the `showBoardScreenshot = False` set to `True` to see where the colors are taken from. 

# 
