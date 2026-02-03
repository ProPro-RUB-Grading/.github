# Grade eX Change Format

This formmat is used, so the Grader can easily be adapted to differing Programming Languages using an Adapter. 

The grader has a few "special" prerequisites that any adapter has to respect, so that it'll work seemlessly.
1. **All Tests should be Stateless.**  
To Ensure all Tests can be ran fairly they shouldnn't share any state or be dependant on one another in any way. This is the case normally, but should definetely be remembered, when designing tests. All State etc. should be set inside the Test.
2. **All Tests should be ran, regardless of "difficulty"**  
Every Test that can be run, should be run, so that the grader can use its internal Grading and Point-Assignment Table to determine the final point count.
3. **All Output should be in GXChange Format**  
The grader can only really work with the Format described here. If there is any additional Information you would like to communicate it has to either be set in the Grading Configuration or be modified inside the Grader system itself. So ideally, the Adapter is as "stupid" as possible, and only communicates the Test-Results transparently to the Inspector.

## Fields
A complete output file should look like this:

```json 
{
  "totalTests": 4,
  "totalFailures": 2,
  "totalSkipped": 0,
  "totalSystemErrors": 0,
  "totalExecutionTime": 0.024,
  "testResults": [
    {
      "name": "more_complex_test",
      "passed": false,
      "message": "Imagine a Java Error Message"
    },
    {
      "name": "very_simple_test",
      "passed": true,
      "message": ""
    },
    {
      "name": "test_for_extra_point",
      "passed": false,
      "message": "Imagine a Java Error Message"
    },
    {
      "name": "test_with_more_limited_scope",
      "passed": true,
      "message": ""
    }
  ]
}
```

There are a few important fields, that we should take a look at:
### Root File
> **totalTests** (int)   
This Field is used to indicate the total numbers of tests the Adapter has found. This is being double-checked internally, to make sure all applicable tests have been run.

> **totalFailures** (int)  
This Value keeps track of everything that has failed, so we can also double check the results later. 

> **totalSkipped** (int)  
If the Testing Suite has skipped running any tests for any reason this should be set to anything > 0 and < totalTests. This indicates to the grader, that something in this submission went wrong, so that somebody can take a look at this later.

> **totalSystemErrors** (int)  
Compile Errors, File not Found Errors or anything to that degree should be mentioned here, so debugging can be made as easy as possible!

> **totalExecutionTime** (float)  
Value to keep track of time, so anything that took an especially long time to validate can be looked at again. (Checking for infinite loops or something. on the Adapters side)

> **totalResults** (TestResult)  
This is a List with the results of the tests. Each test should get its own section here, so it can later be ordered using the Grading Configuration

### TestResult
> **name** (string)  
This should reflect the Name for the test that is configured in the Grading Configuration. How your Adapter gets this name is essentially up to you, but it should be able to retrieve this out of the Tests ran, so that there is no need for any kind of manual intervention into the Grader 

> **passed** (bool)  
Boolean value that indicates if a test was passed or not, pretty straight forward.

> **message** (string)  
any kind of Error Message etc. that you might wanna reference in the generated Feedback inside the grader. Could be anything from descriptive values down to just a Stack-Trace.