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
./technical/plos/pmed.0020015.txt
./technical/plos/journal.pbio.0020053.txt
./technical/plos/journal.pbio.0020047.txt
./technical/plos/pmed.0020203.txt
./technical/plos/journal.pbio.0030056.txt
./technical/plos/pmed.0020201.txt
./technical/plos/journal.pbio.0030097.txt
./technical/plos/pmed.0020017.txt
./technical/plos/journal.pbio.0020125.txt
./technical/plos/journal.pbio.0020440.txt
./technical/plos/pmed.0010062.txt
./technical/plos/pmed.0020189.txt
./technical/plos/pmed.0020162.txt
./technical/plos/pmed.0020016.txt
./technical/plos/pmed.0020002.txt
./technical/plos/pmed.0020200.txt
./technical/plos/pmed.0020231.txt
./technical/plos/journal.pbio.0020263.txt
./technical/plos/pmed.0020027.txt
./technical/plos/pmed.0020033.txt
./technical/plos/journal.pbio.0020101.txt
./technical/plos/pmed.0010047.txt
./technical/plos/journal.pbio.0030105.txt
./technical/plos/journal.pbio.0020302.txt
./technical/plos/pmed.0010046.txt
./technical/plos/pmed.0010052.txt
./technical/plos/pmed.0020191.txt
./technical/plos/journal.pbio.0020100.txt
./technical/plos/pmed.0020146.txt
./technical/plos/journal.pbio.0020262.txt
./technical/plos/journal.pbio.0030065.txt
./technical/plos/journal.pbio.0020276.txt
./technical/plos/pmed.0020232.txt
./technical/plos/pmed.0020226.txt
./technical/plos/pmed.0020024.txt
./technical/plos/pmed.0020018.txt
./technical/plos/pmed.0020144.txt
./technical/plos/pmed.0020150.txt
./technical/plos/journal.pbio.0020116.txt
./technical/plos/pmed.0020187.txt
./technical/plos/pmed.0010050.txt
./technical/plos/pmed.0010051.txt
./technical/plos/pmed.0020192.txt
./technical/plos/pmed.0010045.txt
./technical/plos/pmed.0020145.txt
./technical/plos/pmed.0020019.txt
./technical/plos/journal.pbio.0020063.txt
./technical/plos/journal.pbio.0030076.txt
./technical/plos/journal.pbio.0030062.txt
./technical/plos/pmed.0020237.txt
./technical/plos/journal.pbio.0020067.txt
./technical/plos/pmed.0020009.txt
./technical/plos/journal.pbio.0020073.txt
./technical/plos/pmed.0020035.txt
./technical/plos/pmed.0020021.txt
./technical/plos/journal.pbio.0020113.txt
./technical/plos/pmed.0020155.txt
./technical/plos/pmed.0010069.txt
./technical/plos/pmed.0010041.txt
./technical/plos/pmed.0020182.txt
./technical/plos/pmed.0020196.txt
./technical/plos/journal.pbio.0020311.txt
./technical/plos/journal.pbio.0030102.txt
./technical/plos/journal.pbio.0020310.txt
./technical/plos/pmed.0020197.txt
./technical/plos/pmed.0010068.txt
./technical/plos/pmed.0020140.txt
./technical/plos/journal.pbio.0020112.txt
./technical/plos/pmed.0020020.txt
./technical/plos/pmed.0020034.txt
./technical/plos/pmed.0020236.txt
./technical/plos/journal.pbio.0020272.txt
./technical/plos/pmed.0020208.txt
./technical/plos/journal.pbio.0020064.txt
./technical/plos/pmed.0020022.txt
./technical/plos/pmed.0020036.txt
./technical/plos/pmed.0010056.txt
./technical/plos/pmed.0020195.txt
./technical/plos/pmed.0010042.txt
./technical/plos/pmed.0020181.txt
./technical/plos/journal.pbio.0020306.txt
./technical/plos/journal.pbio.0030129.txt
./technical/plos/journal.pbio.0020307.txt
./technical/plos/pmed.0020180.txt
./technical/plos/pmed.0020194.txt
./technical/plos/pmed.0020157.txt
./technical/plos/journal.pbio.0020105.txt
./technical/plos/pmed.0020023.txt
./technical/plos/journal.pbio.0020071.txt
./technical/plos/pmed.0020235.txt
./technical/plos/journal.pbio.0020267.txt
./technical/plos/pmed.0020209.txt
./technical/plos/pmed.0020246.txt
./technical/plos/journal.pbio.0020228.txt
./technical/plos/journal.pbio.0020214.txt
./technical/plos/pmed.0020050.txt
./technical/plos/pmed.0020118.txt
./technical/plos/pmed.0010030.txt
./technical/plos/pmed.0010024.txt
./technical/plos/journal.pbio.0020348.txt
./technical/plos/journal.pbio.0020406.txt
./technical/plos/pmed.0010025.txt
./technical/plos/pmed.0020086.txt
./technical/plos/pmed.0020045.txt
./technical/plos/journal.pbio.0020215.txt
./technical/plos/pmed.0020247.txt
./technical/plos/pmed.0020047.txt
./technical/plos/journal.pbio.0020001.txt
./technical/plos/pmed.0020090.txt
./technical/plos/journal.pbio.0020161.txt
./technical/plos/journal.pbio.0020439.txt
./technical/plos/journal.pbio.0020404.txt
./technical/plos/pmed.0010026.txt
./technical/plos/journal.pbio.0020148.txt
./technical/plos/pmed.0020085.txt
./technical/plos/pmed.0020091.txt
./technical/plos/journal.pbio.0020028.txt
./technical/plos/journal.pbio.0020216.txt
./technical/plos/pmed.0020278.txt
./technical/plos/pmed.0020268.txt
./technical/plos/journal.pbio.0020206.txt
./technical/plos/journal.pbio.0020010.txt
./technical/plos/journal.pbio.0020164.txt
./technical/plos/pmed.0010022.txt
./technical/plos/pmed.0010036.txt
./technical/plos/journal.pbio.0020400.txt
./technical/plos/journal.pbio.0020401.txt
./technical/plos/pmed.0010023.txt
./technical/plos/pmed.0020123.txt
./technical/plos/pmed.0020094.txt
./technical/plos/journal.pbio.0020213.txt
./technical/plos/pmed.0020257.txt
./technical/plos/journal.pbio.0020013.txt
./technical/plos/pmed.0020055.txt
./technical/plos/pmed.0020082.txt
./technical/plos/pmed.0010021.txt
./technical/plos/pmed.0010034.txt
./technical/plos/pmed.0010008.txt
./technical/plos/pmed.0020120.txt
./technical/plos/journal.pbio.0020172.txt
./technical/plos/pmed.0020040.txt
./technical/plos/pmed.0020068.txt
./technical/plos/journal.pbio.0020012.txt
./technical/plos/pmed.0020281.txt
./technical/plos/pmed.0020242.txt
./technical/biomed/1472-6807-2-2.txt
./technical/biomed/1471-2350-4-3.txt
./technical/biomed/1471-2156-2-3.txt
./technical/biomed/1471-2156-3-11.txt
./technical/biomed/1471-2121-3-10.txt
./technical/biomed/1471-2172-3-4.txt
./technical/biomed/gb-2002-4-1-r2.txt
./technical/biomed/gb-2003-4-6-r41.txt
./technical/biomed/1471-2466-1-1.txt
./technical/biomed/1471-2199-2-10.txt
./technical/biomed/1471-2202-2-9.txt
./technical/biomed/cc991.txt
./technical/biomed/1471-2369-3-9.txt
./technical/biomed/bcr620.txt
./technical/biomed/1476-069X-2-4.txt
./technical/biomed/1472-6750-3-11.txt
./technical/biomed/1471-2164-2-9.txt
./technical/biomed/1471-2091-2-10.txt
./technical/biomed/gb-2001-2-4-research0010.txt
./technical/biomed/gb-2003-4-4-r24.txt
./technical/biomed/1471-213X-2-1.txt
./technical/biomed/1472-6882-3-3.txt
./technical/biomed/1471-2407-2-3.txt
./technical/biomed/ar331.txt
./technical/biomed/ar319.txt
./technical/biomed/1471-2156-4-5.txt
./technical/biomed/1471-2431-2-1.txt
./technical/biomed/1476-4598-2-22.txt
./technical/biomed/1471-2180-2-22.txt
./technical/biomed/1471-2334-3-9.txt
./technical/biomed/1471-2091-2-11.txt
./technical/biomed/gb-2001-2-4-research0011.txt
./technical/biomed/1471-2202-4-12.txt
./technical/biomed/rr73.txt
./technical/biomed/1471-2164-2-8.txt
./technical/biomed/1471-2148-2-12.txt
./technical/biomed/bcr635.txt
./technical/biomed/1468-6708-3-10.txt
./technical/biomed/gb-2003-4-5-r34.txt
./technical/biomed/1471-2202-2-8.txt
./technical/biomed/1471-2121-3-11.txt
./technical/biomed/1471-2156-3-10.txt
./technical/biomed/1471-2458-3-20.txt
./technical/biomed/1471-2350-4-2.txt
./technical/biomed/1472-6807-2-3.txt
./technical/biomed/1472-6807-2-1.txt
./technical/biomed/1476-4598-1-8.txt
./technical/biomed/1477-7525-1-9.txt
./technical/biomed/ar79.txt
./technical/biomed/1476-0711-2-7.txt
./technical/biomed/1472-6947-3-8.txt
./technical/biomed/1471-2121-3-13.txt
./technical/biomed/gb-2002-4-1-r1.txt
./technical/biomed/1471-2407-3-18.txt
./technical/biomed/1471-2229-2-3.txt
./technical/biomed/1471-2334-1-9.txt
./technical/biomed/gb-2002-3-9-research0043.txt
./technical/biomed/1471-2415-3-5.txt
./technical/biomed/1471-2334-1-21.txt
./technical/biomed/gb-2001-2-7-research0025.txt
./technical/biomed/ar130.txt
./technical/biomed/1476-069X-2-7.txt
./technical/biomed/1472-6890-2-5.txt
./technical/biomed/ar118.txt
./technical/biomed/gb-2002-3-7-research0032.txt
./technical/biomed/1471-2253-2-5.txt
./technical/biomed/1471-2210-1-10.txt
./technical/biomed/1471-2091-2-13.txt
./technical/biomed/1471-2180-2-20.txt
./technical/biomed/1471-2202-3-19.txt
./technical/biomed/1471-2202-4-10.txt
./technical/biomed/1472-6963-2-10.txt
./technical/biomed/1476-4598-2-20.txt
./technical/biomed/1471-2156-4-6.txt
./technical/biomed/1471-2458-3-5.txt
./technical/biomed/1472-6769-1-4.txt
./technical/biomed/gb-2003-4-4-r26.txt
./technical/biomed/1472-6882-3-1.txt
./technical/biomed/cc4.txt
./technical/biomed/1471-2180-2-35.txt
./technical/biomed/1471-2202-4-11.txt
./technical/biomed/gb-2001-2-4-research0012.txt
./technical/biomed/1471-2091-2-12.txt
./technical/biomed/1471-2253-2-4.txt
./technical/biomed/gb-2001-2-7-research0024.txt
./technical/biomed/1471-2415-3-4.txt
./technical/biomed/1471-2199-2-12.txt
./technical/biomed/1471-2121-3-12.txt
./technical/biomed/1471-2148-1-8.txt
./technical/biomed/gb-2001-2-3-research0008.txt
./technical/biomed/1471-2156-2-1.txt
./technical/biomed/1471-2466-3-1.txt
./technical/biomed/bcr568.txt
./technical/biomed/gb-2003-4-7-r46.txt
./technical/biomed/1475-2875-2-14.txt
./technical/biomed/1471-2288-2-4.txt
./technical/biomed/1472-6785-1-3.txt
./technical/biomed/ar93.txt
./technical/biomed/1472-6831-2-2.txt
./technical/biomed/bcr583.txt
./technical/biomed/cc367.txt
./technical/biomed/1477-7827-1-17.txt
./technical/biomed/1477-7827-1-13.txt
./technical/biomed/1472-6807-2-4.txt
./technical/biomed/1471-2156-3-17.txt
./technical/biomed/1475-2875-2-10.txt
./technical/biomed/gb-2003-4-7-r42.txt
./technical/biomed/1471-2156-2-5.txt
./technical/biomed/ar68.txt
./technical/biomed/1471-2172-3-2.txt
./technical/biomed/1471-2121-3-16.txt
./technical/biomed/1472-6750-1-12.txt
./technical/biomed/1472-6904-2-7.txt
./technical/biomed/1472-6882-1-7.txt
./technical/biomed/1471-2334-1-24.txt
./technical/biomed/1471-2377-2-4.txt
./technical/biomed/gb-2002-3-9-research0046.txt
./technical/biomed/rr74.txt
./technical/biomed/gb-2002-3-7-research0037.txt
./technical/biomed/gb-2001-2-8-research0027.txt
./technical/biomed/1476-069X-2-2.txt
./technical/biomed/1471-2148-2-15.txt
./technical/biomed/1472-6874-2-1.txt
./technical/biomed/1471-2210-1-8.txt
./technical/biomed/1471-2091-3-8.txt
./technical/biomed/1472-6793-2-8.txt
./technical/biomed/1471-213X-2-7.txt
./technical/biomed/1471-2202-3-20.txt
./technical/biomed/1471-2091-2-16.txt
./technical/biomed/1476-4598-2-25.txt
./technical/biomed/1471-230X-2-21.txt
./technical/biomed/1476-4598-2-24.txt
./technical/biomed/1471-2350-2-2.txt
./technical/biomed/gb-2001-2-11-research0046.txt
./technical/biomed/1472-6769-1-1.txt
./technical/biomed/ar120.txt
./technical/biomed/1471-2148-2-14.txt
./technical/biomed/1471-2407-1-19.txt
./technical/biomed/gb-2001-2-8-research0032.txt
./technical/biomed/gb-2002-3-7-research0036.txt
./technical/biomed/1471-2415-3-1.txt
./technical/biomed/gb-2003-4-5-r32.txt
./technical/biomed/1472-6750-1-13.txt
./technical/biomed/1472-6920-1-3.txt
./technical/biomed/1471-2474-2-1.txt
./technical/biomed/1476-0711-2-3.txt
./technical/biomed/rr171.txt
./technical/biomed/1471-2156-3-16.txt
./technical/biomed/gb-2003-4-7-r43.txt
./technical/biomed/1472-6807-2-5.txt
./technical/biomed/1471-2350-4-4.txt
./technical/biomed/1471-2172-1-1.txt
./technical/biomed/ar297.txt
./technical/biomed/1471-2350-4-6.txt
./technical/biomed/rr167.txt
./technical/biomed/1471-2474-2-3.txt
./technical/biomed/1471-2121-3-15.txt
./technical/biomed/1471-2172-3-1.txt
./technical/biomed/1472-6904-2-4.txt
./technical/biomed/1472-6750-1-11.txt
./technical/biomed/gb-2003-4-5-r30.txt
./technical/biomed/gb-2002-3-9-research0051.txt
./technical/biomed/1471-2415-3-3.txt
./technical/biomed/gb-2002-3-9-research0045.txt
./technical/biomed/gb-2001-2-8-research0030.txt
./technical/biomed/bcr631.txt
./technical/biomed/1472-6769-1-3.txt
./technical/biomed/cc3.txt
./technical/biomed/1471-2180-2-32.txt
./technical/biomed/1471-2202-4-16.txt
./technical/biomed/1471-2180-2-26.txt
./technical/biomed/1471-2431-2-4.txt
./technical/biomed/1471-2458-3-2.txt
./technical/biomed/1475-9276-1-3.txt
./technical/biomed/ar321.txt
./technical/biomed/1471-230X-2-23.txt
./technical/biomed/ar309.txt
./technical/biomed/gb-2001-2-4-research0014.txt
./technical/biomed/1477-7819-1-10.txt
./technical/biomed/gb-2001-2-11-research0045.txt
./technical/biomed/1471-2202-4-17.txt
./technical/biomed/1472-6769-1-2.txt
./technical/biomed/bcr618.txt
./technical/biomed/gb-2002-3-7-research0035.txt
./technical/biomed/gb-2001-2-8-research0031.txt
./technical/biomed/1471-2148-2-17.txt
./technical/biomed/1471-2229-2-4.txt
./technical/biomed/1471-2350-3-12.txt
./technical/biomed/gb-2002-3-9-research0044.txt
./technical/biomed/1471-2377-2-6.txt
./technical/biomed/1471-2474-4-4.txt
./technical/biomed/1472-6904-2-5.txt
./technical/biomed/1472-6823-3-1.txt
./technical/biomed/1471-2474-2-2.txt
./technical/biomed/rr166.txt
./technical/biomed/rr172.txt
./technical/biomed/1471-2156-2-7.txt
./technical/biomed/1472-6785-1-5.txt
./technical/biomed/bcr284.txt
./technical/biomed/gb-2002-3-2-research0008.txt
./technical/biomed/gb-2002-3-11-research0059.txt
./technical/biomed/cc2190.txt
./technical/biomed/gb-2002-3-11-research0065.txt
./technical/biomed/1471-213X-3-2.txt
./technical/biomed/1471-2148-3-18.txt
./technical/biomed/1471-2229-3-3.txt
./technical/biomed/1471-2172-4-1.txt
./technical/biomed/ar795.txt
./technical/biomed/1471-2164-3-15.txt
./technical/biomed/cc1843.txt
./technical/biomed/1471-2164-3-29.txt
./technical/biomed/1471-2458-2-16.txt
./technical/biomed/1475-925X-2-10.txt
./technical/biomed/1472-6807-3-1.txt
./technical/biomed/gb-2003-4-9-r58.txt
./technical/biomed/1471-2105-4-27.txt
./technical/biomed/1471-2105-3-12.txt
./technical/biomed/gb-2003-4-2-r16.txt
./technical/biomed/ar408.txt
./technical/biomed/ar409.txt
./technical/biomed/1471-2407-2-11.txt
./technical/biomed/gb-2001-2-10-research0041.txt
./technical/biomed/1471-2288-3-4.txt
./technical/biomed/1471-2105-4-26.txt
./technical/biomed/1471-230X-1-5.txt
./technical/biomed/gb-2002-3-8-research0040.txt
./technical/biomed/1475-925X-2-11.txt
./technical/biomed/gb-2001-2-9-research0035.txt
./technical/biomed/1471-2172-3-12.txt
./technical/biomed/gb-2003-4-6-r37.txt
./technical/biomed/1472-6750-1-8.txt
./technical/biomed/1471-244X-2-9.txt
./technical/biomed/gb-2002-3-12-research0085.txt
./technical/biomed/1471-213X-1-1.txt
./technical/biomed/1471-2164-4-21.txt
./technical/biomed/cc1856.txt
./technical/biomed/1471-2180-3-15.txt
./technical/biomed/1471-2164-3-28.txt
./technical/biomed/cc105.txt
./technical/biomed/1471-2202-2-10.txt
./technical/biomed/1471-2180-1-8.txt
./technical/biomed/1471-2431-3-3.txt
./technical/biomed/1471-2369-3-10.txt
./technical/biomed/1471-213X-3-3.txt
./technical/biomed/cc1498.txt
./technical/biomed/1471-2377-1-2.txt
./technical/biomed/1471-2350-3-7.txt
./technical/biomed/gb-2002-3-2-research0009.txt
./technical/biomed/bcr285.txt
./technical/biomed/gb-2002-3-6-software0001.txt
./technical/biomed/1475-2867-3-12.txt
./technical/biomed/1471-2229-1-2.txt
./technical/biomed/1471-2407-3-3.txt
./technical/biomed/1472-6890-1-4.txt
./technical/biomed/1471-2172-4-2.txt
./technical/biomed/1471-2164-3-16.txt
./technical/biomed/1471-2091-3-18.txt
./technical/biomed/1471-2202-2-12.txt
./technical/biomed/1471-2164-4-23.txt
./technical/biomed/1471-213X-1-3.txt
./technical/biomed/gb-2002-3-12-research0087.txt
./technical/biomed/1471-2091-3-30.txt
./technical/biomed/gb-2002-3-12-research0078.txt
./technical/biomed/1471-2164-3-9.txt
./technical/biomed/1471-2172-3-10.txt
./technical/biomed/1471-2172-2-4.txt
./technical/biomed/1471-2180-1-12.txt
...
```

the `type f` allows us to see all the files inside `./technical` and this is useful for when we want to look at files without the directory. 

**Searching Newer than the Specified Date (`-newermt` option)**


