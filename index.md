# Lab Report 5
## Elyla Hamada / echamada@ucsd.edu
## CSE 15L

# Part 1. Debugging Scenario
# Piazza Post
**What environment are you using?**
I am running code on the software VS Code on MacBook Pro.

**Describe the symptom that you are seeing. Be specific and make sure to include what you are seeing and what you expect to see.**

<img width="480" alt="Screenshot 2024-06-10 at 22 21 19" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/2d1b6bdb-5f60-49d4-a252-1231930391d3">

Above is the error that I have been receiving. The command that I ran was based on the wavelet lab, but it tosses an error because it says that the main class could not be found.

I had input `vim NumberServer.java` to see if there were any errors that I was missing or any bugs within the code

**Detail the failure-inducing input and context. That might mean any or all of the commands you're running, a test case, command-line arguments, a working directory, and even the last few commands you ran.**
The input that I put after compiling both java files was `java NumberServer.java Server.java` I am using the commands provided by Week 2.

## TA Response
Please look through the command in week 2's lab carefully. When running the java command, what is the `.java` file that you are running it against? Please read through the code for both Java files as well.

## Terminal Output
Oh okay, thank you! I read through the lab again and saw that I was missing the port number to get the server started.
<img width="830" alt="Screenshot 2024-06-10 at 23 30 50" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/617fa94c-7ffc-4972-803b-50c299820ec7">

## Setup
- Fork https://github.com/ucsd-cse15l-s24/wavelet in a SSH ieng6 and navigate to the `/wavelet` directory
- The contents from the forked repository are unmodified
- The input is `javac NumberServer.java Server.java`
- To fix the bug, input the port number after compiling both files together

## Part 2. Reflection
Through CSE 15L, I've learned how to navigate through Java easier and I enjoyed learning VIM functions. With taking other CS classes before, I had to go to tutoring hours a lot to get help in debugging my errors but with this class, it is now more easier to understand the bugs in the file and how to debug them.


