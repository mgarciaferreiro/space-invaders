=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=
CIS 120 Game Project README
PennKey: martagf
=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=:=

===================
=: Core Concepts :=
===================

- List the four core concepts, the features they implement, and why each feature
  is an appropriate use of the concept. Incorporate the feedback you got after
  submitting your proposal.

  1. Appropriately modeling state using 2-D arrays: The aliens are stored in a 2D array of aliens.
  I iterate through the array with for loops in order to check if any of the aliens have been shot,
  if any of them have reached the bottom, etc. Using a 2D array is appropriate becaause the aliens
  form a grid, and it is an easy way to create them at the appropriate locations and to access an
  alien at a specific position easily (which is necessary for dropping bombs from a random alien).

  2. Appropriately modeling state using collections: The levels are stored in a LinkedList.
  The levels should be in a list because they should be in order. We only need to go 
  from one level to the next, so we don't need to be able to get a level at a specific index
  which would be what we would use an ArrayList for. A LinkedList gives us quick access to the
  first element of the list, which is all we need.
  
  3. File I/O: I use file I/O to store the high scores even after closing the game. The Game class
  has a method that reads all the lines (in the format "Marta: 500") stored in the file and stores 
  them in an ArrayList, a method that adds a new line to the list in the correct position 
  (to keep them in order) by using parseInt on the substring after ":" and comparing them, and
  a method that updates the file by writing the lines in the array to the file.

  4. Using JUnit on a testable component of your game: the normal game state and edge cases 
  are tested. The GameTest creates a GameCourt and manipulates it using the GameCourt class 
  methods to move aliens, bombs and shots and check that the game state is updated correctly.
  Some of the edge cases are if bombs and shots intersect (nothing should happen), if an alien
  reaches the bottom of the frame (we lose the game, even though we usually would get shot
  before this), if we pass the last level (the game should end, this is highly unlikely 
  because they get really hard), if non visible shots hit aliens, etc.


=========================
=: Your Implementation :=
=========================

- Provide an overview of each of the classes in your code, and what their
  function is in the overall game.
  
  	Game.java: main runnable class that specifies the frame of the GUI and the buttons to control and show
	game state (new game, save score, instructions, score board). It also writes to and reads from a document
	that stores all time sorted highest scores.
	
	GameCourt.java: holds the primary game logic for how different objects interact with one another.
	Starts timer and calls a tick function every x seconds that repaints the objects, plays sounds and 
	updates the game state based on the objects' interactions. Defines reset, end game and next level 
	methods that update game state, and defines getter methods used in the game class and for testing.
	
	GameObj.java: defines position, velocity, size and bounds of an object in the game and 
	whether it is visible, and has an abstract draw method. Objects move according to their velocity,
	which can change if they hit other objects of walls.
	
	Direction.java: enumeration defining directions, used to determine what direction an object 
	would bounce in after hitting something, used to check if a bomb will hit the ground.
	
	Subclasses of GameObj:
	
	Alien.java: defines the image, size and initial velocity of an alien, 
	overrides the draw method.
	
	UFO.java: defines the image, width, height, initial position and initial velocity of a UFO, 
	overrides the draw method.
	
	Spaceship.java: defines the image, size, initial position and initial velocity of a spaceship, 
	overrides the draw method.
	
	Bomb.java: defines the image, size, and initial velocity of a bomb (dropped by an enemy), 
	overrides the draw method.
	
	Shot.java: defines the image, size, and initial velocity of a shot (shot by spaceship), 
	overrides the draw method.
	
	Level.java: defines levelNumber, speedOfAliens, speedOfUFO, and frequencyOfBombs of a level,
	and has getter methods for each of them.


- Were there any significant stumbling blocks while you were implementing your
  game (related to your design, or otherwise)?
  
  	I was over thinking how game state should be modeled, because I had the mind set 
  	that the whole game court should be like a board and I should know what is in each
  	"square" at all times, but keeping score, position and visibility of objects is also
  	a valid way to model and test game state. This notion made me want to redesign my
  	entire game at one point, but I realized eventually that my design could be tested
  	as it was.
  	
- Evaluate your design. Is there a good separation of functionality? How well is
  private state encapsulated? What would you refactor, if given the chance?
  	
  	Private state is well encapsulated, and can only be accessed with getter and setter
  	methods. If I could re do this assignment, I would separate my "tick" method 
  	into even more individual functions from the beginning, for clarity and so all of 
  	them could be tested separately, like nextLevel, shoot and dropBomb which were inside 
  	tick in my first design.


========================
=: External Resources :=
========================

- Cite any external resources (libraries, images, tutorials, etc.) that you may
  have used while implementing your game.

	I used images from Google images for the background and objects. I looked at this 
	website https://sites.psu.edu/jeffist/2014/12/06/playing-audio-in-java-applications/
	to learn how to add sound to my game. I downloaded my wav sounds from 
	http://soundbible.com.
	