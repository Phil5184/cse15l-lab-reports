## Logging into ieng6:
To log into the ieng6 remote server, I opened up a new terminal. Then, I typed "`ssh cs15lfa23lw@ieng6.ucsd.edu`". Then I pressed `<enter>`. This command logs me into the ieng6 remote server, which I don't need a password for anymore
because I set up a public/private key for it in a previous lab. 


## Git Cloning the Repository:
To clone the repository, I went on the github page and got the link for it (the SSH url). I copied it to my clipboard using the button next to the url. Then I went to my VSCode terminal and 
typed "`git clone`" `<command> C` into the command line. This results in the command "`git clone git@github.com:Phil5184/lab7.git`", then I pressed `<enter>`. `<command> C` copies the url from my clipboard onto the command line, then the command `git clone git@github.com:Phil5184/lab7.git` clones the repository.

## Running the Tests;
To run the tests, I didn't want to use the long `javac` and `java` commands, and I knew there was a bash script for running the tests, so in order to run the bash script, I first had to change my working directory to the appropriate one.
I typed "`cd lab7`" into the command line, then pressed `<enter>`. Then I typed "`bash test.sh`" into the command line, and pressed `<enter>`. The command `cd lab7` changes my working directory to the `lab7` directory, which is where the
 bash test script is. The command `bash test.sh` runs the bash test script, which runs the tests in the file `ListExamplesTests.java`.


