# How to start

<!-- 1. Clone/fork this repository (branch/commit here?)  
2. Start the application  
    <ol>
      <li>Open the root of this repository in Unity,</li>
    </ol>  
    OR  
    <ol>
      <li>Open the root of this repository in Unity,</li>
      <ul>
        <li>If you get a popup about ... press `NO` (?)</li>
      </ul>
      <li>Open the `IntroScene.unity`</li>
      <li>Press the 'Play'-button</li>
    </ol> -->

1. Clone/fork this repository (branch/commit here?)  
2. Open the root of this repository in Unity
3. If you get a warning popup about disabling the old `UnityEngine.Input` API, press `NO`
    - If you accidentally pressed `YES`, you should still be able to ... TODO
4. Open the `IntroScene.unity`
5. Press the 'Play'-button

# User interaction
You will receive a short story intro. You enter your neighbors house while he is away to find evidence against him. To unlock his tablet you need to find 4 paper notes, each of them containing a riddle. Can you crack the code and find out the password?

TODO picture

<details> 
  <summary>SPOILERS: This section contains a summary of all possible interactions and events of the application including solutions to the puzzles </summary>

  ## Four paper notes

  TODO pictures

  Across the apartment you will find four paper notes with the following riddles on them
  ### What occurs twice in a week, once in a year but never in a day?
  - Answer: The letter E, because it appears twice in the word `week` and so on
  - Location: Closet across the bedroom
  - Hierarchy: riddle-e (GameObject)
  ### I go first unless the order is reversed. I stand in front of a lot of things, yet I have no real legs to stand on. You might just yell out my name once you find the answer.
  - Answer: The letter A, because 
    - it's the first letter of the alphabet
    - it literally stands in front of (a) `lot of things`
    - it stands in front of many nouns because it is a determiner/article
    - when you solve something or someone tells you the answer, you might just say 'Ah (I get it)'
  - Location: In the bedroom, underneath the left side pillow
  - Hierarchy: riddle-a (GameObject)
  ### What is the end of everything?
  - Answer: The letter G, because it is the last letter of the word `everything`
  - Location: In the guest room, underneath the bedside table
  - Hierarchy: riddle-g (GameObject)
  ### What comes once in a minute, twice in a moment but not once in a thousand years?
  - Answer: The letter M, because it appears once in the word `moment` and so on
  - Location: 
  - Hierarchy: riddle-m (GameObject)
    

  ## Game events

  ### Spider
  In the guest room, in the right corner of the room next to `riddle-g`, there is a small spider that attacks the player when they get too close and then runs away after a while when they are too far away again.

  TODO picture
  ### Rain
  After three minutes it starts to rain, you can hear but also see the rain if you look out of the windows. Another three minutes later the rain sounds get louder, hinting at more intense rain.

  ### Lightning and thunder
  After four minutes lightning and thunder strike, illuminating the entire scene when they appear. Another three minutes later the rate of lightning and thunder increases, making them appear more frequent. Also emits a lighting with thunder when a paper note has been picked up for the first time.

  TODO pictures

  ### Flickering lights
  After two minutes the lights start to turn off periodically, making a representative sound and spawning sparks when they do. The frequency of them turning off increases steadily over time until about ten minutes in when you hear the sound of a complete power failure, turning all the lights off for the remainder of the experience.

  ### TV
  After about one and a half minutes the TV will start to play a cute and funny short documentary about a wild hamster, immediately after the video concludes another one will start to play. This second video contains disturbing sounds and images of pigs locked up in a CO2 stunning chamber right before their slaughter. 

  ## Special interactions 
  Opening drawers, cupboards and doors
  ### Teleportation

  ### Flashlight
  In the living room, the room the player spawns in, a flashlight can be found. This flashlight can be picked up and will be very useful to explore unlit drawers, closets and the apartment once all the lights are off.

  ### Dangerous items 
  Gun, money and baseball bat (DangerousItems)

  ## Unlocking the tablet
  Once you have found all notes and solved all riddles you will end up with the letters `A`, `G`, `M` and `E`. You should have also found the `I AM GOLDEN` clue scattered multiple times across the apartment. `I AM GOLDEN` depicts its letters in a 3x3 square that lines up with the 3x3 number input of the tablet pin, allowing you to translate the four letters into the four numbers needed for the password. To figure out the correct order of the letters/numbers you should try and find a word. Once you find the word `GAME` and type in the translated number code `4892` on the tablet, you will find it unlocked, revealing various calendar events and emails, but before you really get to read them you hear a gun cocking and your blood scattered across the screen.

</details>
<br>

# Theoretical concept

TODO picture debriefing

# Small user study
In the context of the module a small event was organized where most students presented their projects at the VR lab, testing each other's applications. There we had ...

# Sources
The sources can be seen on the [wiki home page](https://gitlab2.informatik.uni-wuerzburg.de/hci/teaching/courses/special-topics-xr/student-materials/2022-summer/stoxr-project-2/-/wikis/home)

# Requirements (optional to document)