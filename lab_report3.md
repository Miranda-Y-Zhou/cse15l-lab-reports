# Lab Report 3
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 11/05/2023

Back to [index](https://miranda-y-zhou.github.io/cse15l-lab-reports/)

---

## Bugs and Commands (Week 5)

The objective of this lab is to create a Java web server, `StringServer`, to accumulate and display messages.
This lab also delve into SSH key authentication, showcasing a password-less login to `ieng6`, followed by reflections on the learnings from weeks 2 and 3.

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
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```


&nbsp;

---

### Terminal Command: `grep` 



&nbsp;

---

### References

&nbsp;
