# Grader System 

The Autograder is split up into three parts. 
1. The Manager 
2. The Inspector
3. The Adapter
 
Every one of these parts serves a different purpose and is important in its own way.

Let's Take a look at all the different Pieces that make up the Grader:

## 1. The Manager 
This is the System that manages the whole grading Process.
Also it is the single point of In / Output. So basically, this is the (only) part of the Software we really have to interact with when grading.  
The Manager ensures, that all Tests are run, all Grades are accounted for, and that all of this happens anonymized and simultaniously.

In a nutshell, the Grader's Tasks can be split into these parts:
- Taking in all the Submissions from Moodle 
- Anonymizing the Tasks and extracting the relevant Parts 
- Launching all grading Runners and distributing all the Tasks
- Collecting all Points from the Runners 
- Generating final Grading Tables etc.

## 2. The Inspector 
The Inspector is the part of the Software that does the actual Grading. 
Here all of the Tests are ran and points assigned.  
It is provided with a singular Submission and a grading table that determines how Points are assigned.  
To make this Inspector as modular as possible it Runs an Adapter to a Language-Specific 
Testing Suite. Something like JUnit for Java.

So a overview of the Inspectors Tasks are:
- Run The Adapter that actually runs the Tests 
- Take all the test-results and determine how many points can be awarded 
- Send the results back to the Manager 

## 3. Adapter 
This is the last (relevant) Piece of the Autograder. This just runs all the supplied tests against the (cleaned up) submissions and converts the output of the respective Test-Suites output into the specified format!

So in all, the adapter has to do this:
- Run the Tests supplied for the given Exercise 
- Translate the Test-Suites output into the Standardized [GXChange](adapter/gxchange.md) Format, so the Grader can easily work woth it.