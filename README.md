# CS5044-Project-3-Play-Tetris-solution

Download Here: [CS5044 Project 3 – Play Tetris solution](https://jarviscodinghub.com/assignment/project-3-play-tetris-solution/)

For Custom/Original Work email jarviscodinghub@gmail.com/whatsapp +1(541)423-7793

Tetris
(Links to an external site.)
Links to an external site.
was arguably the most popular single-player computer game of all time by the early 1990’s. It’s incredibly simple and fun to play, and even to this day it’s widely considered to be among the best games of all time.

In case you’ve never seen it, the game consists of a 10-unit wide by 24-unit tall well, into which randomly-selected geometric 4-unit pieces begin to fall one at a time. The player manipulates each piece as it falls, by moving it horizontally within the well, and rotating it in 90° increments. Once the piece can fall no further, it becomes locked in place, taking up space in the well.

However, if the player forms one or more full horizontal (10-unit by 1-unit) rows, those rows are removed, with all rows above shifting downward. The goal is to continue playing as long as possible, so the player must attempt to pack the pieces strategically. Eventually, though, the well fills upward to a limit line, and if any portion of a piece is locked in place above this line, the game is over.

You’ll see all of this in action soon enough, and it’s actually quite easy to understand once you’ve played it for just a few minutes.

Requirements
Building a full-functional Tetris application requires a little more Java than what we’ve covered yet this term, so you’ll be provided a working application that you can download and play. It’s a somewhat simplified version, with a very rudimentary scoring mechanism, but it’s still just as enjoyable and challenging as the original.

So, if the application is already provided, what is this assignment all about? The goal here is to develop a basic Artificial Intelligence (“AI”) system, capable of controlling the game as if it were the player.

Implementing an Interface
In previous assignments, you were given a class file with method declarations, Javadoc comments, and placeholder implementations. In this assignment, you’ll be given an interface instead. An interface contains the method declarations and the Javadoc comments, but no code at all (not even placeholders).

Your task is to implement this interface, which means you’ll develop a class that provides code for all the methods declared in the interface. In addition to the methods specified by the interface, you will likely need to develop several private helper methods in order to fully implement it without redundancies.

System Description
The interface you will implement is called edu.vt.cs5044.tetris.AI and your implementation class must be called edu.vt.cs5044.TetrisAI. You will need to develop the code needed to implement the methods defined by the interface. One of the methods will be the overall AI system.

This method receives some parameters, defining the current state of the game board and the shape to be placed, and will need to find the “best” placement for that shape. The other methods are responsible for intermediate calculations.

These methods would normally be private, and not specified by the interface, but for academic purposes we’re exposing these methods to ease the testing requirements. Speaking of tests, your JUnit test file must be called edu.vt.cs5044.TetrisAITest.

Downloads
tetris5044.jar library file containing all the compiled game engine classes
tetris5044-api.jar library file containing the Javadocs for the game engine

Setting up Eclipse
Download the provided files to your computer, and place them in a convenient folder. Open Eclipse and create a new Java Project for this assignment. Right-click the project and select Build Path | Configure Build Path, then select the Libraries tab. Click Add External JARs and navigate to where you placed the downloaded JAR files, select tetris5044.jar, and click OK. You should now see that file listed just above the JRE System Library.

Now click the little triangle to expand the new file, select Javadoc location: (None), and click the “Edit…” button. Here be sure to select “Javadoc in archive” first, then click Browse. Navigate again, this time selecting tetris5044-api.jar, and click Validate. It should tell you the location is likely valid, so click OK, then OK, then OK to get back to your project. Your should see a new Referenced Libraries section, which you can expand to see the tetris5044.jar file.

Shall We Play a Game? (better than tic-tac-toe)
At this point, you can right-click your project and select Run As | Java Application to play Tetris! Go ahead and try it now…

A window should appear with an empty game board and a prompt to type P to play. Once you type P, you will see a new random piece near the top, slowly falling toward the bottom of the well. There are several alternative keyboard controls you can use, but for now just type J and L to move the piece left and right, and type I to rotate the piece. Once the piece is situated as you wish, you can use K (or the space bar) to drop the piece immediately, or you can just enjoy watching the piece fall gently into place.

Zombie (brains?)
You can type ‘?’ into the game at any time to produce a listing in the Eclipse console of all of the available options and keyboard controls. Try this now. Some of these options will be extremely useful during the assignment. You’ll probably notice some interesting options, including a way to enable the Player AI by typing Ctrl-P.

When you enable this mode, just before a new shape appears in the game, the AI is asked how to best rotate then position the shape. Go ahead and type Ctrl-P now. Nothing will happen, except you’ll see a warning in the console that your implementation couldn’t be found, which is perfectly understandable at this point.

Trying to Take Over the World (no, not that Brain)
Close the game for a moment now, while we get some of the basics for the code in place. First, create a new package in your src folder called edu.vt.cs5044 then right-click within that package select New Class. Before you enter the class name, click the “Add…” button to the right of the Interfaces section. In the search box at the top, type AI and you should soon see the AI interface (in the edu.vt.cs5044.tetris package) selected. Click Ok to add that interface, and now you can enter the class name TetrisAI and click Finish.

Notice that the new file declaration says public class TetrisAI implements AI. This is what tells Java that we intend to be compatible with any system that can work with the AI interface. You’ll also notice Eclipse is already showing an error on the class declaration line. Click the tiny red X in the margin and double-click “Add unimplemented methods” from the pop-up.

This asks Eclipse to generate all the method placeholders for you! Save the file, and check out your implementation. It’s already compatible with the game system, even though all it does is return placeholders. That’s not very useful, of course, but it’s actually enough to get started. Let’s see if it’s recognized by the game engine.

Launch the application again, type Ctrl-P to activate the Player AI, and confirm that the console says the Player AI is now on. If so, go ahead and type P to start the game. Well, that’s not very exciting. The console just keeps saying that the AI selected an invalid move for each shape, and we still have to manually place the pieces.

That’s fair enough, since all we have are placeholders that Eclipse generated for us, but at least we know the game found our AI and seems to be communicating with it. Close the game again now so we can code a little more.

Let’s at least provide a valid suggestion, even if it’s always exactly the same suggestion. In the findBestPlacement() method, let’s replace the placeholder:

return null;
with this:
return new Placement(Rotation.NONE, 0);

Eclipse will complain that it doesn’t know about the Rotation class yet, so again click the tiny X in the margin and double-click to import the Rotation class from the edu.vt.cs5044 package. That should resolve the error, so save your file again. This really doesn’t seem like much of an improvement, but we’ll try it anyway.

Launch the game and use Ctrl-P then P to check it out. Now it’s just placing everything against the left edge (column 0) without any rotation, which is still fairly uninteresting. However, it’s clear that our AI is actually placing the pieces automatically for us! Things can only get better from here. Close the game once you’re ready to code again.

Need More Input (accidental AI, maybe)
Obviously we need to examine the shape and the state of the board in order to make some reasonable decisions. Let’s take a look at all those Javadocs that make up the API. In your source file click within the word AI of “implements AI” and type Shift-F2. This should open the Javadocs for the AI interface using an internal browser within Eclipse. You can set it to use an external browser, if you prefer, but this is fine for now.

Reading the Javadocs, click the findBestPlacement() method and you’ll see it actually provides a brief outline of a strategy. We apparently need to iterate over each possible rotation, and for each rotation we need to iterate over every possible column placement. For each of these, we need ask the Board object to tell us what the result of any hypothetical move would be. Click the method Board.getResultBoard() to see how that works. The Javadocs say that the original board instance is not modified, and we’ll get a new board instance that we can examine.

That will meet our needs, but how do we examine one of these hypothetical results? There are only a few other methods available in the Board class. One provides a human-readable rendering of the board, which might prove very useful to visualize what’s happening while debugging, and another promising method seems to let us query any location within the board to see which locations are occupied by fixed blocks.

There are also some static constants that tell us the overall size of the board, plus two constructors. One of the constructors allows us to generate arbitrary board configurations, which is exactly what we’ll need in order to create some nice test cases. Don’t forget about TDD!

Click the Package link at the very top of any Javadoc page to see the package overview, then navigate throughout the various pages to see what each class and enum can do, along with the requirements for the interface. A fundamental part of this assignment is to learn how to use Javadocs to explore unknown libraries, as well as to see how a somewhat larger scale system is divided into multiple classes, each with its own purpose.

Note that class Tetris5044 is for internal use only; you won’t need it at all. Also, classes RandomMode and ShapeStream are only needed for the optional “challenge” section below.

Strategy Games
There’s no such thing as a perfect Tetris strategy, so we won’t even try. We are necessarily taking the heuristic
(Links to an external site.)
Links to an external site.

approach to this problem, and there will necessarily be trade-offs involved. In every placement decision, there are advantages and disadvantages. How can we hope to find the “best” placement? Now is probably a good time to look at those other methods in the interface.

Costs and Benefits
From the API, it seems the remaining methods of the interface are related to making some measurements to evaluate a board position. The idea here is that we’ll compute four distinct “cost” scores, or factors, which tell our system something about how bad (or good) a particular placement might be. We’ll need to develop those method first, before we can hope to have a working AI system.
We’re still focusing on TDD, so start with some fairly straightforward test cases to ensure the individual scoring methods work. Just construct a test board object, then assert the cost score you expect your implementation to compute.

Once all of your individual cost scoring methods are working properly as expected, its time to put it all together. The findBestPlacement() method will need to iterate through all the possible placements, and for each it will combine these individual cost scores in a weighted sum, then choose the lowest cost to return to the game engine. The weightings are important so that certain factors can have more influence on the overall decision than others. At first you can just set all the weights to 1, by simply summing the individual scores together, even though eventually we’ll need to adjust the weights to achieve better results.

Strategic Default
Luck plays a starring role in Tetris. Even with the best of strategies, it’s critical to recognize that some games simply provide a more fortunate sequence of shapes than others. Thus it can be difficult to objectively judge exactly how good a particular strategy might be. To help with this, our implementation provides a set of 4 repeatable test sequences we can use as a benchmark. The average number of pieces placed from these 4 test sequences will act as a very reasonable metric of how well our strategy is working overall.

Teaching to the Test
Eventually we’ll be making a linear combination of our four scores, which just means we multiply each score by some weight, then add the weighted scores. The equation is very straightforward:
overallCost = weight1*score1 + weight2*score2 + weight3*score3 + weight4*score4

Computing the individual scores really isn’t too bad, but what about the weights? As noted above, we can start by simply setting all the weights to 1, and indeed that strategy will place an average of just above 100 pieces for each of the provided test sequences.

Standards of Learning
Can we do better? Sure! As a start, reasonable weight ranges for the selected factors will be 0 through 15. You can just use trial-and-error if you wish; watch your AI play the test games and try to figure out which factors need more or less emphasis. For example, if your AI is creating too many unnecessary gaps, try to increase the weight of the gap count score. Be sure to use Turbo mode in conjunction with all the Random TEST modes.

Your AI must be able to place at least 175 pieces, on average, across the provided test sequences. Try adjusting your weights in increments of 5, meaning weight values of 0, 5, 10, and 15. Of the 256 possible combinations of 0, 5, 10, and 15 as weights, about 12% will result in this level of performance, so guessing will eventually yield a good combination. You don’t need to provide a JUnit test to demonstrate this performance, but Web-CAT will check whether your system meets this minimum or not.

More than Full Coverage
Unlike in the previous assignment, creating JUnit tests to cover all of your code will be very straightforward, since there aren’t very many branches involved in the solution. You can likely achieve full coverage with just one well-designed test case that asserts something about each method. As a result, complete coverage is not nearly enough to ensure you have correctly implemented your code.

Therefore, you must generate at least 5 test cases for each interface method, with non-trivial tests and non-trivial assertions. You can satisfy this by creating at least 5 distinct test boards to be shared among assertions involving all the test methods. Just be sure the test boards cover a reasonably wide range of board layouts. Note that Web-CAT won’t (and can’t) enforce this requirement, but the human grader will definitely be looking for this.

Functional Decomposition
Judicious use of helper methods can significantly reduce the overall amount of code you need to develop. For example, you might want to create a helper method that returns the height of one specified column. You can then call that method from within a loop of all columns, and use the return value to help compute some of the cost factors your. Your code will be inspected during the human review for redundancies, so be sure to develop helper methods wherever appropriate.

Automating the Automation (An OPTIONAL Challenge)
You might have noticed that it can get somewhat tedious to try every combination of 0, 5, 10, and 15 for each of the weights, even in Turbo mode. You might have also noticed that you’ve been given sufficient tools to run entire simulated games without the user interface at all.

As a challenge, see if you can identify the very best combination of 0, 5, 10, and 15 weights, by writing a separate class file called edu.vt.cs5044.WeightFinder with its own main() method. This file will be completely ignored by Web-CAT, and you don’t need to generate any tests for it at all.

You’ll also need to add a public method, such as setWeights(int w1, int w2, int w3, int w4) to your TetrisAI implementation, to apply the various weight combinations. This method will need to be exercised by a single assert, just to be sure it’s covered within your own JUnit tests. The best weights among these combinations will place an average of over 675 pieces for the test sequences.

Once you’ve found the optimum combination, you’ll need to hard-code those values back into your AI as the defaults, in order to watch them in action. That’s quite an improvement, unless you happened to get very lucky in your trial and error phase!

Confirm that this is all working as expected, and that you’re definitely placing over 675 pieces on average for the test sequences before the next part of the challenge. It should be a simple change to your code to try stepping by 3 instead of 5 (meaning you should test every combination of 0, 3, 6, 9, 12, and 15 for every weight).

This process takes about 5-10 times longer to run than stepping by 5. However, if everything was already working properly, you’ll only need to do this once, and you’ll discover that your newly-tuned weights will average over 2,700 pieces placed for the test sequences. We’ll call that a definite win!

Still not satisfied? You can always try stepping by 1 instead. Again it’s a trivial code change, but note that this process takes about 50-100 times longer to run than stepping by 3, so we’re likely talking about a few hours at this point. However, your newly-optimized AI possess the astonishing capability of averaging over 6,750 pieces placed for the test sequences! It’s actually over ten times the best average you can achieve when iterating by fives.

(By the way, you can stop your iterations when you reach this goal; there’s nothing better to find when stepping by ones.) You might be somewhat surprised when you discover the optimum weightings. When you watch this particular combination in action, it’s interesting to compare the variation in results between TEST3 (the worst) and TEST4 (the best).

If you make any progress with this OPTIONAL challenge, please add a brief write-up in the comments of your WeightFinder class, just to let us know what you did, along with any thoughts you’d like to share about the experience. Of course you may also discuss this in Piazza, although please don’t post your code (or any weightings you find) to the entire class, so as not to spoil the fun for anyone else.
Hopefully you enjoyed this challenge!

Submit to Web-CAT

Submit your solution to Web-CAT via Eclipse or the web interface. Please feel free to improve and resubmit your code as many times as you like (before the deadline) in order to improve your score.

Important Notes:
Your submission will be evaluated both by Web-CAT (40 points) and by human (40 points). As such, Web-CAT’s automated score will show at most 40/80 points.
Your JUnit test class will be evaluated by Web-CAT to ensure complete coverage of you implementation code, but it will NOT be evaluated for style. Web-CAT will also use its own internal test suite (that we’ve developed) to evaluate your system.

Carefully review your feedback. In the summary, you will see a table listing each of your source files with a green/red bar by each non-test file. If the bar for any file is not completely green, then some code in that file was not exercised by your own tests. Click the file name to view your source code and look for lines that are highlighted in a pink color.

Hover your mouse over highlighted lines for additional information. You will need to add at least one test case to exercise the highlighted code. This includes testing the same actions you’ve already tested, but starting from different initial conditions.
See the project grading rubric for full details on the grading criteria applied to this assignment.
