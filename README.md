This was one of the Perl Quiz of the Week problems a couple of years ago.  I reused it as [Ruby Quiz #117](http://www.rubyquiz.com/quiz117.html).  It's also my favorite computer simulation.

The goal is to create a simulation of frost.  The end result should look something like this [simulation example](http://www.rubyquiz.com/SimFrost.mov) (13MB Quicktime Movie).

Of course, you don't have to create a movie.  Using the terminal is just fine.

Here are the rules of the simulation.

First, create a two-dimensional grid to hold our simulation.  The width and height must be even numbers.  The top of this grid wraps (or connects) to the bottom and the left and right sides also touch, so technically we are representing a torus here.

Each cell in the grid can hold one of three things:  vacuum, vapor, or ice.  To begin with, place a single ice particle in the center of the grid and fill the remaining space with some random mix of vacuum and vapor.  You will probably want to leave yourself a way to easily adjust the starting vapor percentage as you begin to play with the simulation.

Display the starting grid for the user, then begin a cycle of "ticks" that change the current state of the grid.  Redraw the grid after each tick, so the user can see the changes.  The simulation continues until there are no more vapor particles.  At that time your program should exit.

Each tick changes the grid as follows.  First, divide the board into "neighborhoods."  A neighborhood is always a square of four cells.  Given that, on the first tick we would divide a six by four grid as:

	+--+--+--+
	|  |  |  |
	|  |  |  |
	+--+--+--+
	|  |  |  |
	|  |  |  |
	+--+--+--+

However, even numbered ticks divide the board with an offset of one.  In other words, the neighborhoods will be as follows in the second round:

	 |  |  |
	-+--+--+-
	 |  |  | 
	 |  |  |
	-+--+--+-
	 |  |  |

Remember that the grid wraps in all directions, so there are still just six neighborhoods here.  Later ticks just alternate these two styles of dividing the grid.

In each neighborhood, apply one of the following two changes:

1.  If any cell in the neighborhood contains ice, all vapor particles in the
    neighborhood turn to ice.
2.  Otherwise, rotate the contents of the neighborhood 90% clockwise or
    counter-clockwise (50% random chance for either).

For example (using `" "` for vacuum, `"."` for vapor, and `"*"` for ice), the first rule changes:

	+--+
	| .|
	|* |
	+--+

into:

	+--+
	| *|
	|* |
	+--+

The second rule changes:

	+--+
	|..|
	|  |
	+--+

into:

	+--+      +--+
	|. |  or  | .|  50% chance
	|. |      | .|
	+--+      +--+

Time is discrete in these ticks, so given some grid state at tick T all neighborhood changes appear simultaneously in tick T + 1.

Again, use whatever output you are comfortable with, from ASCII art in the terminal to pretty graphics.
