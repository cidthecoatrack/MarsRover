# MarsRover

This is a kata for the Mars Rover programming exercise

# Problem

The surface of Mars can be modelled by a rectangular grid around which robots are able to move according to instructions provided from Earth. You are to write a program that determines each sequence of robot positions and reports the final position of the robot.

A robot position consists of a grid coordinate (a pair of integers: x-coordinate followed by ycoordinate) and an orientation (N, S, E, W for north, south, east, and west).

A robot instruction is a string of the letters “L”, “R”, and “F” which represent, respectively, the instructions:

- Left : the robot turns left 90 degrees and remains on the current grid point.
- Right : the robot turns right 90 degrees and remains on the current grid point.
- Forward : the robot moves forward one grid point in the direction of the current orientation and maintains the same orientation. The direction North corresponds to the direction from grid point (x, y) to grid point (x,y+1). There is also a possibility that additional command types maybe required in the future and provision should be made for this.

Since the grid is rectangular and bounded, a robot that moves “off” an edge of the grid is lost forever. However, lost robots leave a robot “scent” that prohibits future robots from dropping off the world at the same grid point. The scent is left at the last grid position the robot occupied before disappearing over the edge. An instruction to move “off” the world from a grid point from which a robot has been previously lost is simply ignored by the current robot.

### Input

The first line of input is the upper-right coordinates of the rectangular world, the lower-left coordinates are assumed to be 0,0.

The remaining input consists of a sequence of robot positions and instructions (two lines per robot).

A position consists of two integers specifying the initial coordinates of the robot and an orientation (N, S, E, W), all separated by white space on one line. A robot instruction is a string of the letters “L”, “R”, and “F” on one line.

Each robot is processed sequentially, i.e., finishes executing the robot instructions before the next robot begins execution.

The maximum value for any coordinate is 50. All instruction strings will be less than 100 characters in length.

### Output

For each robot position/instruction in the input, the output should indicate the final grid position and orientation of the robot. If a robot falls off the edge of the grid the word “LOST” should be printed after the position and orientation.

### Sample Input

```
5 3

1 1 E

RFRFRFRF

3 2 N

FRRFLLFFRRFLL

0 3 W

LLFFFLFLFL
```

### Sample Output

```
1 1 E

3 3 N LOST

2 3 S
```

# Architecture & Design Overview

- Satellite: Manages the world map and the overall position of the rovers.  Sends commands to the rovers.
- Rover: Component that moves about the map.  Knows its current position.  Accepts o=instructions and executes them, but does not update its own coordinates
    - Motor: turns and moves a rover

# Assumptions

- Input is received as a string with lines delimited by line break characters (`\n`)
- Output is in a similar format (a single string delimited by line breaks)
- All testing will be automated, and there will be no manual QA efforts
- Project can exist as a code library, and can be initally headless (no UI, no CLI).  If a UI or CLI is desired at a later point, one can be added on top of the headless implementation.
- C# is an acceptable language (the hypothetical rover can support running C# code)
- Measurements are according to the world map grid, and are not beholden to either imperial or metric measurements (so no rovers should crash into the surface upon landing).
- Other than edges of the world map, no obstacles exist within the confines of the map that might hinder the rover's movements
- All input is received as all upper-case.  Handling strings as case-insensitive can be implemented in a future iteration.

# Estimate

Estimate to complete this solution, including testing, is 4 hours.
- Start Time: 1:00 PM
- Completion Time: 5:30 PM
- Estimate Accuracy: 112% (underestimated)

# Backlog

- Ideally not every class would be public.  Convert al lclasses not needed for public facing (basically all except `ISatellite`) into internal classes
- Set up build configuration (I would use TravisCI) to automatically run tests on all commits
- Ideally no service that executes action would be stateful.  Instead, they would manipulate separate, stateful data structures.