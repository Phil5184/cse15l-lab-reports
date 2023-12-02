## Phillip's Edstem Post:
Hello, I am Phillip Mai and I would like some help with my center pivot partitioner method. It's supposed to partition a String array based on a pivot at the center, so that all the elements less than the pivot are to the left of the pivot, and all elements bigger than the pivot are to the right. Right now my code isn't working when I run the tests. Here is a screenshot of my failure test.

I don't know what the bug is, it seems like the method isn't running to the very end because the last element remains the same. The last element should be "N" but instead it is "H". I think there is something wrong that makes it so that my code isn't reaching the last for-loop.

## TA: Hi! So to me, it seems like your thoughts about the possible bug might be correct, but to make sure, let's add in some print lines at the last for loop to see if it's reaching the loop. I also see that your code is making a copy of the string array and modifying it, then updating the original string array with the modified copy. Just to make sure there isn't any issues with the copy, can you add some print statements to print out the original array and the copy array right at the end before the original array is updated? If none of these ends up leading us to the right answer, we can try out some more debugging techniques. 

## Phillip: 
Thank you! I'll try it out right now. 

## Phillip: 
Here is the results of the running test and the prints after adding in what you told me to add. 

It seems like the copy array and the original array are the same thing, even though the print statement is before the original one was copied over. Does this mean that when I was modifying the copy, it was modifying the original one at the same time too?

## TA: 
Yeah, that's the issue. That was what I was trying to check for, to see if the copy was actually another string array object and not just a shallow copy. Try fixing it to make the copy a deep copy instead, where you create a new string array and manually copy the elements over. 

## Clear Description of Bug:
The bug is that the copied array wasn't actually a copy of the original one. It wasn't a new string array object. The student wrote the code in a way where the copy was just another reference to the original array, so every time the copy was modified, it was just modifying the original one along with it. 

## File and Directory Structure:
My setup didn't require much, I just needed a main home directory, and because I used the file structure for our CSE15L lab 4 as my foundation, my home directory was `CSE15L-lab4`. In that directory, I had a file for the method which was called `CentralPivotPartitioner.java`, and a bash script file called `test.sh` that had the commands to compile and run the tests. 
Here is the code in each file before the fixes:  

## CentralPivotPartitioner.java:  
```
import java.util.Arrays;
public class CentralPivotPartitioner {
	public static String[] partition(String[] strs, int low, int high) {
		//int h = high - 1;
		int PivotForCenter = (high + low)/2; 
		String pivot2 = strs[PivotForCenter];
		String[] copy1 = strs;
		int index1 = low;
		for (int i = low; i < PivotForCenter; i += 1) {
			if (strs[i].compareTo(pivot2) <= 0) {
				copy1[index1] = strs[i];
				index1 = index1 + 1;
			}
		}
		for (int a = PivotForCenter+1; a < high; a += 1) {
			if (strs[a].compareTo(pivot2) <= 0) {
				copy1[index1] = strs[a];
				index1 = index1 +1;
			}
		}
		copy1[index1] = pivot2;
		int returned1 = index1;
		index1 = index1 + 1;
		
		for (int i = low; i < PivotForCenter; i += 1) {
			if (strs[i].compareTo(pivot2) > 0) {
				System.out.println(strs[i]);
				copy1[index1] = strs[i];
				index1 = index1 + 1;
			}
		}
		System.out.println("here is the last for loop");
		for (int c = PivotForCenter+1; c < high; c += 1) {
			if (strs[c].compareTo(pivot2) > 0) {
				copy1[index1] = strs[c];
				index1 = index1 + 1;
			}
		}
		System.out.print(Arrays.toString(strs));
		System.out.print(Arrays.toString(copy1));
		strs = copy1;
		return strs;
	}

}
```
## test.sh file:
```
set -e

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore partitionerTests
```
## The commands I ran to trigger the bug:
I just used the bash script to run the tests that triggered the bug, so I ran the command `bash test.sh`

## What to do to fix the bug:
To fix the bug, all I had to do was make a "true" copy of the original array rather than another variable that referred to the same object as the original. So to do this, I added code to make a new String array object, then used a for-loop to manually copy each element over. At the end, I used another for-loop to manually update the original array's elements. 
The code fixes look like this:  
```
String[] copy1 = new String[strs.length];  
		for (int  i = 0; i < strs.length; i+=1) {
			copy1[i] = strs[i];
		}
```
and 
```
for (int  i = 0; i < strs.length; i+=1) {
			strs[i] = copy1[i];
		}
```
These blocks of code show what I added in place of what I had previously, which was just single lines of: 

`String[] copy1 = strs` 

and 

`strs = copy1`.
