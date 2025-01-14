<h1 align="center">Design Cricinfo</h1>
<h3 align="center">Let's design Cricinfo</h3>

**We'll cover the following:**

* [System Requirements](#system-requirements)
* [Use Case Diagram](#use-case-diagram)
* [Class Diagram](#class-diagram)
* [Activity Diagram](#activity-diagram)
* [Code](#code)

Cricinfo is a sports news website exclusively for the game of cricket. The site features live coverage of cricket matches containing ball-by-ball commentary and a database for all the historic matches. The site also provides news and articles about cricket.

<p align="center">
    <img src="/media-files/cricinfo.png" alt="Cricinfo">
    <br />
    Cricinfo
</p>

### System Requirements

We will focus on the following set of requirements while designing Cricinfo:

1. The system should keep track of all cricket-playing teams and their matches.
2. The system should show live ball-by-ball commentary of cricket matches.
3. All international cricket rules should be followed.
4. Any team playing a tournament will announce a squad (a set of players) for the tournament.
5. For each match, both teams will announce their playing-eleven from the tournament squad.
6. The system should be able to record stats about players, matches, and tournaments.
7. The system should be able to answer global stats queries like, “Who is the highest wicket taker of all time?”, “Who has scored maximum numbers of 100s in test matches?”, etc.
8. The system should keep track of all ODI, Test and T20 matches.

### Use Case Diagram

We have two main Actors in our system:

* **Admin:** An Admin will be able to add/modify players, teams, tournaments, and matches, and will also record ball-by-ball details of each match.
* **Commentator:** Commentators will be responsible for adding ball-by-ball commentary for matches.

Here are the top use cases of our system:

* **Add/modify teams and players:** An Admin will add players to teams and keeps up-to-date information about them in the system.
* **Add tournaments and matches:** Admins will add tournaments and matches in the system.
* Add ball: Admins will record ball-by-ball details of a match.
* **Add stadium, umpire, and referee:** The system will keep track of stadiums as well as of the umpires and referees managing the matches.
* **Add/update stats:** Admins will add stats about matches and tournaments. The system will generate certain stats.
* **Add commentary:** Add ball-by-ball commentary of matches.

Here is the use case diagram of Cricinfo:

<p align="center">
    <img src="/media-files/cricinfo-use-case-diagram.svg" alt="Cricinfo Use Case Diagram">
    <br />
    Use Case Diagram for Cricinfo
</p>

### Class Diagram

Here are the main classes of the Cricinfo system:

* **Player:** Keeps a record of a cricket player, their basic profile and contracts.
* **Team:** This class manages cricket teams.
* **Tournament:** Manages cricket tournaments and keeps track of the points table for all playing teams.
* **TournamentSquad:** Each team playing a tournament will announce a set of players who will be playing the tournament. TournamentSquad will encapsulate that.
* **Playing11:** Each team playing a match will select 11 players from their announced tournaments squad.
* **Match:** Encapsulates all information of a cricket match. Our system will support three match types: 1) ODI, 2) T20, and 3) Test
* **Innings:** Records all innings of a match.
* **Over:** Records details about an Over.
* **Ball:** Records every detail of a ball, such as the number of runs scored, if it was a wicket-taking ball, etc.
* **Run:** Records the number and type of runs scored on a ball. The different run types are: Wide, LegBy, Four, Six, etc.
* **Commentator and Commentary:** The commentator adds ball-by-ball commentary.
* **Umpire and Referee:** These classes will store details about umpires and referees, respectively.
* **Stat:** Our system will keep track of the stats for every player, match and tournament.
* **StatQuery:** This class will encapsulate general stat queries and their answers, like “Who has scored the maximum number of 100s in ODIs?” or, “Which bowler has taken the most wickets in test matches?”, etc.

<p align="center">
    <img src="/media-files/cricinfo-class-diagram.png" alt="Cricinfo Class Diagram">
    <br />
    Class Diagram for Cricinfo
</p>

<p align="center">
    <img src="/media-files/cricinfo-uml.svg" alt="Cricinfo UML">
    <br />
    UML for Cricinfo
</p>

### Activity Diagram

**Record a Ball of an Over:** Here are the steps to record a ball of an over in the system:

<p align="center">
    <img src="/media-files/cricinfo-activity-diagram.svg" alt="Cricinfo Activity Diagram">
    <br />
    Activity Diagram for Cricinfo
</p>

### Code

Here is the high-level definition for the classes described above.

// Enums representing various states and types in the cricket management system

public enum MatchFormat {
    ODI, T20, TEST
}

public enum MatchResult {
    LIVE, FINISHED, DRAWN, CANCELED
}

public enum UmpireType {
    FIELD, RESERVED, TV
}

public enum WicketType {
    BOLD, CAUGHT, STUMPED, RUN_OUT, LBW, RETIRED_HURT, HIT_WICKET, OBSTRUCTING
}

public enum BallType {
    NORMAL, WIDE, WICKET, NO_BALL
}

public enum RunType {
    NORMAL, FOUR, SIX, LEG_BYE, BYE, NO_BALL, OVERTHROW
}

// Supporting Address class
public class Address {
    private String streetAddress;
    private String city;
    private String state;
    private String zipCode;
    private String country;

    // Constructor, Getters, and Setters are omitted for brevity
}

// Abstract Person class
public abstract class Person {
    private String name;
    private Address address;
    private String email;
    private String phone;

    // Constructor, Getters, and Setters are omitted for brevity
}

// Player class representing a cricket player
public class Player extends Person {
    private List<PlayerContract> contracts = new ArrayList<>();

    public boolean addContract(PlayerContract contract) {
        contracts.add(contract);
        return true;
    }
}

// Admin class handling administrative tasks
public class Admin extends Person {
    public boolean addMatch(Match match) {
        System.out.println("Match added: " + match);
        return true;
    }

    public boolean addTeam(Team team) {
        System.out.println("Team added: " + team.getName());
        return true;
    }

    public boolean addTournament(Tournament tournament) {
        System.out.println("Tournament added: " + tournament.getName());
        return true;
    }
}

// Umpire class managing umpiring tasks
public class Umpire extends Person {
    public boolean assignMatch(Match match) {
        System.out.println("Umpire assigned to match: " + match.getMatchNumber());
        return true;
    }
}

// Referee class handling refereeing tasks
public class Referee extends Person {
    public boolean assignMatch(Match match) {
        System.out.println("Referee assigned to match: " + match.getMatchNumber());
        return true;
    }
}

// Commentator class handling match commentary, with Observer pattern
public class Commentator extends Person implements Observer {
    private List<Match> assignedMatches = new ArrayList<>();

    public boolean assignMatch(Match match) {
        assignedMatches.add(match);
        match.addObserver(this);
        System.out.println("Commentator assigned to match: " + match.getMatchNumber());
        return true;
    }

    @Override
    public void update(String commentaryText) {
        System.out.println("Commentator received update: " + commentaryText);
    }
}

// Observer interface for notifying Commentators about match updates
interface Observer {
    void update(String message);
}

// Observable Match class implementing match updates and observer management
public abstract class Match {
    private int number;
    private Date startTime;
    private MatchResult result;
    private List<Observer> observers = new ArrayList<>();

    private Playing11[] teams = new Playing11[2];
    private List<Inning> innings = new ArrayList<>();
    private List<Umpire> umpires = new ArrayList<>();
    private Referee referee;
    private List<Commentator> commentators = new ArrayList<>();
    private Stadium stadium;

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }

    public void assignStadium(Stadium stadium) {
        this.stadium = stadium;
    }

    public void assignReferee(Referee referee) {
        this.referee = referee;
    }

    public int getMatchNumber() {
        return number;
    }

    public void addCommentary(String commentaryText) {
        notifyObservers(commentaryText);
    }

    // Other match-specific methods omitted for brevity
}

// Specific match types using the Factory Pattern
public class ODI extends Match {
    // ODI-specific methods
}

public class Test extends Match {
    // Test-specific methods
}

public class T20 extends Match {
    // T20-specific methods
}

// Factory to create different match formats
public class MatchFactory {
    public static Match createMatch(MatchFormat format) {
        switch (format) {
            case ODI:
                return new ODI();
            case T20:
                return new T20();
            case TEST:
                return new Test();
            default:
                throw new IllegalArgumentException("Unknown format");
        }
    }
}

// Team class representing a cricket team
public class Team {
    private String name;
    private List<Player> players = new ArrayList<>();
    private Coach coach;

    public boolean addPlayer(Player player) {
        players.add(player);
        return true;
    }

    public boolean addNews(News news) {
        System.out.println("News added to team: " + name);
        return true;
    }

    public String getName() {
        return name;
    }
}

// Tournament-related classes
public class Tournament {
    private String name;
    private List<Team> teams = new ArrayList<>();

    public String getName() {
        return name;
    }
}

public class TournamentSquad {
    private List<Player> players = new ArrayList<>();

    public boolean addPlayer(Player player) {
        players.add(player);
        return true;
    }
}

// Playing11 class representing the final playing squad for a match
public class Playing11 {
    private List<Player> players = new ArrayList<>();
    private Player twelfthMan;

    public boolean addPlayer(Player player) {
        players.add(player);
        return true;
    }
}

// Ball-by-ball representation
public class Ball {
    private Player bowledBy;
    private Player playedBy;
    private BallType type;
    private Wicket wicket;
    private List<Run> runs = new ArrayList<>();
    private Commentary commentary;

    public void addRun(Run run) {
        runs.add(run);
    }

    public void addWicket(Wicket wicket) {
        this.wicket = wicket;
    }
}

// Over class representing an over in the match
public class Over {
    private int number;
    private List<Ball> balls = new ArrayList<>();

    public void addBall(Ball ball) {
        balls.add(ball);
    }
}

// Inning class representing an inning in the match
public class Inning {
    private int number;
    private Date startTime;
    private List<Over> overs = new ArrayList<>();

    public boolean addOver(Over over) {
        overs.add(over);
        return true;
    }
}

// Wicket class representing a wicket event
public class Wicket {
    private WicketType type;
    private Player playerOut;
    private Player caughtBy;
    private Player runoutBy;
    private Player stumpedBy;
}

// Commentary class for ball-by-ball commentary
public class Commentary {
    private String text;
    private Date createdAt;
    private Commentator createdBy;

    public Commentary(String text, Commentator createdBy) {
        this.text = text;
        this.createdBy = createdBy;
        this.createdAt = new Date();
    }
}

// Stadium class for the match location
public class Stadium {
    private String name;
    private Address location;

    public String getName() {
        return name;
    }
}

// Run class representing runs scored in a ball
public class Run {
    private RunType type;
    private int value;

    public Run(RunType type, int value) {
        this.type = type;
        this.value = value;
    }

    public int getValue() {
        return value;
    }
}

// Main class to demonstrate the use of the system
public class Main {
    public static void main(String[] args) {
        Admin admin = new Admin();
        Match match = MatchFactory.createMatch(MatchFormat.T20);
        admin.addMatch(match);

        Commentator commentator = new Commentator();
        commentator.assignMatch(match);

        match.addCommentary("Batsman hits a four!");
    }
}