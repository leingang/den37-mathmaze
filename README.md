# den37-mathmaze
Math Maze
!!!!!!!!!

A scratch game for Cub Scout Pack 163, Den 3/7

Spring 2017

Design
======

Core gameplay
-------------

The player navigates a hero through a maze.  Along the way he meets critters.
When the hero meets a critter, the critter challenges the hero with a math fact.
If the player gets the problem right, the critter disappears.  If he gets it
wrong, the player goes back to the start of the maze or his most recent checkpoint.

At the end of each maze, the player must battle a boss.  The boss presents 
a series of math problems.  Each correctly solved math problem results in damage to
the boss until he is defeated.

Successive levels can be harder by a more complicated maze, more critters, and bosses
with more hit points.  

Extra features
--------------

If we can figure the core gameplay out, we can explore these options:

* Choose your avatar: alien, grandma, Elvis, ... ?

* multiplication and division math facts?

* Cut scenes.

Implementation
==============

Element specification
---------------------

The hero and critters are sprites.  The maze exit could be another sprite, or
perhaps a special color.

The maze, critter encounter, and boss battle modes are different backdrops.

Sprites vary in size, but 100x100 seems right.  Since the library contains bitmap and
vector sprites, I assume they can be either.  SVG maybe?  

Backdrops are 480x360.  Some options for maze grid:

 * 16x12 of 30px per side (25px hall, 5px wall)

 * 15x10 of 36px per side  (30px hall, 6px wall)

 * 12x9 of 40px per side

 * 8x6 of 60px per side

A finer grid should make harder gameplay.


Game modes
----------

Maze Navigation
~~~~~~~~~~~~~~~

The hero starts at an initial position.  The critters start at an initial position.
The maze exit is marked.  

Upon maze start, a number of critters spawn at regular intervals.  The number of
critters depends on the maze level.

The hero uses arrow keys to navigate the maze.  The move script listens for keypresses,
checks if the ordered move is "legal" (not into a wall), and then moves in the right
direction.

The critter(s) are moving in the maze, towards the hero.  This [maze algorithm](https://scratch.mit.edu/projects/53990658/#player) 
by RestroD has an implementation with Dijkstra's method.

If a critter meets a hero, we move to Critter Encounter mode with a backdrop change
and/or messge broadcast.

Critter Encounter
~~~~~~~~~~~~~~~~~

Backdrop changes, closeup on the critter.  We can use a clone of the sprite here, at 
a larger size and in the middle of the backdrop.

The critter generates a random math fact and asks the hero to solve it.  We can use
the Ask and Wait block for that.

If the answer is correct, the critter gives an affirmative message.  Maybe it makes
a celebratory gesture with a costume change.  The game back to Maze Navigation mode,
but the critter either vanishes or moves back to its initial position.  Maybe it 
respawns later.

If the answer is incorrect, the critter gives a negative message, possible gesture.
The game goes back to Maze Navigation mode, but the player is moved back to his 
starting position.

Boss Battle
~~~~~~~~~~~

Backdrop changes, closeup on the boss.  The boss has a health register that
depends on the level.  

Until the health register is zero... the boss generates a random math fact and 
asks the hero to solve it. If the answer is correct, the boss takes a hit and the
damage register goes down.  If the answer is incorrect ... does the hero have 
a damage register too?  Maybe a time limit?

If the player health reaches zero, he goes back to the beginning of the level.
If the boss health reaches zero, he goes to the next level.  

Cut scenes
~~~~~~~~~~

These can be any kind of animation.  They can go at the start of the game,
between levels, at the end of the game.

Tasks
=====

There are four developers: Felix, Christopher, Kieran, Liam.  Maybe Ethan
if he joins in.

Artwork can be done within the Scratch editor.

Maze design
-----------

We need at least 5 mazes.  Matthew will design one mockup.

Hero art
--------

One sprite.  Customizeable avatars could be implemented with different 
costumes.    Or we somehow use separate sprites and copy the scripts.

For the mockup we can use the cat.

Critter art
-----------

There is only one critter sprite, but he could have different costumes:

 * smiling

 * frowning

 * questioning (eyebrows raised)

 * shrieking ("Oh nooooooo")

I was using the bat sprite from the Scratch library.

Boss art
--------

We need at least 5 bosses, with similar expressions as above.

Pick a monster from the scratch library.

Cut scenes
----------

Opening and closing.  Animated text.  Sounds, maybe?

TODO: Study how to make animations like this.

Scripting
---------

* Hero maze navigation:

  - legal movement

  - back to start

  - trigger boss battle

* Critter movement

  - towards hero (Dijkstra)

  - trigger critter encounter

* Critter encounter

  - Pose question

  - check answer and react.

* Boss battle

  - health bar

  - question loop

  - check answer, react

  - result choice












