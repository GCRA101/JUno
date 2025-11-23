# JUno

[![Project Status](https://img.shields.io/badge/status-active-brightgreen.svg)]()
[![Language](https://img.shields.io/badge/language-Java-orange.svg)]()
[![Branch](https://img.shields.io/badge/branch-main-blue.svg)]()
[![License: TODO](https://img.shields.io/badge/license-TODO-lightgrey.svg)]()

JUno is a Java implementation of the UNO card game designed with solid object-oriented principles and a layered architecture. The project separates the core game engine, rules and services, AI players, and front-end modules. It demonstrates applied design patterns (Factory, Strategy, Observer, Command) and uses the Model-View-Controller (MVC) pattern to keep the UI modular and replaceable.

![JUno Hero](project-docs/images/ViewGame.png)

Overview
--------
JUno implements UNO's core mechanics while focusing on maintainability, testability, and extensibility. The project is intended for:
- learning and demonstrating design patterns in a real-world game
- experimenting with AI strategies
- creating modular front-ends (CLI, Swing/JavaFX, web frontend)

Highlights
----------
- Clean separation: engine, services/rules, AI, UI
- Design patterns: Factory (card & player creation), Strategy (AI decision-making), Observer (event propagation), Command (player actions / undo)
- MVC-friendly so UIs can be swapped without changing the engine
- Modular AI: plug-in strategies to experiment with playing techniques

Architecture & Design
---------------------
High level layers:
- Core Engine: game state, turn flow, card effects
- Rules / Services: penalty handling, validation, scoring
- AI: pluggable Strategy implementations for CPU players
- Front-end: CLI, GUI, or headless execution that communicates with the engine via controllers

Design Patterns used
- Factory — to create and configure cards, decks and players
- Strategy — to encapsulate different AI behaviors
- Observer — to propagate game events to UIs, logs and analytics
- Command — to model player actions (play, draw, pass) and support undo if needed
- MVC — decouples UI from game model for multiple front-ends


## UML Class Diagrams

### Model

![Model](project-docs/uml_diagrams/UMLdiagram_Model.png)

### View
![View](project-docs/uml_diagrams/UMLdiagram_View.png)

### Controller
![Controller](project-docs/uml_diagrams/UMLdiagram_Controller.png)


Features
--------
- Full UNO rule support (plus configurable rule toggles)
- Multiple AI strategies (random, heuristic, aggressive, conservative)
- Turn timer support for interactive play
- Pluggable front-ends (CLI implemented; add Swing/JavaFX or web)
- Unit tests for core game logic
- Extensible card and rules engine for custom game variants

Quick Start
-----------

Requirements
- Java 11+ (Java 17 recommended)
- Maven 3.6+ or Gradle (Maven examples below)
- Git

Build (Maven)
```bash
# clone
git clone https://github.com/GCRA101/JUno.git
cd JUno

# build
mvn clean package
```

Run (packaged jar)
```bash
# if build produces target/juno.jar
java -jar target/juno.jar
```

Run (from IDE)
- Open the project in IntelliJ IDEA or Eclipse.
- Run the main class: com.gcra101.juno.App (example — replace with actual main class if different).
- Use the application arguments to choose front-end, e.g. --ui=cli or --ui=gui.

Configuration
-------------
Configuration lives in config/application.properties (create if absent). Example:
```properties
# config/application.properties
game.maxPlayers=4
game.startingHandSize=7
ai.strategy.default=heuristic
ui.mode=cli
network.enabled=false
log.level=INFO
```

Gameplay (short)
----------------
- Standard UNO rules apply: match by color or number/symbol, special cards (Skip, Reverse, Draw Two, Wild, Wild Draw Four)
- The engine validates plays, enforces Draw penalties, and checks win conditions
- Custom rule toggles allow alternative sequences or scoring

AI & Strategies
---------------
The AI subsystem provides several strategies:
- RandomStrategy — picks a random legal card
- HeuristicStrategy — prioritizes cards to reduce hand size and block opponents
- AggressiveStrategy — prioritizes Draw/Skip/Reverse to target opponents
- DefensiveStrategy — tries to hold Wild cards for critical moments

To add a strategy, implement the interface:
```java
public interface PlayStrategy {
    Card chooseCard(GameState state, Player player);
}
```

Extending JUno
--------------
Common extension points:
- Add new UI: implement the controller/view contract and register the view
- Add new AI: implement PlayStrategy and register via factory or service loader
- Add custom rules: extend RulesService and inject behavior into the engine
- Add network play: implement a network adapter that forwards player commands to the engine

Testing & Continuous Integration
-------------------------------
- Unit tests cover core engine and rules. Run:
```bash
mvn test
```
- Add GitHub Actions workflow (/.github/workflows/ci.yml) to run tests on PRs
- Recommended checks: mvn -DskipTests=false verify, static analysis (SpotBugs/Checkstyle)

License
-------

Contact & Credits
-----------------
Maintainer: GCRA101 — https://github.com/GCRA101
If you use this project or have suggestions, please open an issue or a PR.

Acknowledgements
- UNO game rules specification
- Inspiration from community projects that demonstrate clean architecture and design patterns