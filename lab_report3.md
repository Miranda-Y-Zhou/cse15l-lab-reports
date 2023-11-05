# Lab Report 3
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 11/05/2023

Back to [index](https://miranda-y-zhou.github.io/cse15l-lab-reports/)

---

## Bugs and Commands (Week 5)

The objective of this lab is to further analyze and document a bug from week 4's lab, illustrating it with JUnit test cases.
This lab also explore the functionalities of the terminal command `grep` by providing examples of its command-line options.


* [Bugs from Week 4's Lab](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report3.html#bugs-from-week-4s-lab)
* [Terminal Command: `grep`](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report3.html#terminal-command-grep)
* [References](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report3.html#references)

---

### Bugs from Week 4's Lab

The original `reversed` method from `ArrayExamples` class is shown below. 
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
This method is designed to take in an integer array and return a **new** array with all the elements of the input array in reversed order.

Initially, attention is given to a test case that is expected to fail, revealing the flaw in the `reversed` method. The JUnit test below has been designed to reverse a non-empty array and, as such, should demonstrate the defect in the method's implementation.

```
@Test
  public void testReversed2() {
    int[] input1 = { 1, 5, 6, 3, 9 };
    assertArrayEquals(new int[]{ 9, 3, 6, 5, 1 }, ArrayExamples.reversed(input1));
  }
```

Failure-inducing input: `{ 1, 5, 6, 3, 9 }`

There's a situation where the method in question works just fine. If the user hand it an empty array, it outputs back an empty array, which is exactly expected output. The following test case confirms this observation.

```
@Test
  public void testReversed() {
    int[] input1 = {};
    assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
  }
```

Input that doesn’t induce a failure: `{}`

Upon execution of the JUnit tests, it is observed that the `testReversed2` fails, its symptom shown in the image below. The `testReversed` test, however, succeeds, which suggests that the method is capable of handling empty arrays without introducing errors.

![image of symptom](Images/Screen Shot symptom.png)

**The Bug in Code**

Here's the original method that contains the bug. It attempts to assign the new integer array list's elements into the old one, which is not the intended behavior. 

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

**The Corrected Method**

After identifying the issue, the method was corrected to ensure that a new array is assigned with the reversed elements of the original array, which remains unchanged:

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[arr.length - i - 1] = arr[i]; 
    }
    return newArray;
  }
```

**Explaining the Fix**

The original code failed because it attempts to assign elements of the new integer array into the input array, which is the opposite assignment of what it is intended. Since the new array is created to be an empty array of the same length as the original, it is just an array with filled with `0`. Thus, this original method simply assigns `0` to all elements of the input array. The corrected code resolves the problem by correctly assigning the elements from the end of the input integer array to the beginning of the new array newArray. The loop now iterates through each index and assigns the corresponding reversed value properly to the new integer array. This fix ensures that the reversed method behaves as intended, returning a new array with elements in reverse order, without modifying the original array.

With these changes, the reversed method now accurately produces a new array with the input array's elements reversed, and the passing of all JUnit test cases confirm this expected behavior.

![image of bug fixed](Images/Screen Shot corrected bug.png)

&nbsp;

---

### Terminal Command: `grep` 

The `grep` command, short for “global regular expression print”, is a powerful command for searching through text and files for lines that match a given string, then printing matching lines. 
This command follows the general syntax: `grep "string" 《file name》`.

Here are four interesting options for `grep` and two examples for each, applied to files and directories from `./technical`.

#### 1. Recursive Search `-r`

The `-r` option tells `grep` to read all files under each directory, recursively. It will search for a string in the current directory and all other subdirectories. Then, the matching lines along with their file paths are printed to the terminal.
This command option is useful because it allows the user to perform a string search across numerous files and nested directories simultaneously, saving time and effort when dealing with large collections of files.

**Example 1:**

```
Mirandas-MBP:docsearch zhoujijun$ pwd
/Users/zhoujijun/Documents/GitHub/docsearch
Mirandas-MBP:docsearch zhoujijun$ grep -r "grape" ./technical/
./technical//plos/journal.pbio.0020224.txt:        Dactylosphera vitifoliae devastated European grapewine varieties
./technical//plos/journal.pbio.0020214.txt:        2004). The grapevine distributes stories of “bad words” that should be avoided when
./technical//biomed/1471-2229-3-3.txt:        grapevine and tomato [ 34 ] . The locus PM50 contains only
./technical//biomed/1472-6750-2-2.txt:        Biological control by F2/5 is grape-specific, as F2/5 is
./technical//biomed/1472-6750-2-2.txt:        not effective on non-grapevine host plants such as 
./technical//biomed/1472-6750-2-2.txt:        grape would be beneficial for disease control in field
./technical//911report/chapter-12.txt:                about the size of a grapefruit or an orange, together with commercially available
```

The above command `grep -r "grape" ./technical/` searches for the string "grape" in all files within the `./technical` directory and all of its subdirectories, including `plos`, `biomed`, `911report`, `government`, and all subdirectories of the subdirectories until there are no more directories. Then, it prints the lines that contained the string "grape" and the file path of that file. 

**Example 2:**

```
Mirandas-MBP:docsearch zhoujijun$ pwd
/Users/zhoujijun/Documents/GitHub/docsearch
Mirandas-MBP:docsearch zhoujijun$ grep -r "biology" ./technical/government/
./technical/government//Gen_Account_Office/pe1019.txt:as chemistry, biology, physics, and computer science."
./technical/government//Gen_Account_Office/pe1019.txt:science to fisheries biology and chemical engineering. Of note is
./technical/government//Media/Law_Award_from_College.txt:in both biology and psychology, she worked as legal secretary for
```

The above command `grep -r "biology" ./technical/government/` searches for the string "biology" in all files within the `./technical/government/` directory and all of its subdirectories, including `About_LSC`, `Alcohol_Problems`, `Env_Prot_Agen`, `Gen_Account_Office`, `Media`, `Post_Rate_Comm` and all subdirectories of the subdirectories until there are no more directories. Then, it prints the lines that contained the string "biology" and the file path of that file. 

&nbsp;

#### 2. Case-Insensitive Search `-i`

The `-i` option allows `grep` to perform case-insensitive searches, so it doesn't differentiate between uppercase and lowercase letters.
This option for grep is useful because it lets the user find matches regardless of letter case, making it easier to search for text when the user is unsure of the exact capitalization or want to include all variations.

**Example 1:**

```
Mirandas-MBP:docsearch zhoujijun$ pwd
/Users/zhoujijun/Documents/GitHub/docsearch
Mirandas-MBP:docsearch zhoujijun$ grep "PHYLOGENIES" ./technical/plos//journal.pbio.0030021.txt
Mirandas-MBP:docsearch zhoujijun$ grep -i "PHYLOGENIES" ./technical/plos//journal.pbio.0030021.txt
        produce two sexes, and current phylogenies (e.g., [1]) suggest that sexual dimorphism was
        important factor in this area are new phylogenies of the genus [17,18], which consistently
```
The above command searches for the word "phylogenies" in the `journal.pbio.0030021.txt` file within the `./technical/plos/` directory, ignoring case differences. As illustrated in the example, when the user tries to search "PHYLOGENIES" using only `grep` with no other command options, there are no output as there are no string matched "PHYLOGENIES" in the file. However, when the command option `-i` is included, it searches for "phylogenies", "PHYLOGENIES", "PHyLOGeNIes", or any combination of letter cases, which in the file above there are two matching "phylogenies".

**Example 2:**

```
Mirandas-MBP:docsearch zhoujijun$ pwd
/Users/zhoujijun/Documents/GitHub/docsearch
Mirandas-MBP:docsearch zhoujijun$ grep "JuRASsiC pArk" ./technical/plos//journal.pbio.0030056.txt
Mirandas-MBP:docsearch zhoujijun$ grep -i "JuRASsiC pArk" ./technical/plos//journal.pbio.0030056.txt
        Jurassic Park was still taking in millions of dollars at the box office,
```

The above command searches for the word "jurassic park" in the `journal.pbio.0030056.txt` file within the `./technical/plos/` directory, ignoring case differences. As illustrated in the example, when the user tries to search "JuRASsiC pArk" using only `grep` with no other command options, there are no output as there are no string matched "JuRASsiC pArk" in the file. However, when the command option `-i` is included, it searches for "jurassic park", "JURASSIC PARK", "JuRASsiC pArk", or any combination of letter cases, which in the file above there is one matching "Jurassic Park".

&nbsp;

#### 3. Line Number `-n`

&nbsp;

#### 4. Count Matches `-c`


&nbsp;

---

### References

&nbsp;
