## Bug from Lab4 - Failure Inducing Input:
I decided to choose the merge test from ListExamples as my bug. Here is the failure-inducing test input:  

```
@Test  
public void mergeTest2() {
    List<String> input1 = new ArrayList<>(Arrays.asList("a", "b", "c", "d", "e"));
    List<String> input2 = new ArrayList<>(Arrays.asList("h", "i"));
    List<String> output1 = new ArrayList<>(Arrays.asList("a", "b", "c", "d", "e", "h", "i"));
    assertEquals(output1, ListExamples.merge(input1, input2));
}
```

## Bug from Lab4 - Successful Input:
Here is the successful test input:  

```
@Test
public void mergeTest1() {
    List<String> input1 = new ArrayList<>(Arrays.asList("a", "b", "c", "h", "i"));
    List<String> input2 = new ArrayList<>(Arrays.asList("d", "e"));
    List<String> output1 = new ArrayList<>(Arrays.asList("a", "b", "c", "d", "e", "h", "i"));
    assertEquals(output1, ListExamples.merge(input1, input2));
}
```

## Symptoms of the 2 Tests above:
Here are the screenshots for the outputs of the 2 tests above after running them at the command line.
![Image](LabReport3Symptom.jpg)

## The Bug (in the Merge method in ListExamples)
Here is the buggy code:  

```
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
      index1 += 1;
    }
    return result;
  }
```

Here is the fixed code:  

```
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
```

The reason why the method was buggy in the beginning was that if your inputs for the method arguments (`list1` and `list2`) were sorted in such a way that the variable `index1` in the method reached the end of `list1` before `index2` reached the end of `list2`, then the method would jump to the 3rd while loop, to finish looping through `list2`. However, inside of the 3rd while loop, instead of updating index2 to continue running through each index in `list2`, the loop would update `index1`. This led to `index1` continuously being updated over and over again while the same element from `list2` was continously added. Thus the Out of Memory Error. 
  
## Researching Commands:  

### grep -c:  

Example 1:  

Input:  ```grep -c "base pair" biomedlines.txt```  


Output:  ```226```  


Example 2:  

Input: ```grep -c ".txt" biomedlines1.txt ```  


Output:  ```74```  


This `-c` command searches through the file provided for lines that match the pattern provided, then prints only the count of the lines that match the pattern. This is useful when you want to find how many lines inside of a file match a pattern without being concerned with the content or where those lines are. Such as the question during lab that asked us to find the number of lines that contained "base pair" in technical/biomed, instead of using `wc` after in order to see the lines, we could have just used `grep -c`.  

Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

### grep -n
Example 1:  

Input: ```grep -n ".txt" biomedlines1.txt```  

Output:
```
1:technical/biomed/1471-2156-2-3.txt
2:technical/biomed/1471-2121-3-10.txt
3:technical/biomed/gb-2001-2-4-research0010.txt
4:technical/biomed/gb-2003-4-4-r24.txt
5:technical/biomed/gb-2001-2-4-research0011.txt
6:technical/biomed/1471-2229-2-3.txt
7:technical/biomed/gb-2001-2-7-research0025.txt
8:technical/biomed/1471-2458-3-5.txt
9:technical/biomed/1471-2199-2-12.txt
10:technical/biomed/gb-2001-2-3-research0008.txt
11:technical/biomed/gb-2001-2-8-research0027.txt
12:technical/biomed/1471-2350-2-2.txt
13:technical/biomed/1472-6750-1-13.txt
14:technical/biomed/1471-2474-2-1.txt
15:technical/biomed/1471-2156-3-16.txt
16:technical/biomed/ar297.txt
```

Example 2:  

Input: ```grep -n "base pair" biomedwords.txt ```  

Output:
```
1:technical/biomed/1471-2156-2-3.txt:          three exons. The first exon contains 279 base pairs (bp)
2:technical/biomed/1471-2121-3-10.txt:        both encode a 10-base pair sequence that is identical to
3:technical/biomed/1471-2121-3-10.txt:        the P3 sequence with an insertion of 3 base pairs at
4:technical/biomed/gb-2001-2-4-research0010.txt:          necessarily true because of Watson-Crick base pairing.
5:technical/biomed/gb-2003-4-4-r24.txt:        important considering that within a few hundred base pairs,
6:technical/biomed/gb-2001-2-4-research0011.txt:          sequenced to completion, yielding a 1,036 base pair (bp)
7:technical/biomed/1471-2229-2-3.txt:        stringency with a 300 base pair homologous 
8:technical/biomed/1471-2229-2-3.txt:        conducted at high stringency with a 1700 base pair
9:technical/biomed/1471-2229-2-3.txt:        approximately 100 base pairs for ease of visualization on
10:technical/biomed/1471-2229-2-3.txt:        amplification product of 579 base pairs. Primer pair T-21
11:technical/biomed/1471-2229-2-3.txt:        455 base pairs. Primers T-31 and T-32 correspond to
12:technical/biomed/1471-2229-2-3.txt:        transcript-3 and amplify a 362 base pair product. Lastly,
13:technical/biomed/1471-2229-2-3.txt:        produce a 238 base pair amplification product. The
14:technical/biomed/1471-2229-2-3.txt:          was a 300 base pair digoxigenin labeled PCR product.
15:technical/biomed/1471-2229-2-3.txt:          analysis was a 1700 base pair PCR product.
```
This `-n` command searches through files for lines that match the provided pattern, and then prints the line number and the contents of the line that match the pattern. This is useful for when you want to look inside a specific file and want lines that match a pattern, as well as where those lines are to find them easier later.

Source: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

### grep -rc
Example 1:  

Input: ```grep -rc "base pair" technical/plos ```  

Output:
```
technical/plos/pmed.0020273.txt:0
technical/plos/journal.pbio.0030032.txt:0
technical/plos/pmed.0020065.txt:0
technical/plos/pmed.0020071.txt:0
technical/plos/pmed.0020059.txt:0
technical/plos/pmed.0010039.txt:0
technical/plos/journal.pbio.0020354.txt:0
technical/plos/pmed.0010010.txt:0
technical/plos/journal.pbio.0020156.txt:0
technical/plos/pmed.0020104.txt:0
technical/plos/pmed.0020272.txt:0
technical/plos/pmed.0020258.txt:0
technical/plos/pmed.0020099.txt:0
technical/plos/journal.pbio.0020140.txt:0
```

Example 2:  

Input: ```grep -rc "base pair" technical/biomed```  

Output:
```
technical/biomed/1472-6807-2-2.txt:0
technical/biomed/1471-2350-4-3.txt:0
technical/biomed/1471-2156-2-3.txt:1
technical/biomed/1471-2156-3-11.txt:0
technical/biomed/1471-2121-3-10.txt:2
technical/biomed/1471-2172-3-4.txt:0
technical/biomed/gb-2002-4-1-r2.txt:0
technical/biomed/gb-2003-4-6-r41.txt:0
technical/biomed/1471-2466-1-1.txt:0
technical/biomed/1471-2199-2-10.txt:0
technical/biomed/1471-2202-2-9.txt:0
technical/biomed/cc991.txt:0
technical/biomed/1471-2369-3-9.txt:0
technical/biomed/bcr620.txt:0
technical/biomed/1476-069X-2-4.txt:0
technical/biomed/1472-6750-3-11.txt:0
technical/biomed/1471-2164-2-9.txt:0
technical/biomed/1471-2091-2-10.txt:0
technical/biomed/gb-2001-2-4-research0010.txt:1
```
This `-rc` command searches through directories and subdirectories and files within those directories for lines that match with the pattern provided, and then next to the file names, it prints the count of the lines that match the pattern. This is useful if you are searching through a directory rather than an individual file and only want the count of the lines in each file that match the pattern, rather than the content. 

Source: I found this command using a combination of a website called "geeksforgeeks" as well as the `man grep` command. Here is the link for the website: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

### grep -rh
Example 1:  

Input: ```grep -rh "base pair" technical/plos ```  

Output:
```
Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
sequence, which is a specific series of eight base pairs in the DNA of the bacterial
chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
```
Example 2:  

Input: ```grep -rh "base pair" technical/biomed```  

Output:
```
          three exons. The first exon contains 279 base pairs (bp)
        both encode a 10-base pair sequence that is identical to
        the P3 sequence with an insertion of 3 base pairs at
          necessarily true because of Watson-Crick base pairing.
        important considering that within a few hundred base pairs,
          sequenced to completion, yielding a 1,036 base pair (bp)
        stringency with a 300 base pair homologous 
        conducted at high stringency with a 1700 base pair
        approximately 100 base pairs for ease of visualization on
        amplification product of 579 base pairs. Primer pair T-21
        455 base pairs. Primers T-31 and T-32 correspond to
        transcript-3 and amplify a 362 base pair product. Lastly,
        produce a 238 base pair amplification product. The
          was a 300 base pair digoxigenin labeled PCR product.
          analysis was a 1700 base pair PCR product.
```
This `-rh` option for grep recursively searches through directories and subdirectories and files inside of the directories to find lines that match with the pattern provided, and then print the lines that match without printing the file name that those lines are in. This is useful if you want to look through a directory and not just an individual file, and only want the content that matches rather than all the file names. 

Source: I found this command using a combination of a website called "geeksforgeeks" as well as the `man grep` command. Here is the link for the website: https://www.geeksforgeeks.org/grep-command-in-unixlinux/

__Disclaimer: For some of the command outputs, I only showed a portion of the output because the full output was too long (some of the outputs were 226 lines long)__
