German University in Cairo
Media Engineering and Technology
Prof. Dr. Slim Abdennadher
CSIS 201 - Programming II, Spring 2025
Jackaroo: A New Game Spin
Milestone 1
Deadline: 14.3.2025 @ 11:59 PM
This milestone is an exercise on the concepts of Object Oriented Programming (OOP).
The following sections describe the requirements of the milestone.
By the end of this milestone, you should have:
• A structured package hierarchy for your code.
• An initial implementation for all the needed data structures.
• Basic data loading functionality from a csv file.
Note: You may utilize AI tools to assist with your milestone project. However, please be
aware that the outputs from these tools may not always be accurate or valid. Be critical of the
output and inspect it, and make any necessary modifications to make the output work to your
advantage. You may use prompt engineering techniques for more informed interaction with AI
tools. Whether you code without or with the help of AI tools, it is your full responsibility to
ensure that your submission is correct and functions as intended. If you choose to use AI tools,
it is required that you conduct your work in a dedicated AI session (e.g. ChatGPT new chat).
Before submitting your milestone, make sure to download and include the log from this session
as part of your submission, to document the use of AI assistance. Your grades in the milestone
will not be impacted by the use of AI tools; only by whether your submission works successfully
as expected in evaluation.
1 Build the Project Hierarchy
1.1 Add the packages
Create a new Java project and build the following package hierarchy:
1. engine
2. engine.board
3. model
4. model.card
5. model.player
6. model.card.standard
7. model.card.wild
8. exception
9. test
1
10. view
Afterwards, proceed by implementing the following classes. You are allowed to add more classes, attributes and methods. However, you must use the same specific names for the provided ones.
1.2 Naming and privacy conventions
Please note that all your class attributes and methods must be private for this milestone unless otherwise
stated. Your implementation should have the appropriate setters and getters conforming with the access
constraints. if a variable is said to be READ then we are allowed to get its value. If the variable is said
to be WRITE then we are allowed to change its value. Please note that getters and setters should match
the Java naming conventions unless mentioned otherwise. If the instance variable is of type boolean, the
getter method name starts by is followed by the exact name of the instance variable. Otherwise, the
method name starts by the verb (get or set) followed by the exact name of the instance variable; the
first letter of the instance variable should be capitalized. Please note that the method names are case
sensitive.
Example 1 You want a getter for an instance variable called milkCount → Method name = getMilkCount()
Example 2 You want a setter for an instance variable called milkCount → Method name = setMilkCount()
Example 3 You want a getter for a boolean variable called alive → Method name = isAlive()
Throughout the whole milestone, if an attribute will never be changed once initialized, you should declare
it as final. If a particular member (variable or method) belongs to the class, rather than instances of the
class then it’s said to be static. Combining both is commonly used for defining constants that should
be accessible without creating an instance of the class and whose value remains constant throughout the
program.
Example 4 You want a constant price value for each instance → final int price = 100;
Example 5 You want a counter that will be shared by all instances → static int counter = 0;
Example 6 You want a constant code shared by all instances → static final int code = 1;
2 Build the Enums
2.1 Build the Colour Enum
Name : Colour
Package : model
Type : Enum
Description : An enum representing the four colours of the marbles. Possible values are: RED,
GREEN, BLUE, YELLOW.
2.2 Build the CellType Enum
Name : CellType
Package : engine.board
Type : Enum
Description : An enum representing the four states of the cells. Possible values are: NORMAL, SAFE,
BASE, ENTRY
2
2.3 Build the Suit Enum
Name : Suit
Package : model.card.standard
Type : Enum
Description : An enum representing the four suits of the cards. Possible values are: HEART, DIAMOND, SPADE, CLUB.
3 Build the Interfaces
Interfaces define a set of abstract functionalities that a class can implement, allowing it to perform specific
actions. Classes should implement the interfaces that allow them to do their specified functionality.
Interface methods must be public.
3.1 Build the GameManager Interface
Name : GameManager
Package : engine
Type : Interface
Description : An interface that will allow other classes down the hierarchy to communicate with the
Game class.
3.2 Build the BoardManager Interface
Name : BoardManager
Package : engine.board
Type : Interface
Description : An interface that will allow other classes down the hierarchy to communicate with the
Board class.
3.2.1 Methods
1. int getSplitDistance(): Further information will be provided in the Board class section.
4 Build the Classes
4.1 Build the Marble Class
Name : Marble
Package : model.player
Type : class.
Description : A class representing the Marbles available in the game.
4.1.1 Attributes
1. Colour colour: An enum representing the colour of the marble, and associating it to a Player.
Further information will be provided in the Player class section. This attribute is READ ONLY
and cannot be change once initialized.
3
4.1.2 Constructors
1. Marble(Colour colour): Constructor that initializes a Marble object with the colour as attribute.
4.2 Build the Cell Class
Name : Cell
Package : engine.board
Type : class.
Description : A class representing the Cells available on the board.
4.2.1 Attributes
All Cell attributes are both READ and WRITE.
1. Marble marble: An object of type Marble where it’s either null or occupied by a marble object.
2. CellType cellType: An enum of type CellType specifying the type of cell.
3. boolean trap: a boolean value determining whether the cell is a trap cell or not.
4.2.2 Constructors
1. Cell(CellType cellType): Constructor that initializes a Cell object with the cell type and sets
the marble to null, and trap to false.
4.3 Build the Safe Zone Class
Name : SafeZone
Package : engine.board
Type : class.
Description : A class representing any Safe Zone available on the board.
4.3.1 Attributes
All SafeZone attribute is READ ONLY and cannot be change once initialized.
1. Colour colour: An object of type colour, associating the zone to a Player. Further information
will be provided in the Player class section.
2. ArrayList<Cell> cells: An arraylist of cells representing the 4 cells of a safezone.
4.3.2 Constructors
1. SafeZone(Colour colour): Constructor that initializes a Safe zone object with the specified
colour and creates 4 SAFE cells in the arraylist of cells.
4.4 Build the Card Class
Name : Card
Package : model.card
Type : Abstract Class
Description : A class representing Cards in the game. No objects of type Card can be instantiated.
4
4.4.1 Attributes
1. String name: A string representing the name of the card. This attribute is READ ONLY and
cannot be changed once initialized.
2. String description: A string representing the action of the card. This attribute is READ ONLY
and cannot be changed once initialized.
3. protected BoardManager boardManager: The current board instance, initialized by the Game
class, wrapped as the interface BoardManager.
4. protected GameManager gameManager: The current game instance wrapped as the interface
GameManager.
4.4.2 Constructors
1. Card(String name, String description, BoardManager boardManager, GameManager gameManager):
Constructor that initializes a Card object with the given parameters.
4.4.3 Subclasses
The game features two main types of cards: Standard Cards and Wild Cards. Each type is a subclass
of the Card class and further subdivides into specific card types, each defined in its respective class
within the appropriate package. There are 8 different types of standard cards available in the game and
2 different wild cards. Each type is modeled as a subclass of the Standard or Wild card class. Each
type should be implemented in a separate class within the same package as the parent class. Each of
the subclasses representing the different action cards should have its own constructor that utilizes the
Standard card or Wild card constructor. Carefully consider the design of the constructor of each subclass.
4.5 Build the Standard Class
Name : Standard
Package : model.card.standard
Type : Class
Description : A class representing the standard deck cards available in the game. This class is a
subclass of the Card class.
Subclasses : A standard card has the following 8 subclasses: Ace, King, Queen, Jack, Four, Five,
Seven, Ten
4.5.1 Attributes
All attributes are READ ONLY and cannot be changed once initialized.
1. int rank: An int representing the rank (number) of a standard card.
2. Suit suit: An enum representing the suit of a standard card.
4.5.2 Constructors
1. Standard(String name, String description, int rank, Suit suit, BoardManager boardManager,
GameManager gameManager): Constructor that initializes a Standard object with the given parameters.
5
4.6 Build the Ace Class
Name : Ace
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 1.
4.6.1 Constructors
1. Ace(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes an Ace object with the given parameters and sets the
rank to 1.
4.7 Build the King Class
Name : King
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 13.
4.7.1 Constructors
1. King(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a King object with the given parameters and sets the
rank to 13.
4.8 Build the Queen Class
Name : Queen
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 12.
4.8.1 Constructors
1. Queen(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Queen object with the given parameters and sets the
rank to 12.
4.9 Build the Jack Class
Name : Jack
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 11.
4.9.1 Constructors
1. Jack(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Jack object with the given parameters and sets the
rank to 11.
6
4.10 Build the Ten Class
Name : Ten
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 10.
4.10.1 Constructors
1. Ten(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Ten object with the given parameters and sets the
rank to 10.
4.11 Build the Seven Class
Name : Seven
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 7.
4.11.1 Constructors
1. Seven(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Seven object with the given parameters and sets the
rank to 7.
4.12 Build the Five Class
Name : Five
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 5.
4.12.1 Constructors
1. Five(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Five object with the given parameters and sets the
rank to 5.
4.13 Build the Four Class
Name : Four
Package : model.card.standard
Type : Class
Description : A subclass of Standard representing a card of rank 4.
4.13.1 Constructors
1. Four(String name, String description, Suit suit, BoardManager boardManager, GameManager
gameManager): Constructor that initializes a Four object with the given parameters and sets the
rank to 4.
7
4.14 Build the Wild Class
Name : Wild
Package : model.card.wild
Type : Abstract Class
Description : A class representing the wild cards available in the game. This class is a subclass of the
Card class. No objects of type Wild can be instantiated.
Subclasses : A wild card has the following 2 subclasses: Burner, Saver
4.14.1 Constructors
1. Wild(String name, String description, BoardManager boardManager, GameManager gameManager):
Constructor that initializes a Wild card with the given parameters.
4.15 Build the Burner Class
Name : Burner
Package : model.card.wild
Type : Class
Description : A subclass of Wild representing a special card.
4.15.1 Constructors
1. Burner(String name, String description, BoardManager boardManager, GameManager gameManager):
Constructor that initializes a Burner object with the given parameters.
4.16 Build the Saver Class
Name : Saver
Package : model.card.wild
Type : Class
Description : A subclass of Wild representing a special card.
4.16.1 Constructors
1. Saver(String name, String description, BoardManager boardManager, GameManager gameManager):
Constructor that initializes a Saver object with the given parameters.
4.17 Build the Deck Class
Name : Deck
Package : model.card
Type : Class
Description : A class representing the deck of cards in the game. Used to import data from a given
csv file. The imported data is then used to create and initialize cards for the deck and fill them
with the entries from the csv file. The csv file should be placed in the same directory as the .src
folder and not inside it.
Description of Cards CSV file
1. Each line represents the information of a single card.
2. The data has no header, i.e. the first line represents the first card.
8
3. The parameters are separated by a comma (,).
4. The line represents the cards’ data as follows: {code, frequency, name, description} or
{code, frequency, name, description, rank, suit} based on the type of card (rank and
suit are added only if the card type is standard).
For more details, refer to the example in game description.
4.17.1 Attributes
1. String CARDS FILE: A String containing the name of the card’s csv file. This attribute cannot be
changed once initialized and is a member of the class rather than its instances.
2. ArrayList<Card> cardsPool: Arraylist to store the available cards. This attribute is a member
of the class rather than its instances.
4.17.2 Methods
1. public static void loadCardPool(BoardManager boardManager, GameManager gameManager)
throws IOException: reads the csv file and instantiates the right card based on the code (first
column of the csv). This card is added to the cardsPool according to the number of its frequency. For example, a frequency of 5 means the card will have 5 copies of that card added to the
cardsPool.
The code will either be the rank of the card for the Standard subclasses (Ace, King, Queen, Ten,
Seven, Five, Four), 14 for the Burner class, 15 for the Saver Class, or 0 for representing the
rest of the Standard cards, all initialized card should have the values of the boardManager and
gameManager passed to them.
2. public static ArrayList<Card> drawCards(): Shuffles the cardsPool, then removes and returns the first four cards from it.
4.18 Build the Player Class
Name : Player
Package : model.player
Type : class.
Description : A class representing the Players available in the game.
4.18.1 Attributes
1. String name: A String representing the name of a player. This attribute is READ ONLY and
cannot be changed once initialized.
2. Colour colour: An object of type Colour acting as a reference to associate a player to their
SafeZone and Marbles. This attribute is READ ONLY and cannot be changed once initialized.
3. ArrayList<Card> hand: An arraylist representing the hand of cards each player has. This attribute is both READ and WRITE.
4. ArrayList<Marble> marbles: An arraylist representing the marbles each player has in their Home
Zone. This attribute is READ ONLY. Also, this attribute cannot be changed once initialized.
5. Card selectedCard: A Card object representing the card to be played. This attribute is READ
ONLY.
6. ArrayList<Marble> selectedMarbles: An arraylist representing the marbles to be played. This
attribute is neither READ nor WRITE. Also, This attribute cannot be changed once initialized.
9
4.18.2 Constructors
1. Player(String name, Colour colour): Constructor that initializes a Player object with the
player name and colour as attributes, and does the following:
1. Initialize the hand, selectedMarbles, and marbles to empty ArrayLists
2. Create 4 marbles with the same colour as the player and add them to the marbles.
3. Initialize the selectedCard to null (Default Value)
4.18.3 Subclasses
The game features automated players that will play against the Human player, this is represented in the
subclass CPU.
4.19 Build the CPU Class
Name : CPU
Package : model.player
Type : class.
Description : A subclass of the Player class representing the CPU players available in the game.
4.19.1 Attributes
1. BoardManager boardManager: The current board instance, initialized by the Game class, wrapped
as the interface BoardManager. This attribute cannot be changed once initialized.
4.19.2 Constructors
1. CPU(String name, Colour colour, BoardManager boardManager): Constructor that initializes a CPU object with the given parameters and initializes the board manager with the given
parameter.
4.20 Build the Board Class
Name : Board
Package : engine.board
Type : class.
Description : A class representing the game Board, implementing the BoardManager interface.
4.20.1 Attributes
1. GameManager gameManager: The active game instance wrapped as the interface GameManager.
This attribute cannot be changed once initialized.
2. ArrayList<Cell> track: An arraylist representing the general track. This attribute is READ
ONLY and cannot be changed once initialized.
3. ArrayList<SafeZone> safeZones: An arraylist representing each player’s safe zone. This attribute is READ ONLY and cannot be changed once initialized.
4. int splitDistance: An integer specifying how to split 7 moves between two marbles. This is
attribute is READ (through a relevant interface method) and WRITE.
10
4.20.2 Constructors
1. Board(ArrayList<Colour> colourOrder, GameManager gameManager): Constructor that initializes a Board object by doing the following:
1. Set the gameManager to the passed parameter.
2. Initializes the track, and safeZones to empty ArrayLists
3. Sets the splitDistance to 3.
4. Set the track with the correct type of cells whether BASE, Safe Zone ENTRY or NORMAL according
to what is mentioned in the game description.
5. Change 8 random NORMAL track cells to be flagged as trap using the below assignTrapCell
method.
6. Create 4 SafeZones and add them to the safeZones with the given colour order.
4.20.3 Methods
1. void assignTrapCell() should randomize a cell position on the track and flag it as a trap cell.
The position must be a NORMAL cell and not flagged as trap already.
Game Setup
4.21 Build the Game Class
Name : Game
Package : engine
Type : Class
Description : A class representing the Game itself, implementing the GameManager interface. This class
will represent the main engine of the game.
4.21.1 Attributes
1. Board board: An Object representing the game board. This attribute is READ ONLY and cannot
be changed once initialized.
2. ArrayList<Player> players: An arraylist representing the players participating in the game.
This attribute is READ ONLY and cannot be changed once initialized.
3. ArrayList<Card> firePit: An arraylist representing the cards that have been played / discarded
in the game. This attribute is READ ONLY and cannot be changed once initialized.
4. int currentPlayerIndex: An integer representing which of the players should play next.
5. int turn: An integer representing the current game turn.
4.21.2 Constructors
1. Game(String playerName) throws IOException: Constructor that initializes a Game object with
the specified parameters and:
1. Initializes the game board with a list of all the available colours in a random order (shuffled).
Also, passing this game’s reference as GameManager to the board.
2. Loads the card pool from the deck to ensure all cards are ready for gameplay. This is facilitated
by the Deck.loadCardPool method, passing the reference of this game as GameManager, and
the created board as a BoardManager.
3. Creates a list of players, adding a human player with the name and the first colour in the
shuffled colour order list.
11
4. Creates CPU players named "CPU 1", "CPU 2", "CPU 3" with each subsequent colour, passing
the created board as a BoardManager to each of them.
5. Distributes a set of 4 cards to each player’s hand from a central deck using the Deck.drawCards
method.
6. Sets the initial values for tracking the current player index and the game turn counter to 0.
7. Initializes the firepit with an empty arrayList.
5 Build the Exceptions
5.1 Build the Game Exception Class
Name : GameException
Package : exception
Type : Abstract class.
Description : Class representing a generic exception that can occur during game play. These exceptions
arise from any invalid action that is performed. This class is a subclass of java’s Exception class.
No objects of type GameException can be instantiated.
5.1.1 Constructors
1. GameException(): Initializes an instance of a GameException by calling the constructor of the
super class.
2. GameException(String message): Initializes an instance of a GameException by calling the constructor of the super class with a customized message.
5.1.2 Subclasses
This class has two abstract subclasses: InvalidSelectionException and ActionException which have
their own subclasses.
5.2 Build the Invalid Selection Exception Class
Name : InvalidSelectionException
Package : exception
Type : Abstract Class
Description : Class representing an exception that can occur whenever an invalid selection is made.
This class is a subclass of GameException class. This class cannot be instantiated.
Subclasses : An InvalidSelectionException has the following 3 subclasses: InvalidMarbleException,
InvalidCardException, SplitOutOfRangeException
5.2.1 Constructors
1. InvalidSelectionException(): Initializes an instance of an InvalidSelectionException by
calling the constructor of the super class.
2. InvalidSelectionException(String message): Initializes an instance of an InvalidSelectionException
by calling the constructor of the super class with a customized message.
12
5.3 Build the Invalid Card Selection Exception Class
Name : InvalidCardException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an invalid card is selected in
the game. This class is a subclass of InvalidSelectionException class.
5.3.1 Constructors
1. InvalidCardException(): Initializes an instance of an InvalidCardException by calling the
constructor of the super class.
2. InvalidCardException(String message): Initializes an instance of an InvalidCardException
by calling the constructor of the super class with a customized message.
5.4 Build the Invalid Marble Selection Exception Class
Name : InvalidMarbleException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an invalid marble is selected
in the game. This class is a subclass of InvalidSelectionException class.
5.4.1 Constructors
1. InvalidMarbleException(): Initializes an instance of an InvalidMarbleException by calling
the constructor of the super class.
2. InvalidMarbleException(String message): Initializes an instance of an InvalidMarbleException
by calling the constructor of the super class with a customized message.
5.5 Build the Split Out Of Range Exception Class
Name : SplitOutOfRangeException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an invalid split distance is
chosen. This class is a subclass of InvalidSelectionException class.
5.5.1 Constructors
1. SplitOutOfRangeException(): Initializes an instance of an SplitOutOfRangeException by calling the constructor of the super class.
2. SplitOutOfRangeException(String message): Initializes an instance of an SplitOutOfRangeException
by calling the constructor of the super class with a customized message.
13
5.6 Build the Action Exception Class
Name : ActionException
Package : exception
Type : Abstract Class
Description : Class representing an exception that can occur whenever an illegal move is done throughout the game. This class is a subclass of GameException class. This class cannot be instantiated.
Subclasses : An ActionException has the following 5 subclasses: IllegalMovementException,
IllegalSwapException, IllegalDestroyException, CannotFieldException, CannotDiscardException
5.6.1 Constructors
1. ActionException(): Initializes an instance of an ActionException by calling the constructor of
the super class.
2. ActionException(String message): Initializes an instance of an ActionException by calling
the constructor of the super class with a customized message.
5.7 Build the Illegal Movement Exception Class
Name : IllegalMovementException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an illegal marble movement
occurs in the game. This class is a subclass of ActionException class.
5.7.1 Constructors
1. IllegalMovementException(): Initializes an instance of an IllegalMovementException by calling the constructor of the super class.
2. IllegalMovementException(String message): Initializes an instance of an IllegalMovementException
by calling the constructor of the super class with a customized message.
5.8 Build the Illegal Swap Exception Class
Name : IllegalSwapException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an illegal marble swap occurs
in the game. This class is a subclass of ActionException class.
5.8.1 Constructors
1. IllegalSwapException(): Initializes an instance of an IllegalSwapException by calling the
constructor of the super class.
2. IllegalSwapException(String message): Initializes an instance of an IllegalSwapException
by calling the constructor of the super class with a customized message.
14
5.9 Build the Illegal Destroy Exception Class
Name : IllegalDestroyException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an invalid action happens that
would lead to returning the marble to its Home Zone. This class is a subclass of ActionException
class.
5.9.1 Constructors
1. IllegalDestroyException(): Initializes an instance of an IllegalDestroyException by calling
the constructor of the super class.
2. IllegalDestroyException(String message): Initializes an instance of an IllegalDestroyException
by calling the constructor of the super class with a customized message.
5.10 Build the Cannot Field Exception Class
Name : CannotFieldException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever a marble cannot be placed on
board. This class is a subclass of ActionException class.
5.10.1 Constructors
1. CannotFieldException(): Initializes an instance of a CannotFieldException by calling the constructor of the super class.
2. CannotFieldException(String message): Initializes an instance of a CannotFieldException
by calling the constructor of the super class with a customized message.
5.11 Build the Cannot Discard Exception Class
Name : CannotDiscardException
Package : exception
Type : Class
Description : Class representing an exception that can occur whenever an invalid card discard occurs.
This class is a subclass of ActionException class.
5.11.1 Constructors
1. CannotDiscardException(): Initializes an instance of a CannotDiscardException by calling the
constructor of the super class.
2. CannotDiscardException(String message): Initializes an instance of a CannotDiscardException
by calling the constructor of the super class with a customized message.
15
