# pacman-ctf
## Python3 version of UC Berkeley's CS 188 Pacman Capture the Flag project

### Original Licensing Agreement (which also extends to this version)
Licensing Information:  You are free to use or extend these projects for
educational purposes provided that (1) you do not distribute or publish
solutions, (2) you retain this notice, and (3) you provide clear
attribution to UC Berkeley, including a link to http://ai.berkeley.edu.

Attribution Information: The Pacman AI projects were developed at UC Berkeley.
The core projects and autograders were primarily created by John DeNero
(denero@cs.berkeley.edu) and Dan Klein (klein@cs.berkeley.edu).
Student side autograding was added by Brad Miller, Nick Hay, and
Pieter Abbeel (pabbeel@cs.berkeley.edu).

### This version attribution
This version (cshelton/pacman-ctf github repo) was modified by Christian
Shelton (cshelton@cs.ucr.edu) on June 23, 2020 to run under Python 3.


## Getting Started
(much of this is from the original HTML documentation, in origdoc/)

### Short Version:

run `python capture.py`

make your agents by modifying `myTeam.py`

run `python capture.py --red=myTeam` to test your team as Red

run `python capture.py --help` to see other options


### Longer Version:

The challenge is to design agents to play Capture-the-Flag in a Pacman-like
arena.   

![Example Game](/origdoc/capture_the_flag.png)

#### Rules

**Layout:** The Pacman map is divided into two halves: blue (right) and red (left).  Red agents (which all have even indices) must defend the red food while trying to eat the blue food.  When on the red side, a red agent is a ghost.  When crossing into enemy territory, the agent becomes a Pacman.

**Scoring:**  When a Pacman eats a food dot, the food is stored up inside of that Pacman and removed from the board.  When a Pacman returns to his side of the board, he "deposits" the food dots he is carrying, earning one point per food pellet delivered.  Red team scores are positive, while Blue team scores are negative.

**Eating Pacman:** When a Pacman is eaten by an opposing ghost, the Pacman returns to its starting position (as a ghost).  The food dots that the Pacman was carrying are deposited back onto the board.  No points are awarded for eating an opponent.

**Power capsules:** If Pacman eats a power capsule, agents on the opposing team become "scared" for the next 40 moves, or until they are eaten and respawn, whichever comes sooner.  Agents that are "scared" are susceptible while in the form of ghosts (i.e. while on their own team's side) to being eaten by Pacman.  Specifically, if Pacman collides with a "scared" ghost, Pacman is unaffected and the ghost respawns at its starting position (no longer in the "scared" state).

**Observations:** Agents can only observe an opponent's configuration (position and direction) if they or their teammate is within 5 squares (Manhattan distance).  In addition, an agent always gets a noisy distance reading for each agent on the board, which can be used to approximately locate unobserved opponents.

**Winning:** A game ends when one team eats all but two of the opponents' dots.  Games are also limited to 1200 agent moves (300 moves per each of the four agents).  If this move limit is reached, whichever team has eaten the most food wins. If the score is zero (i.e., tied) this is recorded as a tie game.

**Computation Time:** Each agent has 1 second to return each action. Each move which does not return within one second will incur a warning.  After three warnings, or any single move taking more than 3 seconds, the game is forfeit.  There will be an initial start-up allowance of 15 seconds (use the `registerInitialState` method). If you agent times out or otherwise throws an exception, an error message will be present in the log files, which you can download from the results page (see below).

#### Key data structures

`CaptureAgent` (in `captureAgent.py`) is a useful base class for your agents.
It has a variety of methods that can return useful information.  This includes a `distancer` field that contains a `distanceCalculator` object that can automatically calculate (and cache) the distances between every two points in the maze.

`GameState` (in `capture.py`) has still more information that can be queried.  A current `GameState` object is passed into your agents' `chooseAction` methods.  Note that `GameState` objects can return the set of legal actions for an agent and can generate new `GameState` s that would result from any action.

`game.py` has code that defines `Directions`, `Configurations`, `AgentState`, and a `Grid`, all of which might be handy and save extra work on your part.

`util.py` has code that might prove helpful.  Of particular note is the `Counter` class which implements a dictionary, but where unused keys default to mapping to 0 (instead of undefined).  A `Counter` mapping positions (integer pairs) to a real value can be used with `CaptureAgent.displayDistributionsOverPositions` to color the cells on the map with debugging information.

`myTeam.py` has skeleton code for generating a team of agents.  Its format should not be changed and needs to have the function `createTeam` as specified.  You should copy this file, change its name, and use it to build your own team.
