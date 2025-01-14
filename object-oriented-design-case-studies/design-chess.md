<h1 align="center">Design Chess</h1>
<h3 align="center">Let's design a system to play chess</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagram](#activity-diagram)
* [Code](#code)

Chess is a two-player strategy board game played on a chessboard, which is a checkered gameboard with 64 squares arranged in an 8×8 grid. There are a few versions of game types that people play all over the world. In this design problem, we are going to focus on designing a two-player online chess game.

<p align="center">
    <img src="/media-files/chess.png" alt="Chess">
    <br />
    Chess
</p>

### System Requirements

We’ll focus on the following set of requirements while designing the game of chess:

1. The system should support two online players to play a game of chess.
2. All rules of international chess will be followed.
3. Each player will be randomly assigned a side, black or white.
4. Both players will play their moves one after the other. The white side plays the first move.
5. Players can’t cancel or roll back their moves.
6. The system should maintain a log of all moves by both players.
7. Each side will start with 8 pawns, 2 rooks, 2 bishops, 2 knights, 1 queen, and 1 king.
8. The game can finish either in a checkmate from one side, forfeit or stalemate (a draw), or resignation.

### Use Case Diagram

We have two actors in our system:

* **Player:** A registered account in the system, who will play the game. The player will play chess moves.
* **Admin:** To ban/modify players.

Here are the top use cases for chess:

* **Player moves a piece:** To make a valid move of any chess piece.
* **Resign or forfeit a game:** A player resigns from/forfeits the game.
* **Register new account/Cancel membership:** To add a new member or cancel an existing member.
* **Update game log:** To add a move to the game log.

Here is the use case diagram of our Chess Game:

<p align="center">
    <img src="/media-files/chess-use-case-diagram.png" alt="Chess Use Case Diagram">
    <br />
    Use Case Diagram for Chess
</p>

### Class Diagram

Here are the main classes for chess:

**Player:** Player class represents one of the participants playing the game. It keeps track of which side (black or white) the player is playing.<br />
**Account:** We’ll have two types of accounts in the system: one will be a player, and the other will be an admin.<br />
**Game:** This class controls the flow of a game. It keeps track of all the game moves, which player has the current turn, and the final result of the game.<br />
**Box:** A box represents one block of the 8x8 grid and an optional piece.<br />
**Board:** Board is an 8x8 set of boxes containing all active chess pieces.<br />
**Piece:** The basic building block of the system, every piece will be placed on a box. This class contains the color the piece represents and the status of the piece (that is, if the piece is currently in play or not). This would be an abstract class and all game pieces will extend it.<br />
**Move:** Represents a game move, containing the starting and ending box. The Move class will also keep track of the player who made the move, if it is a castling move, or if the move resulted in the capture of a piece.<br />
**GameController:** Player class uses GameController to make moves.<br />
**GameView:** Game class updates the GameView to show changes to the players.<br />

<p align="center">
    <img src="/media-files/chess-class-diagram.png" alt="Chess Class Diagram">
    <br />
    Class Diagram for Chess
</p>

<p align="center">
    <img src="/media-files/chess-uml.svg" alt="Chess UML">
    <br />
    UML for Chess
</p>

### Activity Diagram

**Make move:** Any Player can perform this activity. Here are the set of steps to make a move:

<p align="center">
    <img src="/media-files/chess-activity-diagram.svg" alt="Chess Activity Diagram">
    <br />
    Activity Diagram for Chess
</p>

### Code

Here is the code for the top use cases.

Step 4: Code
Class: Piece

public abstract class Piece {
    private boolean white;
    private boolean killed = false;
    public abstract boolean canMove(Board board,Block startBlock, Block endBlock);
    public Piece(boolean white) {
        this.white = white;
    }
    public boolean isWhite() {
        return white;
    }
    public boolean isKilled() {
        return killed;
    }
    public void setKilled(boolean killed) {
        this.killed = killed;
    }
}
Class: King

public class King extends Piece {
    public King(boolean white) {
        super(white);
    }
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
}
Class: Queen

public class Queen extends Piece {
    @Override
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
    public Queen(boolean white) {
        super(white);
    }
}
Class: Bishop

public class Bishop extends Piece {
    public Bishop(boolean white) {
        super(white);
    }
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
}
Class: Knight

public class Knight extends Piece {
    public Knight(boolean white) {
        super(white);
    }
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
}
Class: Rook

public class Rook extends Piece {
    public Rook(boolean white) {
        super(white);
    }
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
}
Class: Pawn

public class Pawn extends Piece {
    public Pawn(boolean white) {
        super(white);
    }
    public boolean canMove(Board board, Block startBlock, Block endBlock) {
        return false;
    }
}
Class: Block

public class Block {
    private int x,y;
    private String label;
    private Piece piece;
    public Block(int x, int y, Piece piece) {
        this.x = x;
        this.y = y;
        this.label = assignLabel(x,y);
        this.piece = piece;
    }
    private  String assignLabel(int x, int y){
        String[] xLabels = {"1","2","3","4","5","6","7","8"};
        String[] yLabels = {"A","B","C","D","E","F","G","H"};
        return xLabels[x] + yLabels[y];
    }
    public Piece getPiece() {
        return piece;
    }
    public void setPiece(Piece piece) {
        this.piece = piece;
    }
}
Class: Board

public class Board {
    private Block[][] blocks;
    public Board() {
        initializeBoard();
    }
    private void initializeBoard(){
        // Setting White Pieces
        blocks[0][0] = new Block(0,0,new Rook(true));
        blocks[0][1] = new Block(0,1,new Knight(true));
        blocks[0][2] = new Block(0,2,new Bishop(true));
        blocks[0][3] = new Block(0,3,new Queen(true));
        blocks[0][4] = new Block(0,4,new King(true));
        blocks[0][5] = new Block(0,5,new Bishop(true));
        blocks[0][6] = new Block(0,6,new Knight(true));
        blocks[0][7] = new Block(0,7,new Rook(true));
        for(int j=0; j<8 ; j++){
            blocks[1][j] = new Block(1,j,new Pawn(true));
        }
        //Setting Black Pieces
        blocks[7][0] = new Block(7,0,new Rook(false));
        blocks[7][1] = new Block(7,1,new Knight(false));
        blocks[7][2] = new Block(7,2,new Bishop(false));
        blocks[7][3] = new Block(7,3,new Queen(false));
        blocks[7][4] = new Block(7,4,new King(false));
        blocks[7][5] = new Block(7,5,new Bishop(false));
        blocks[7][6] = new Block(7,6,new Knight(false));
        blocks[7][7] = new Block(7,7,new Rook(false));
        for(int j=0; j<8 ; j++){
            blocks[6][j] = new Block(6,j,new Pawn(false));
        }
        // Defining rest of the blocks having no pieces
        for(int i=2;i<6;i++){
            for( int j=0; j<8; j++){
                blocks[i][j] = new Block(i,j,null);
            }
        }
    }
}
Class: Move

public class Move {
    private Block startBlock;
    private Block endBlock;
    public Move(Block startBlock, Block endBlock){
        this.endBlock= endBlock;
        this.startBlock = startBlock;
    }
    public boolean isValid(){
            return !(startBlock.getPiece().isWhite() == endBlock.getPiece().isWhite());
    }
    public Block getStartBlock() {
        return startBlock;
    }
    public Block getEndBlock() {
        return endBlock;
    }
}
Enum: Status

public enum Status {
    ACTIVE, SAVED, BLACK_WIN, WHITE_WIN, STALEMATE;
}
Class: Player

public class Player {
    String name;
    public Player(String name) {
        this.name = name;
    }
    public void join(Game g){
    }
}
Class: Game

import java.util.ArrayList;

public class Game {
    private Board board;
    // Assuming player1 is always WHITE
    private Player player1;
    // Assuming player2 is always BLACK
    private Player player2;
    boolean isWhiteTurn;
    private ArrayList<Move> gameLog;
    private Status status;
    public Game(Player player1, Player player2){
        this.player1 = player1;
        this.player2 = player2;
        this.board = new Board();
        this.isWhiteTurn = true;
        this.status = Status.ACTIVE;
        this.gameLog = new ArrayList<>();
    }
    public void start(){
        // Continue the game till the status is active
        while(this.status==Status.ACTIVE){
            // player1 will make the move if its white's turn
            // else player2 will make the move
            if(isWhiteTurn){
                //makeMove(new Move(startBlock,endBlock),player1);
            }
            else{
                //makeMove(new Move(startBlock,endBlock),player2);
            }
        }
    }
    public void makeMove(Move move, Player player){
        // Initial check for valid move
        // To check if source and destination doesn't contain
        // the same color pieces.
        if (move.isValid()){
            Piece sourcePiece = move.getStartBlock().getPiece();
            // Check if source piece can be moved or not
            if(sourcePiece.canMove(this.board,move.getStartBlock(),move.getEndBlock())){
                Piece destinationPiece = move.getEndBlock().getPiece();
                // check if destination block contains some peice
                if(destinationPiece != null ){
                    // if destination block contains King
                    // and currently white is playing --> White wins
                    if(destinationPiece instanceof King && isWhiteTurn){
                        this.status = Status.WHITE_WIN;
                        return;
                    }
                    // if destination block contains King
                    // and currently Black is playing --> Black wins
                    if(destinationPiece instanceof King && !isWhiteTurn){
                        this.status = Status.BLACK_WIN;
                        return;
                    }
                    // Set the destination piece as killed
                    destinationPiece.setKilled(true);
                }
                // Adding the valid move to game logs
                gameLog.add(move);
                // Moving the source piece to the destination block
                move.getEndBlock().setPiece(sourcePiece);
                // Setting the source block to null (means it doesn't have any piece)
                move.getStartBlock().setPiece(null);
                // Toggling the turn
                // If it is white Turn, next will be Black Turn
                // else if it is Black Turn, next will be White Turn
                isWhiteTurn = !isWhiteTurn;
            }
        }
    }
}