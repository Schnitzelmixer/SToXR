# Note
Git lfs has been used to upload this project.
To export from lfs to normal files run git lfs 'migrate export --include "*"' 
![Stackoverflow issue](https://stackoverflow.com/questions/63408225/files-have-become-unreadbale-post-git-lfs-migrate-import-how-to-undo)

# How to start
1. Clone/fork this repository  
2. Open the root of this repository in Unity
3. If you get a warning popup about disabling the old `UnityEngine.Input` API, press `NO`  
  ![image](./LabRecordings/popup-press-no.jpg)
    - If you accidentally pressed `YES`, you should still be able to switch to the old input manager in the project settings under `Player`:
    ![image](./LabRecordings/switch-input-manager.png)
4. Open the `IntroScene.unity` (stoxr-project-2\Assets\Brick Project Studio\Apartment Kit\Scenes)
5. Press the 'Play'-button

# Project Overview/ Extended Documentation
<details> 
  <summary>This section contains a descriptive overview about the structure and classes of this project.</summary>

  ## Directory structure
  On the top level of the directory structure are mostly default directories. Our relevant code is inside the *Assets* folder.
  Inside this folder the following directory structure can be seen (nested files and directories aren't shown here for clarity):
  ```
  │
  ├── Baseball Bats\
  │
  ├── Blood decal pack\
  │
  ├── Brick Project Studio\
  │
  ├── EffectExamples\
  │
  ├── Flashlights\
  │
  ├── HDRPDefaultResources\
  │
  ├── Heist Unity\
  │
  ├── Oculus\
  │
  ├── Own Assets\
  │
  ├── PB_Spider\
  │
  ├── Resources\
  │
  ├── SkySeries Freebie\
  |
  ├── TextMesh Pro\
  │
  └── XR\
  ```
  A lot of these directories are packages that we imported for models, animations, audio files etc. *Own Assets* is an exception here, as there are some small models (tablet, notes) that we created ourselves lying inside this directory. 
  All necessary files, (Meshes, materials, animations, scripts...) are within their respective directory, e.g. the Flashlight files are within the *FLashlights* directory, although the naming of the directories sometimes refers to their imported package name.
  If the necessary files aren't in their respective directory, then they are in the *Brick Project Studio* directory, which forms the baseline of this project, as this package contains the apartment. The directory tree of *Brick Project Studio* looks like this (files are not listed for clarity):
  ```
  │
  ├── Apartment Kit\
  │   │
  │   ├── Materials\ <- imported scripts from the apartment asset and our own custom materials
  │   │   │
  │   │   └── ...
  │   │
  │   ├── Models\ <- all models of the imported apartment asset
  │   │
  │   ├── Prefabs\ <- all imported prefabs from the apartment asset
  │   │   │
  │   │   └── ...
  │   │
  │   ├── Scenes\ <- includes all relevant scenes (IntroScene, MainScene, DebriefingScene)
  │   │   
  │   ├── Scripts & Animation\ <- imported scripts of the apartment asset and our own scripts
  │   │   │
  │   │   ├── Closet\
  │   │   │
  │   │   ├── Grabbable\
  │   │   │
  │   │   ├── Light_flickering\
  │   │   │
  │   │   ├── Managers\
  │   │   │
  │   │   ├── OvenOpen\
  │   │   │
  │   │   ├── Slide\
  │   │   │
  │   │   ├── Spider_movement\
  │   │   │
  │   │   ├── TableFlip\
  │   │   │
  │   │   ├── Tablet\
  │   │   │
  │   │   ├── Weather\
  │   │   │
  │   │   ├── Windows\
  │   │   │
  │   │   └── Z Axis -1\
  │   │
  │   ├── Sounds\ <- all sound effects we added
  │   │
  │   ├── Textures\ <- the imported textures of the apartment asset and our own custom textures
  │   │   │
  │   │   └── ... 
  │   │
  │   └── Videos\ <- the video clips played on the in game TV
  │
  └── SE Basic Assets\ <- this folder only contains imported files from the apartment asset like prefabs
      │
      └── ...
  ```
  There are two directories, *Apartment Kit* and *SE Basic Assets*.
  The latter contains many default files, which we used but we didn't add any files inside this directory. The *Apartment Kit* directory on the other hand contains many important files, for example the *Scripts & Animations* directory holds important scripts and animations, that aren't necessarily bound to imported packages. Also, the *Scenes* directory with our Scenes is located here as well as the video clips.
  Despite the fact that there are quite a few directories in this project, this description focused on the separation of default packages and relevant files. There could be a few unused directories of early development stages, which can be ignored.

  ## MainScene hierarchy (top level)
  ```
  MainScene
  │ 
  ├── GameEventManager <- Handels all in game events like rain and TV
  │
  ├── blood <- Blood splatters that show on tablet after ending gun shot
  │
  ├── Tablet
  │
  ├── Clues <- All four paper clues with riddles
  │
  ├── DangerousObjects <- Weapons and money, vibrate when you get near them
  │
  ├── MainHouse <- All structure (walls, floor, ceiling) and furniture of the main house you start in
  │
  ├── GlobalLightningLight <- Directional light at intensity 0, gets set intensity on lightning
  │
  ├── RainEffect <- rain particle system
  │
  ├── Base Scene <- floor around the house
  │
  ├── Lightning <- lightning and thunder particle system
  │
  ├── PlayerController <- OVR player with camera rig
  │
  ├── spider 
  │
  ├── Flashlight
  │
  ├── Sky and Fog Volume <- contains info for skybox and fog volume for volumetric flashlight light
  │
  ├── ExternalStructure1 <- house structure next to main house you can see from window
  │
  ├── ExternalStructure2 <- house structure next to main house you can see from window
  │
  ├── EventSystem <- was generated by previous tablet input (probably not needed anymore)
  │
  ├── GeneratorAudio <- audio source of generator fallout when all lights turn off
  │
  ├── GunSounds <- audio source for ending gun shot
  │
  └── Translators <- I AM GOLDEN game objects
  ```

  ## UML Class Diagrams
  To get an overview of the code architecture of this project, we list UML class diagrams of the classes we created. All classes listed here have additional comments about their functionality in their code files. <br>

  The first diagram shows the classes responsible for the scene management.
  - *Scene* is an enum which holds all scenes.
  - *SceneLoader* loads the scenes.
  - *IntroManager* checks if the MainScene should be loaded.<br>
  ![image](./UMLs/Scenes.png)

  The second diagram focuses on the Event System.
  - *GameEventManager* manages all timed events, meaning that certain events get queued and set active after a specified delay.
  - *flicker_lights* controls the flickering of the apartment lights.
  - *spider_behavior* manages the behavior and animations of the spider.
  - *GrabbableWithSound* manages the Grabs on grabbable objects.
  - *GrabbableClues* inherits from *GrabbableWithSound* and has special behavior for the clues (notes)
  ![image](./UMLs/GameEventManager.png)

  In the third diagram are all individual scripts, that aren't bound to timers and therefore not bound to the *GameEventManager* system.
  - *TabletFunctionality* controls the interactions with the tablet (numpad)
  - *ButtonTrigger* is for the individual buttons on the numpad of the tablet and calls NumberPressed() of *TabletFunctionality*
  - *OpenAndClose* is bound to all Gameobjects that can be opened or closed with individual animations and sounds.
  - *flashlight_logic* manages the behavior of the flashlight.
  - *LightningTrigger* contains the logic of the collision.
  - *GrabbableDangerous*
  ![image](./UMLs/IndividualScripts.png)
</details> 

# User interaction
A demo video documenting all features and user interaction can be found in [\stoxr-project-2\LabRecordings](https://gitlab2.informatik.uni-wuerzburg.de/hci/teaching/courses/special-topics-xr/student-materials/2022-summer/stoxr-project-2/-/blob/main/LabRecordings/stoxr-project-2-video.mp4). You will receive a short story intro. You enter your neighbors house while he is away to find evidence against him. To unlock his tablet you need to find 4 paper notes, each of them containing a riddle. Can you crack the code and find out the password?

![image](./LabRecordings/intro.jpg)

<details> 
  <summary>SPOILERS: This section contains a summary of all possible interactions and events of the application including solutions to the puzzles </summary>

  ## Four paper notes
  Across the apartment you will find four paper notes with the following riddles on them
  ### What occurs twice in a week, once in a year but never in a day?
  - Answer: The letter E, because it appears twice in the word `week` and so on
  - Location: Closet opposite the bedroom
  ![image](./LabRecordings/location-riddle-e.jpg)
  - Hierarchy: riddle-e (GameObject)
  ### I go first unless the order is reversed. I stand in front of a lot of things, yet I have no real legs to stand on. You might just yell out my name once you find the answer.
  - Answer: The letter A, because 
    - it's the first letter of the alphabet
    - it literally stands in front of (a) `lot of things`
    - it stands in front of many nouns because it is a determiner/article
    - when you solve something or someone tells you the answer, you might just say 'Ah (I get it)'
  - Location: In the bedroom, underneath the left side pillow
  ![image](./LabRecordings/location-riddle-a.jpg)
  - Hierarchy: riddle-a (GameObject)
  ### What is the end of everything?
  - Answer: The letter G, because it is the last letter of the word `everything`
  - Location: In the guest room, underneath the bedside table
  ![image](./LabRecordings/location-riddle-g.jpg)
  - Hierarchy: riddle-g (GameObject)
  ### What comes once in a minute, twice in a moment but not once in a thousand years?
  - Answer: The letter M, because it appears once in the word `moment` and so on
  - Location: In the kitchen, in the second wall cabinet from the right
  ![image](./LabRecordings/location-riddle-m.jpg)
  - Hierarchy: riddle-m (GameObject)
    

  ## Game events

  ### Spider
  In the guest room, in the right corner of the room next to `riddle-g`, there is a small spider that follows and attacks the player when they get too close and then runs away when they are too far away again.

  ![image](./LabRecordings/spider.jpg)

  ### Rain
  After three minutes it starts to rain, you can hear but also see the rain if you look out of the windows. Another three minutes later the rain sounds get louder, hinting at more intense rain.

  ### Lightning and thunder
  After four minutes lightning and thunder strike, illuminating the entire scene when they appear. While they are technically visible to the player when looking out the window under certain circumstance it is quite unlikely they will actually see the lightning itself, though they can definitely see the flash of light. Another three minutes later the rate of lightning and thunder increases, making them appear more frequent. Also emits a lighting with thunder when a paper note has been picked up for the first time.

  ![image](./LabRecordings/lightning-1.jpg)
  ![image](./LabRecordings/lightning-2.jpg)


  ### Flickering lights
  After two minutes the lights start to turn off periodically, making a representative sound and spawning sparks when they do. The frequency of them turning off as well as the time of them staying off increases steadily over time until about ten minutes in when you hear the sound of a complete power failure, turning all the lights off for the remainder of the experience.

  ### TV
  After about one and a half minutes the TV will start to play a cute and funny short documentary about a wild hamster, immediately after the video concludes another one will start to play. This second video contains disturbing sounds and images of pigs locked up in a CO2 stunning chamber right before their slaughter. 

  ## Special interactions 
  Almost all small objects you think you should be able to grab are grabbable by pressing and holding `Axis1D.PrimaryHandTrigger` / `Axis1D.SecondaryHandTrigger`. Almost all drawers, doors, cupboards etc. are openable. To do so, move any hand near the handle and tap `Axis1D.PrimaryHandTrigger` / `Axis1D.SecondaryHandTrigger`.

  ![image](./LabRecordings/ovr-controller-mappings.png)

  ### Teleportation
  To prevent motion sickness we decided to implement teleportation instead of thumbstick movement. While holding the `Axis1D.PrimaryIndexTrigger` / L Index trigger (left hand) the player can aim at a target location and let go of the button to teleport. Additionally, the player can also adjust the look direction (arrow on target location) with the left thumbstick while aiming.

  ![image](./LabRecordings/teleport.gif)

  ### Flashlight
  In the living room, the room the player spawns in, a flashlight can be found. This flashlight can be picked up and will be very useful to explore unlit drawers, closets and the apartment once all the lights are off.

  ![image](./LabRecordings/flashlight.jpg)
  
  ![image](./LabRecordings/flashlight.gif)


  ### Dangerous items 
  Some items placed around the apartment are 'dangerous' and will cause the controllers to vibrate once they get near them and picking them up will vibrate at maximum intensity. These items include a gun in the desk drawer, a stack of money near the bed in the bedroom and a baseball bat in the corner of the bedroom closet.

  ![image](./LabRecordings/pistol.jpg)
  ![image](./LabRecordings/money.jpg)
  ![image](./LabRecordings/baseball.jpg)

  ## Unlocking the tablet
  Once you have found all notes and solved all riddles you will end up with the letters `A`, `G`, `M` and `E`. You should have also found the `I AM GOLDEN` clue scattered multiple times across the apartment. 
  
  ![image](./LabRecordings/iamgolden.jpg)
  
  `I AM GOLDEN` depicts its letters in a 3x3 square that lines up with the 3x3 number input of the tablet pin, allowing you to translate the four letters into the four numbers needed for the password. 
  
  ![image](./LabRecordings/tablet.jpg)

  To figure out the correct order of the letters/numbers you should try and find a word. Once you find the word `GAME` and type in the translated number code `4892` on the tablet, you will find it unlocked, revealing various calendar events and emails, but before you really get to read them you hear a gun cocking and see your blood scattered across the screen.
</details>
<br>

# Theoretical concept
We hope to evoke feelings of fear, tension, distress and horror (mostly focusing on fear and tension, but they are all connected to some extent). To achieve this we created an environment with dim and interactive lightning including but not limited to the flickering lights, flashlight, unlit closets and lightning. The experience takes place in someone else's apartment resulting in an unknown and confined space. The sound design, unpredictable game events and increasing intensity of it all is also supposed to contribute to evoking tension and fear. The interactive puzzle and exploration is meant to immerse and motivate the player, keeping them invested and potentially caring more about the events and thus evoking stronger emotional responses. This concept and goal was also explained to the player in the short `DebriefingScene` at the end of the experience:

![image](./LabRecordings/debriefing.jpg)

# Small user study
In the context of the module a small event was organized where most students presented their projects at the university VR lab, testing each other's applications. There we had the opportunity to test the effects of our application with eight people and see if we can evoke feelings of fear and tension. Their all received short introduction to the objective (finding four paper notes and solving the puzzles to unlock the tablet) and the controls. The participants started in the `IntroScene` and questions were answered as well as hints were given during the experience to save time and try to keep the time spent around 15 minutes, ideally below 20 minutes. After the VR experience each participant was asked five questions, usually in German, in an open interview:

## Welche Emotionen hat die Anwendung ausgelöst? / What emotions did this application evoke?
While some experienced fear to some extent, many stated explicitly that they did not really experience fear. So while some felt uncomfortable or creeped out the most mentioned emotion was in the field of stress/anxiousness/tension. Fun, curiosity and determination to solve the puzzles were also mentioned frequently.

## Welche Situation hatte die stärksten Emotionen ausgelöst? (Und welche Emotion war es?) / What situation evoked the strongest emotions? (And which emotion was it?)
The most intense moments were the gun shot in the end and all lights turning off, which were both mentioned twice but also the second video playing on TV, finding the gun and the lighting/thunder. These moments caused anxiousness, agitation and fear.

## Wie würdest du die Erfahrung beschreiben? / How would you describe the experience?
Some answers included experiencing nervousness, joy of exploration and solving of puzzles, anxiousness, stress and pressure of time, tension.

## Wie bewusst war es dir, dass du dich in einer virtuellen Umgebung befindest? / How aware were you that you were in a virtual environment?
The experience was generally perceived as immersive, but with certain situations breaking that immersion like the teleportation, hearing other people talk in the room, receiving hints and asking questions.

## Wie echt erschien dir die Erfahrung in der virtuellen Umgebung? / How real did the experience in the virtual environment seem to you?
This question was answered similarly to the previous one but a bit more positively (more real). This question was meant to target more the believability and credibility of the experience and not so much the immersion. The high interactivity and frequent use of sound effects made the experience feel quite real.

## Conclusion
We were able to evoke negative emotions but more so stress, anxiousness and tension rather than fear and distress. This might have been due to the setting of the event creating artificial stress and pressure of time. While we were hoping to evoke stronger emotions by keeping the players invested into the experience with exploration and puzzles these elements seemed to evoke fun and did motivate to keep playing until the riddles are solved. All in all we are happy with the results and believe we have sufficiently evoked the emotions we wanted to evoke.

# Sources
The sources can be seen on the [wiki home page](https://gitlab2.informatik.uni-wuerzburg.de/hci/teaching/courses/special-topics-xr/student-materials/2022-summer/stoxr-project-2/-/wikis/home)

# Requirements
## Major
- Increase in intensity
  - Increasing frequency and intensity of game events (for example rain, lightning/thunder)
  - Lighting: Starting with all lights on. After some time lights start to turn off. The frequency and length of these outages increases until all lights will shut down.
  - TV: After a short time a cute video clip of a hamster starts playing followed by a disturbing video of pigs in a CO2 chamber.
  - Rain, Thunder, Lightning: Starting with no rain. After some time it starts raining and after even more time the rain intensifies and lightnings start to appear. The frequency of lightnigs also increases over time.
- Interaction with the environment
  - Can open/close almost all doors, drawers, windows and cabinets
  - Can pick up most small objects
  - Can interact with the tablet
- Extended documentation
  - UML class diagrams
  - Description of file structure
  - Description of file structure of Unity MainScene
  - Inline code documentation
- Debriefing
  - Explanation after the ending (See `DebriefingScene`)

## Minor
- Polished appearance
  - HDPR render pipeline
  - Particle effects
    - Lightning
    - Rain
    - Electrical sparks when lights turn off
  - Volumetric lighting/fog for flashlight
  - Skybox
- Audiovisual and/or haptic features
  - Sound effects on grab for paper notes
  - Opening and closing sound effects as well as animations for all doors, drawers, windows and cabinets
  - Moving hands near dangerous items (like the gun) causes vibration and maximum vibration on grab
