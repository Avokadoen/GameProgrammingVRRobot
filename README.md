# GameProgrammingVRRobot
Mirror repo of: https://gitlab.com/avokadoen/GameProgrammingVRRobot

# Mr. RogueBot
![Mr. RogueBot](https://i.imgur.com/W98Zv0M.png)
---

## Game Description
Mr. Roguebot is a VR Rogue-like shooter that is about surviving a robot apocalypse while progressing through the robot compounds. 

#### Key features in the game currently:
- Random level generation
- Physics based gameplay loop 
- Machine learned hybrid AI (tensorflow, statemachine and coding)

## Based on our initial idea:
The player (and agents) can wield powerful components that they can attach to their body to use as tools of destruction on both self and others around. Every agent and the player consist of a custom made skeleton system that contains physical objects that can be destroyed.

The levels contain a diverse range of styles and will be interesting to observe in VR. The range of weapons will like the components be enjoyable to experient with. Such as the gravity gun that is loaded with anything and will fire it out of the barrel with high speed. 

In the hub you can explore differnt combination of body parts to achive your desired playstyle. Heavier parts will be more bulky with more health but will be loud and limit mobility and vice versa.

#### Key features missing in the game currently:
- Skeleton system
    - Customize bodyparts
    - Diverse enemies
    - Mutilation
- Versatility in most (weapons, rooms/levels ...)
- Settings (free locamotion vs teleporting, graphics ...)
- Component system (items that attach to the body)
- Weight system


## A selection of our notable features:
### Networking
 * Twitch Integration
     * Player can view twitch chat while playing

---
Networking has not really been one of our main objectives for this game project. Also as it is supposed to be single-player game, though it has potential to have some sort of leaderboard system or a competitive-game mode. However the game is currently not in a state where this is suiting. 

![Twitch Integration](https://i.imgur.com/F47XiaL.png)

What we do have though is a twitch integration so that the user can interact with twitch chat while playing the game. (The user has to put his own credentials in system environments for twitch authentication, if not the chat will just be disabled) This twitch canvas can be toggled by a press on the controllers and is viewed on a canvas for the player.

---

### UI / UX
 * Level Selection
     * Overview of map
     * Seed selection
     * Level teleporter
 * Weapons
     * Haptic feedback
     * Sound
 * _Teleport dashing_ indicators
 * Inventory aka. attach to self
 * Twitch chat canvas
 * VR Keyboard in main hub
---
As our project is set in a VR environment we feel that our approach on the UI part of the project will be a bit different than for any other typical 2D-screen UI. So for this we have a couple of things we would consider as world-based UI. We have a main hub where the player is presented with a war-table indicating what levels are possible for selection, these also display whether a level is locked, unlocked, or already played through. There is also indication on a teleporter in this hub whether if it is active for going to a new level or not.

![Main Hub](https://i.imgur.com/MrEvt3l.gif)

Furthermore we are using a _dashing_ method for movement in VR, and this uses an indication method from the hand to the floor where the player will land after the dash.

Also, as this is in VR we have a couple of things we feel should atleast go under UX, like haptic feedback and sound for indications of different things in the world environment.

---
### Graphics
 * Optimizations
     * Static batching (Combining meshes)
     * Textures channel-usage
     * GPU-instancing
     * Pooling mechanisms
 * Custom physically based shaders
     * Channel masking shaders
 * Custom shaders
     * Stylized shaders in the hub scene
 * Custom effects
     * _animated_ materials
---
As we work with VR, the focus needs to be on optimizing to stay above 90 fps. 

On our generator we combine the prefab meshes in the room to one mesh to make the draw calls faster. 

For the AI we use GPU-instancing for squad materials to make them look distinct while doing so with minor costs to performance. 
![channel masking](https://i.imgur.com/GUdXF3z.gif)

For the bullets we use a singleton pooling mechanism that supplies magazines bullets. Bullets also don't overstay their welcome and will deactivate on heavy impact or despawn after a certain timer.

We also apply shaders to some problems to give the game a unique look like animating materials. 

---

### AI
 * Machine-learnt squad behaviour
 * Three layers of AI:
     * High-level: CommanderBrain ([ML-agents](https://github.com/Unity-Technologies/ml-agents))
     * Middle layer: Activites (StateMachines)
     * Low layer: UnitActions and UnitSensors 
 * Maneuvering (based on navmesh paths)
 * Generator systems
     * "Flocking" room-placements
     * Minimum spanning tree
     * Corridor pathfinding
     
---

![path](https://i.imgur.com/msGyH83.gif)

AI has been one of our bigger focus areas during this project. We developed our main AI-system as part of our AI project in the _AI intro_-course:
The system is composed of a multilayered structure consisting of both simple reflex agents, and a machine learnt agent ordering said reflex agets around.
In order to construct more complex behaviour in the reflex agents (_units_ as we came to calling them), we introduced a middle layer where the agents behaviour is determined by states in (sub-)state machines.

![image alt](https://i.imgur.com/cN5Tbm6.gif)

Our suggested multilayered system ([here's the report from that](https://docs.google.com/document/d/1luuUYjUr6BZ6iQgFZsEwww4VvL52l7-tBe0Ctpm2h7I/edit?usp=sharing), if interested) got praised for being both inventive and new-thinking in the AI course. - We've now trained it a bit further, and it is (at least to some degree) working as intended.

![Architectures](https://i.imgur.com/CS2YoMC.png)

In addition, we'll mention parts of our generation system that takes AI-principles into account: 

In order to manage where rooms are placed we're biasing selection of room placement by physically testing for space, and testing relations, similar to what one might do in certain _boids_-implementations.

We're then ordering the rooms into a minimum spanning tree, in order to connect the rooms in the _most sensible_ way. The tree is from this point on  used as an interface to execute pieces of code. Speciffically we use it to generate pathfind corridor placement between the rooms by traversing from the root nodes to child nodes in the tree.

![Generating rooms](https://i.imgur.com/PPjyDdJ.gif)

---

### Extras (i.e. stuff that we feel should contribute to the grade but apparently doesn't 😢)
 * Procedural Generation
    * Map over levels
    * Level generation
    * Room generation
    * Decoration/Interior placement
    * Seeded input
 * Self-made assets
    * Roughly 95% of the used assets are self made
---
A huge part of our initial work with this project was with the procedurally generated levels, as this is a rogue-like game. Furthermore we wanted this system to be very flexible and dynamic. Creating all of this was quite a big task, and especially as the generation is done through several layers.

Almost every asset used in the project are self-made and has also been part of the learning process. Working on how to integrate those tools, and learning the workflow with them has also been good experiences to have. E.g. how to go about modelling and texturing objects we wanted to have in our game.

---

## What each of us did
Throughout the whole project we've worked fairly effectively together on different features. -Meaning we've not really distingushed between who did what at each time, as we all worked on bits and pieces as we saw fit. often going back and forth over each other's code. Contrary to what is most often the case when working together on a Unity project this didn't cause issues that often as we were all careful to work within our own scenes, and notifying each other whenever we needed scene merging to happen.

However, here are some notable pieces of code each of us worked on more than others:
 * Halvor
    Level generators (i.e. rooms and corridors)
 * Aksel
    Weapon systems 
 * Nikolai
    The player hub
## Discussion
### What went wrong?


First of all, we definitely scoped too big for this project, even though that can be good for the learning process, and as this to some degree is a prototype of a game and is not supposed to be that polished, we had a lot of areas we wanted to cover. 

Initially when we started our project we immediately started working on procedural generation of levels and all that it includes. This took a lot of work, and we used a lot of time on these systems before we started implementing actual gameplay.

When discussing this within the group now a couple of weeks before delivery, we all agreed upon that we probably should've had some kind of gameplay loop in a lot earlier, and that that probably would've been a better approach. 

This way we probably would've noticed challenges more upfront, and also we would to some degree have a more working product earlier in development, that we could expand upon, rather than working on systems across the board for a long time in development, to eventually merging them a bit late. Which at that point is a pretty big process in itself.

![Commits per time](https://i.imgur.com/VeO2FC3.png)
_Time_ was definitely a big factor in terms of how this project went as well though, as we initially in the semester felt we had a lot of time for a bigger scope project than we ended up having as there was a lot of work across all courses over the semester, more so than expected.

### Summary

The consensus in the group is that we like the concept of our project and we all would like to see it expanded. What we have is _definitively_ a WIP product but it has some emergent gameplay shining through its rough state. It's hard to say if we could have optimized our workflow to any degree or not, but time and more trial and error will show.

#### Gameplay video
[Here's a video of some recorded gameplay from our game](https://www.youtube.com/watch?v=XVTmAA_UvRM)
