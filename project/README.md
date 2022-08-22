# Adventurec
#### Video Demo:  https://youtu.be/kYj9rZ6s-_U
#### Description:
#### Adventurec is a text game that runs in the terminal window with C (so it's an adventure, in C!).
#### An abstract description of the main section of "adventure.c":
    First it reads the lang.txt file to know what is the established preferred language of the player, with the default
    when one downloads the game being english. After that there is a menu loop, wich can give a rundown of the game in (1)
    guide, can change the language of the game in (2)language, can start the game in (3)start and can stop everything with
     (4)leave.
    If one starts the game, the main game loop beggins, and will continue until the player inputs the 'l' character in the
    terminal window or wins the game. This loop prints a header with some important information for the player, prints the
    area in wich the player currently is, prints subtitles for the space, receives user input, wich can be wasd for
    movement, for example, and then runs npc action, if there are any around.

#### A more specific description of the functions in "adventure.c":
    langread(): opens lang.txt file and reads it's character as an int into the lang variable.
    menurun(): starts by printing the menu options in the apropriate language and then receives user input wich it inserts
    in the menu variable.
        menu = 1: opens and prints a file wich contains a general guide to how to play the game in the correct language.
        menu = 2: presents the user with three language options and writes the input in the lang.txt file.
        menu = 3: receives game dificulty as user input, ends menu loop, game starts.
        menu = 4: ends both menu and game loop, ending game.
        textcat(): creates the file name of a given file in the subs directory and correct language directory, given a char
        pointer for the file name, as well as a buffer. usualy takes a spaces name as it's string, but in this instance
        takes "controls" as it's string, because the file name for the game guide would be subs/lang(0, 1 or 2)/controls.
        txt.
    header(): calls the death function, and then prints to the screen the coins, all the itens, the hp and the damage.
        death(): checks if tdmg (taken damage) is greater than hp, if so resets creatures, coins, itens from further in the
        game, as well as player hp and damagesends. Then sends player back to last freed space and prints a death message.
    rprint(): opens, reads through and prints apropriate file in spaces directory, if outside, increases visibility
    variable temporarily.
        spacecat(): concatenates a space file name in format spaces/(space name).txt.
        reading(): reads currentspace data from some arrays into more usable variables h, w, coinlocal and itemlocal.
        thingprintcheck(): check if a given character is that of a found coin or item, erasing it, if it is a creatures,
        printing its hit points, if it is the payers, printing 'o', and if it is outside of the players visibility,
        printing a '#'.
        labrynthgame(): uses the players location and surrounding characters to determine if the player has moved into one
        of the labrynth walls, if so moves them back.
    subprint(): finds currentspace's file in subs dirrectory and in chosen language dirrectory and prints it
        (again) textcat(): creates name of file within subs array based on currentspace and lang and in format: subs/lang
        (0, 1 or 2)/(name).txt.
    moving(): receives single character from user input, discards rest of input ("aw_çih0dn" is read as 'a'). alters x or y
    apropriately depending on the move and then calls movecheck. checks if player is using the semi collon to win the game
    or a healing item.
        movecheck(): checks if player moved into borders of map or objects of the space, thus sending the player back.
        checks if player moved into unfound item or coin, thus defining those as found. checks if moving into living
        creature of this space, thus dealing damage to said creature (if creature doesn't die, player doesn't move into it
        and only deals damage). if all creatures are defeated update lastspace. if found end of game stop game.
            doorcheck(): checks if x and y or the x and y skiped by moving 2 characters is that of a door, thus updating
            currentspace and the x and y to the othersides apropriate values. updates lastvspace if this is space is new.
            might skip spaces based on dificulty.
    action(): for every living creature in currentspace, move towards player and, if adjacent, deal damage.
        cmovecheck: checks, based on a creatures.where and a moves axis a modifier, if creature would move into space of
        other creature or player (or out of game, just in case), if so returns 0, wich stops the move within action().

#### Within adventurec (other than the c file and compiled c file) are olderversons/, lang.txt, subs/ and spaces/. Here I will explain what each of those is and how it is used by adventure.c
        olderversions/: This directory stores some older versions of the game, it exists to catalogue significant events,
        like the first version where I could read from the spaces directory, or when I first implemented movement. It also
        contains game.c, a file I started working on near the beggining of the course, a file from wich I got the idea to
        make this whole game in the first place.
        spaces/: The spaces directory contains one text file for every space in the game, wich represents a (usualy)
        vertical perspective of an area where the player can move around and find things.
        subs/: This directory contains three diectories, one for each language, within each of those there is one text file
        for each space in the game, this file has some text that will be printed under the space.
        lang.txt: This very simple file contains a single character, 0, 1 or 2, and serves to store the preferred language
        of the player even after the game stops running. It is read by the langread() function as soon as the game starts
        and can be overwritten through the language section of the menu.