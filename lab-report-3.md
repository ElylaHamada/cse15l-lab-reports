# Lab report 3

## Part 1

For this section, I will be exploring the bugs within the array methods that we dealt with from the Week 4 lab. 

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

}
```

The following code block will contain the tests with no input to show the tests succeeding and when we include an input of the array as it is and then trying to reverse it, we will see a failure induced. This will show both an input that does not induce a failure, which is when the arrays are empty and the failure inducing input, which is when we try to input the values into the array and try to assert if they are equal or not. For this example, we input `{1, 2, 3}` into the array and expect it to become `{3, 2, 1}` . 
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = {};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{}, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = {};
    assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
  }
}
```
```
JUnit version 4.13.2
..
Time: 0.016

OK (2 tests)
```
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = {1, 2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{3, 2, 1}, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = {1, 2, 3};
    assertArrayEquals(new int[]{3, 2, 1 }, ArrayExamples.reversed(input1));
  }
}

```

```
JUnit version 4.13.2
.E.E
Time: 0.013
There were 2 failures:
1) testReverseInPlace(ArrayTests)
arrays first differed at element [2]; expected:<1> but was:<3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace(ArrayTests.java:9)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more
2) testReversed(ArrayTests)
arrays first differed at element [0]; expected:<3> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversed(ArrayTests.java:15)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<3> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more

FAILURES!!!
Tests run: 2,  Failures: 2
```

As we can see, after running and compiling these tests, they both failed and the expected value was not the same as the actual value. To resolve this, we can fix the methods in the other file called ArrayExamples.java to then be able to run the tests. I had fixed the methods in the ArrayExamples.java to look like this:

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }

}

```
The following will be a screenshot which will show the symptom, in which when we include an input in one of the tests, one will pass and one will fail. 
<img width="809" alt="Screenshot 2024-05-08 at 21 09 33" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/f0dc5018-ea4f-4087-8e9e-8fc3d1a9a0dd">

As shown in the image, only one tests failed after 2 tests ran, therefore we can see that when we add an input into the method, it does not reverse as it should. The bug in this method is that first of all, both methods are assigning values incorrectly. The `arr[i] = newArray[arr.length - i - 1]` is wrong as it is supposed to be assigned as `newArray[i] = arr[arr.length - i - 1]`. Additionally, since it was assigned wrong, the **reversed** method also returns the wrong variable as it should return `newArray` and not `arr`. Additionally, for the **reverseInPlace** method, we fixed how there was no assignment to the `arr[i]` and we called it temp so we added `int temp = arr[i]` into the method in the beginning. With this new assignment, it helps us swap the inputs in the array. once we swap every input in the array we can reassign it to the variable `temp`. We also divided the arr.length by 2 for the for loop to find the midpoint of the array.

## Part 2

We will be focusing on the `find` command, and find 4 interesting command-line options or alternative ways to use the single command `find`. 
I did use the source: https://www.redhat.com/sysadmin/linux-find-command for some of the examples:

**Finding Files by the type (`-type` option)**
Example:
```find ./technical -type d```

Output:
```
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/biomed
./technical/911report
```
Using the `-type d` option, we can use this to search for directories inside `technical`. Just `-type` option can help search for files or directories based on the type we search for. 

Example 2: 
```find ./technical -type f```

Output:
```
./technical/plos/pmed.0020005.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/pmed.0020039.txt
./technical/plos/pmed.0010071.txt
./technical/plos/journal.pbio.0030127.txt
./technical/plos/pmed.0010058.txt
./technical/plos/pmed.0010070.txt
./technical/plos/pmed.0010064.txt
./technical/plos/pmed.0020158.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020297.txt
./technical/plos/pmed.0020206.txt
./technical/plos/pmed.0020212.txt
./technical/plos/pmed.0020216.txt
./technical/plos/journal.pbio.0030094.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/pmed.0020028.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/pmed.0020148.txt
./technical/plos/pmed.0020160.txt
./technical/plos/pmed.0010048.txt
./technical/plos/pmed.0010060.txt
./technical/plos/journal.pbio.0030137.txt
./technical/plos/journal.pbio.0030136.txt
./technical/plos/pmed.0010061.txt
./technical/plos/pmed.0010049.txt
./technical/plos/pmed.0020161.txt
./technical/plos/journal.pbio.0020127.txt
./technical/plos/pmed.0020149.txt
./technical/plos/journal.pbio.0020133.txt
...
```

the `type f` allows us to see all the files inside `./technical` and this is useful for when we want to look at files without the directory. It helps us filter out what we are looking for more efficiently.

**Searching Newer than the Specified Date (`-newermt` option)**
the `newermt` option allows for searching of files or directories taht are newer than the specified date or time. 

Example:
 ``` find ./technical -type d -newermt '2023-01-01 00:00:00' ```

 Output:
 ```
elylasfolder@Elylas-MBP docsearch % find ./technical -type d -newermt '2023-01-01 00:00:00'
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/biomed
./technical/911report
```
In this first example, we are using teh `-newermt` to find directories that are newer than 01/01/2023

Example 2:
```
find ./technical -type f -newermt '2024-05-08 00:00:00'
```

Output:
```
nothing was shown
```

In this second example, we are using the `-newermt` to find anything new that was created after today, being 05/08/2023, in which there was nothing printed since there was nothing new created after today.

This option is useful when we want to look at files that are modified or directories in certain periods of time after a certain date. It can also help us track our work. 


**Find Empty (`-empty` option)**
We use the -empty command to see if there are any empty directories or files. 

Example:
```
find ./technical -type d -empty
```
Output
```
Nothing shown on the terminal
```
This first example shows us that after we use the `-empty` command to find if there are any empty directories, the output is empty as there are no empty directories.

Example 2:
```
find ./technical -type f  -empty
```
Output: 
```
Nothing was shown on the terminal
```

We also tried the same thing with files and there were no empty files to be discovered.

This option is helpful when we need to find empty files or directories, especially if we want to clean up and delete these empty files/directories or see if we are missing some data. By combining it with `-type f -empty`, we will find all empty files under `./technical` path. This one can be useful to detect if there is any empty file under `./technical` path.


**Case-Insensitive Name Searching (`-iname` option)**
The `-iname` option is similar to the `-name` option but it is case-insensitive therefore it allows us to search for files and directories based on their name using case-insensitive shell pattern matching

Example: 
```
find ./technical -iname 'plos'
```

Output:
```
./technical/plos
```
We tried finding files with the 'plos' name and it showed us the singular path with 'pllos'

Example 2:
```
find ./technical -iname '*.TXT'
```

Output:
```
./technical/plos/pmed.0020005.txt
./technical/plos/journal.pbio.0020043.txt
./technical/plos/pmed.0020039.txt
./technical/plos/pmed.0010071.txt
./technical/plos/journal.pbio.0030127.txt
./technical/plos/pmed.0010058.txt
./technical/plos/pmed.0010070.txt
./technical/plos/pmed.0010064.txt
./technical/plos/pmed.0020158.txt
./technical/plos/journal.pbio.0020042.txt
./technical/plos/journal.pbio.0020297.txt
./technical/plos/pmed.0020206.txt
./technical/plos/pmed.0020212.txt
./technical/plos/pmed.0020216.txt
./technical/plos/journal.pbio.0030094.txt
./technical/plos/journal.pbio.0020046.txt
./technical/plos/pmed.0020028.txt
./technical/plos/journal.pbio.0020052.txt
./technical/plos/pmed.0020148.txt
./technical/plos/pmed.0020160.txt
./technical/plos/pmed.0010048.txt
./technical/plos/pmed.0010060.txt
./technical/plos/journal.pbio.0030137.txt
./technical/plos/journal.pbio.0030136.txt
./technical/plos/pmed.0010061.txt
./technical/plos/pmed.0010049.txt
./technical/plos/pmed.0020161.txt
...
```
This can be more useful than -name if we do not care about cases of our searches as it is more effective. Unlike -name, this can be especially helpful when sometimes we are inconsistent about case choices, which can prevent us from missing some files



