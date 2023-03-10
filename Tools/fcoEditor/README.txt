------------------------------------------------------------------
-------------fcoEditor User Manual - by brianuuu 2019-------------
------------------------------------------------------------------

fcoEditor is a program to modify fco files used for subtitles in Sonic Generations (does not support Sonic Unleashed). This program aims to provided a fast, easy and intrusive method to modify fco files. If you find any bugs, please DM brianuuuSonic on discord.

Updates:
v1.1
-Added file drop to exe, drop to opened program and default app

v2.0
-Added sub-tool Event Caption Editor to edit .cap file from Sonic Generations

v3.0
-Added Font Texture Generator, this allows creating new characters using custom font or edit existing font

-----------------------------------------------------------------
TL;DL Instructions
-----------------------------------------------------------------
1. Open your .fco file
2. Use "Find" to search for subtitle or double-click to edit a subtitle
3. Edit the subtitle and press "Apply Changes" when you are done
4. File->Save/Save As to save your file


-----------------------------------------------------------------
Full Application Detail
-----------------------------------------------------------------
New Group: Add a new group at the buttom of the file
Delete Current Group: Delete current selected group
Move Group Up & Down: Shift current group up or down
(WARNING: Delete or moving will affect SerifuID, use them at your own risk)

New Subtitle: Add a new subtitle at the buttom of the current selected group
Delete Current Subtitle: Delete current selected subtitle
Move Subtitle Up & Down: Shift current subtitle up or down
(WARNING: Delete or moving will affect SerifuID, use them at your own risk)

Subtitle Tree View:
-You can view all the fco structure here
-SerifuID is the ID referenced by and only relevant to Omochao, other subtitles doesn't use this so you can hide the ID if you want
-Double-click on the subtitle to start editing

Searching:
-Searching is case sensitive
-You can search from the top or the current selected subtitle
-When typing a new search keyword it will auto change to search from top

Group & Subtitle Name:
-Once a subtitle is selected, you can edit the subtitle name and the name of the group it belongs to
-Upon editing, the changes will automatically apply

Main Subtitle Editor:
-Edit your subtitle here, you can check the full list of supported characters in fcoDatabaseRAW.txt
-If there are unsupported characters, the status bar will warn you about it, if you want to know how to add unsupported characters, read the instructions below
-For special characters like A,B,X,Y,LT,RT,Start,Back etc, you must encapsulate with two backslashes, \A\, \Start\ etc, you can check all the supported special characters in fcoDatabase.txt
-When finish editor, make sure you press the "Apply Changes" button otherwise the changes won't apply

Color Blocks & Default Color:
-Default color is the color used for the entire subtitle
-Change the color by clicking on the color box
-You can add as many color blocks as your want
-You can change the alpha, start and end position by dragging up or down
-Shift color blocks order by pressing the up/down button
-Delete a color block by pressing the X button
-Hardcoded color is the default color used depending on the background, Omochao uses black BG so the hardcoded color is white, whlist HUB messages have white background so the hardcoded color is black

Subtitle Preview Box:
-You can see the immediate preview when you do any changes, incliding color blocks
-If the subtitle has more than 2 rows it will switch to black text, it assumes this is not an Omochao subtitle


-----------------------------------------------------------------
Adding Unsupported Characters (OUTDATED)
-----------------------------------------------------------------
THIS SECTION IS OUTDATED, PLEASE USE FONT TEXTURE GENERATOR!

Applications required: 
-HxD (with data inspector)
-GIMP 2.0 (with dds plugin)
-FOT-SeuratPro-B.oft (provided)
-Generations Archive Editor (download from Sonic Retro)

1. Editing fcoEditor database:
-Open fcoDatabase.txt, add a new character at the end "XX XX XX XX = Y", you must follow the exact format with the spacings

2. Updating font texture:
-Extract disk/bb2/ConverseCommon.ar.00
-Open All_002.dds with GIMP 2.0
-Use FOT-SeuratPro-B font, size 22x and white color, add the new character in empty space, for kanji I suggest you to line up with the column and row
-File->Overwrite the original file and keep the file open

3. Updating All.fte
-Open All.fte with HxD, set byte order to Big endian, set displaying 24 bytes per row
-Add one to offset 0x68 (4 bytes), this is the total number of characters
-Goto the end of file, copy one row above (0x18 bytes)
-Format "AA AA AA AA BB BB BB BB CC CC CC CC DD DD DD DD EE EE EE EE FF FF 00 15"
-AA AA AA AA: Texture ID, All_002.dds should be 00 00 00 02
-BB BB BB BB: Left pixel percentage
-CC CC CC CC: Top pixel percentage
-DD DD DD DD: Right pixel percentage
-EE EE EE EE: Bottom pixel percentage
-These four are pixel percetage in FLOAT, you can check them by selecting an area in GIMP 2.0 and change the display to percentage to view the top-left pixel, once you find the percentage, change the FLOAT number directly in data inspector, if you have lined up with the column above and the row on the left, you should be able to copy the coordinates from other characters
FF FF: WideChar/char16_t encoding of the character, change that to the new character in the data inspector
-Save the file

4. Updateing All.fco (DO NOT OPEN THIS WITH fcoEditor)
-Open All.fco with HxD, set displaying 28 bytes per row
-Add one to offset 0x24 (4 bytes), this is the total number of characters
-Goto the end of file, copy one row above (0x1C bytes)
-At offset 0x0C (4-bytes) of what you pasted, match the number you added: "XX XX XX XX"

And you're all set! You can now add the new character in fcoEditor!

-----------------------------------------------------------------
Special Thanks
-----------------------------------------------------------------
N69vid - General help on fte/fco formats
Joeylaw123 - Beta testing
