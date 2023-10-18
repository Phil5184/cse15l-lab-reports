# `Cd` command with NO arguments
![Image](LabReport1.jpg)
The working directory when this code was run was the `/home` directory. 
There was no output because the command `cd` changes the directory to whatever argument you put in, so since I put in no arguments, there was no change in directory or output to be made. 
This output is not an error.

# `Cd` command with a path to a directory as an argument
![Image](LabReport2.jpg)
The working directory when this code was run was the `/home` directory. There was no output, but the working directory after running the code did change to the `/lecture1` directory. This is the expected result/output, since the `cd` command changes the directory to the argument that you put in, and my argument was `/home/lecture1`, so the directory changed to `/lecture1`. This is not an error. 


![Image](LabReport3.jpg)
The working directory when this code was run was the `/lecture1` directory. The output was an error message saying that the path to the file that I put in as the argument is "not a directory". This is because the `cd` command works to change directories, and if you put in an argument that is not a directory, the command cannot work. This is an error because we tried using a file as the argument for `cd`, and the working directory cannot be changed to something that is a file (like `en-us.txt`). 

![Image](LabReport4.jpg)
The working directory when this code was run was the `/lecture1` directory. The output was a list of all the files and folders that are "inside" of `/lecture1`. This is because the ls command returns a list of the folders and files inside of the current working directory (or the current argument), and if the current working directory is `/lecture1`, then the `ls` command will show all files inside `/lecture1`. This is not an error. 

![Image](LabReport5.jpg)
The working directory when this code was run was the `/lecture1` directory, like before. The output was the same as before because the argument I put was `/home/lecture1` and the `ls` command returns the files and folders inside of the argument (`/lecture1`). This is expected and is not an error. 

![Image](LabReport6.jpg)
The working directory when this code was run was the `/lecture1` directory. The output showed a pathway to the file that was the argument (so the output was the exact same as the argument) and this is because we provided a file as the argument, which has no files or folders inside of it. The command `ls` cannot work with this as an argument, because there is nothing to show if there is nothing inside of the argument provided. I believe this is an error because we provided an argument that does not work with the command `ls`. 

![Image](LabReport7.jpg)
The working directory when this code was run was the `/lecture1` directory. The output is nothing, and it "broke" the terminal because I was not able to type in any other commands or arguments after. This output was because the command `cat` usually prints out the text that is in the file provided as the argument. If there is no argument, there is no file to print out text from. I believe this is an error, because we did not provide an argument for the command to work on, and the command also broke the terminal. 

![Image](LabReport8.jpg)
The working directory when this code was run was the `/lecture1` directory. The output was an error message stating that the argument `/home/lecture1` was a directory. This is because the command `cat` only works with files to print out the text in those files. It does not work with directories that have no text to print. This is an error because we provided an argument type that does not work with the command and as seen, the output is not what we wanted. 

![Image](LabReport9.jpg)
The working directory is the `/lecture1` directory, like last time. The output is the "Hello World!" message because this is the text that is inside the `en-us.txt` file, which is the file path that we provided as the argument. In this case, the command `cat` works as expected and this is not an error.
