# Coin-Wheel-Game

A Game for fun and analysis.

## Repo URL

https://github.com/AgileSoftwareArchitects/coin-wheel-game

## Delivery
This delivery is published at `./delivery/20181022-2039/` available in the repository above.

----------------------
### How to run
* This product is an implementation of the StrategicPlayer interface (src/StrategicPlayer.java). As such, no main method is implemented.
* In this delivery, the ant task `report` runs the software and demonstrates certain requirements are met. This serves as "running" the product in this delivery.
* Primary requirements tested for in this delivery
    * For non-4/2 games, Player objects
        * successfully begin a game
        * successfully return a properly formatted request to reveal the correct number of coins
        * successfully return a properly formatted request to update the wheel state based on coins revealed
    * For 4/2 games Player objects are guaranteed to win each game in 5 turns or less

### New in this delivery
* ant tasks
    * `report`: HTML formatted JUnit test results summary
    * `doc-private`: HTML formatted JavaDoc documentation including private info for all classes 
    * `format`: HTML formatted representation of all source and test code
    * `checkstyle`: HTML formatted results of checkstyle code analysis
    * `coverage`: HTML formatted reports for JaCoCo test coverage analysis
    * `pmd`: HTML formatted results of pmd static analysis
    * `cpd`: HTML formatted results of cpd static analysis

  NOTE: checkstyle, pmd, and cpd will report issues at this stage. Efforts to revise source code to address the issues reported will be in a future sprint

* Cleaned up code
    * Significant refactors in
        * src/Player.java
        * src/Utility.java to hold frequently used static utility methods
        * src/Wheel.java added to hold wheel responsibilities
        * test/PlayerTest.java
        * test/WheelTest.java added to test the wheel class
    * test/PlayerTest.java now relies on src/Wheel.java to implement wheel functionality for testing

-----------------------
### Game Description:

A wheel that contains a ring of coins.

A player may choose the number of coins, number of coins to reveal, and max number of spins. 

All coin states are initially hidden from the player.  

The wheel is considered to be in winning state when all coins are of the same face.

During a game a player attempts to configure a wheel into a winning state before the max number of spins is depleted. 

After each spin, a set amount of coins will be revealed to the player in order to manipulate into a winning state.

#### State of coin:

    Heads state -> "H"
    Tails state -> "T" 
    Hidden state -> "-"
    Request coin state -> "?"

#### STEPS:
    (0) Set up of wheel with number of coins, number of reveals, and max number of spins.  

    (1) If the wheel is in a winning state, the player wins and the game is over.
        If the number of turns per game is exceeded, the player loses and the game is over.
    
    (2) The player chooses which coins they wish to reveal in this turn and the state of each chosen
        coin is revealed to the player.

    (3) The player may choose to modify any states of the revealed coins. 

    (4) Coins are then hidden, and the wheel is spun at random amount.

    (5) Repeat 1-4 until reach winning state or number of spins is depleted. 


## Strategic Player Implementation
------------------------------------------

### Algorithm of Four Coin Two Reveal Strategy:
 
Algorithm for a guaranteed win state in five moves or less with four coins and two reveals.

#### STEPS: 

     Spin 1: Open and reveal two diagonal coins and flip to the same face. 

     Spin 2: Open and reveal two adjacent coins and flip to the same face. 

     Spin 3: Open and reveal two diagonal coins:

             Best Case: If final coin found, flip to the same face in order to win the game.
       
             Worst Case: Otherwise, flip one of the matching coins to make mismatched faces. 
       
             ->This provides a known state of the wheel: matching faces that are set adjacent to one another. 
 
     Spin 4: Open and reveal two adjacent coins:
       
             -If the faces match flip both coins to win.
             -If faces do not match then flip both coins: H->T and T->H 
 
     Spin 5: Open and reveal two diagonal coins and flip both coins to win.  

### Delivery Organization:
 
 #### TOP LEVEL:  
   * Overview and Instructions (README.md)
   * Directory of support tools for development and testing (lib/)
   * Java source code (src/)
   * JUnit source code (test/)
   * Build for updated Ant environment (build.xml)

        
 #### lib/
* Files that support JUnit, JaCoCo, Checkstyle, Java2HTML, CPD, PMD, Proguard
* See:
    * https://junit.org
    * https://www.jacoco.org/jacoco/trunk/doc
    * http://checkstyle.sourceforge.net
    * http://www.java2html.com
    * https://pmd.github.io
    * https://sourceforge.net/projects/proguard/

#### Ant Tasks

The default target (all):
* removes artifacts from the previous builds and tests
* compiles src/ and test/
* creates JUnit test reports
* creates maintainer-appropriate API documentation (doc-private)
* generates HTML formatted versions of the source code
* verifies adherence to Java coding conventions
* determines code coverage fo the tests
* flags aread of the source code most likely to contain weaknesses (including complexity metrics)

The set of main targets can be displayed at the command line using:  

`ant -p`

Example: 

    Buildfile: ../build.xml

    Build file for StrategicPlayer project

    Main targets:

    checkstyle          generate checkstyle report
    clean               clean up
    compile             compile the source
    cpd                 proccess source with CPD
    doc-private         generate the maintenance documentation
    format              generate formatted versions of source code
    pmd                 process source with PMD
    report              format junit test results
    test                run junit tests
    testCoverage        run junit tests with JaCoCo instrumentation
    testCoverageReport  format JUnit and JaCoCo test results
Default target: all

See also: https://antapache.org

#### Authors:

- Jon Bowen | jbowen10@msudenver.edu

- Jackie Nugent | jnugent3@msudenver.edu

- Mark Huntington | mhuntin1@msudenver.edu
