# Lab Report 5
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 12/03/2023

Back to [index](https://miranda-y-zhou.github.io/cse15l-lab-reports/)

---

## Putting it All Together (Week 9)

The objective of this lab is to simulate a debugging process for a Java program and bash script, followed by reflections on the learnings from the second half of this quarter.

* [Debugging Scenario](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report5.html#debugging-scenario)
* [Learning Reflection](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report5.html#learning-reflection)

---

### Debugging Scenario

#### Original File

**Directory and File Structure**

The directory and file structure is designed to facilitate the testing and grading of student submitted Java program:

* `list-examples-grader`
  * `lib`
    * `hamcrest-core-1.3.jar`
    * `junit-4.13.2.jar`
  * `grade.sh`
  * `GradeServer.java`
  * `Server.java`
  * `TestListExamples.java`

The main components are as follows:

`ListExamples.java`: This is the primary Java file containing the program logic. It defines a class ListExamples with methods filter and merge. The filter method filters a list of strings based on a given condition, and the merge method merges two sorted lists into a single sorted list.

`TestListExample.java`: This file contains JUnit tests for the ListExamples class. It includes a custom implementation of the StringChecker interface, IsMoon, and a test method testMergeRightEnd to verify the correctness of the merge method in ListExamples.

`grade.sh`: This bash script is used for automating the grading process. It performs various tasks such as cloning the student's submission from a repository, verifying the presence of the required Java files, compiling the Java files, running JUnit tests, and calculating the score based on test outcomes.

It is noted that two more directories, `student-submission` and `grading-area` would be created under `list-examples-grader` by the `grade.sh` once it is ran. 

**Java File**

`ListExamples.java` has the contents below:

```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}

```

`TestListExample.java` has the contents below:

```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
}

```

**Bash Script**

`grade.sh` has the contents below:

```
CPATH='.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar'

# clean up any previous student submissions and grading areas
rm -rf student-submission
rm -rf grading-area

# Create a new grading area
mkdir grading-area

# Git clone the student repository 
git clone $1 student-submission
echo 'Finished cloning'

# Define variables for file path
DIR_NAME="student-submission"
FILE_NAME="ListExamples.java"
FILE_PATH="student-submission/ListExamples.java"

# Check if the expected file exists
if [ ! -f "student-submission/ListExamples.java" ]; then
    # Provide feedback and exit if the file does not exist
    echo "Error: Expected file '$FILE_NAME' not found in the submission."
    exit 1
fi

echo "Student code has the correct file submitted."

# Copy relevent files for grading into grading-area
cp "student-submission/ListExamples.java" "grading-area"
cp "TestListExamples.java" "grading-area"
cp "GradeServer.java" "grading-area"
cp "Server.java" "grading-area"

echo "All java files are copied into the grading-area directory"

# Change working directory into grading area
cd grading-area

# Complie all the java files
javac -cp $CPATH *.java &> "javac_output.txt"

# Check the exit status of the last command (javac)
if [ $? -ne 0 ]; then
    echo "Compilation failed:"
    grep "error" javac_output.txt
    exit 1
else
    echo "Compilation successful."
fi

# Run JUnit Tests
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples &> "junit_output.txt"

tests_run=$(grep -o 'run: [0-9]*' junit_output.txt | grep -o '[0-9]*')
failures=$(grep -o 'Failures: [0-9]*' junit_output.txt | grep -o '[0-9]*')
correct=$((tests_run-failures))

# Calculate grade
echo "Score:" $((correct/tests_run))"%"

# Back to original directory
cd ..

```

**Output**

#### Student's EdStem Post

#### TA's EdStem Posts

#### Trying Out TA's Suggestions



&nbsp;

---

### Learning Reflection



&nbsp;
