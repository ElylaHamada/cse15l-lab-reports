## Lab report 1
This will be a blog post about the filesystem commands that we learned today in class. These consist of the commands `cd`, `ls`, and `cat`.

The first few examples consist of using the commands with no arguments, this consists of the following: 

<img width="442" alt="Screenshot 2024-04-09 at 00 58 00" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/89dfb6f0-3f11-444b-af68-56a3b622e647">

to begin, the first example of using the `cd` command without any arguments will change our directory to our home directory. the `ls` command did its job to list the files from the directory it is working from, therefore it had portrayed the files that is within the folder that I am currently working from, called elylasfolder. And lastly, the cat command, without any argument will read date from its standard input and write them to the standard output, which basically means that it will just output whatever the user input is.

The next few examples will be using these commands with a path to a directory as its argument:

<img width="442" alt="Screenshot 2024-04-09 at 00 47 36" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/78e10a9b-2f7a-4801-bf3b-f28f74e9c49b">
<img width="442" alt="Screenshot 2024-04-09 at 00 48 55" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/fe6abf49-a2ca-427b-8524-8e39b623261f">
<img width="442" alt="Screenshot 2024-04-09 at 00 49 21" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/af4d1a22-3c84-4512-86cc-4e8c610b31a0">

this second example of using the `cd` command with a path to a directory as its argument shows us that ti had changed from our home directory to the lecture1 directory. Therefore there was no output shown. For the next example, using the `ls` command, since we were already in the lecture1 directory, then I could put the `ls` command without an argument and the result would be the same as putting `ls lecture1` if I were working in the home directory. I included both examples of using the `ls` command with and without its respective argument and the result was the same, as it had listed out the files that are within the directory, being `Hello.java`, `README`, and `messages`. And finally, since the `cat` command really only works on files within the directory, the result was the same without an argument, as it would simply output whatever the user inputs. Additionally, if coding from the home directory and we input `cat lecture1` the result instead shows us `cat: lecture1: is a directory`, meaning that we need a file as an argument for the cat command to work. 

The final examples will be using same 3 commands, `cd`, `ls` and `cat` commands but with a path to a file as an argument. 

<img width="442" alt="Screenshot 2024-04-09 at 00 55 56" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/6c465861-9170-44c7-999d-209379257410">

What these final examples show us is that the `cd` command only works with directories and not paths to a file as an argument. Additionally, the `ls` command, using a path to a file as an argument will print out the name of the file, but not the contents, as shown in the example, that it had simply outputted the name of the file that came from the user input. And lastly, using a path to a file as an argument for the `cat` command will output the contents of the file itself as shown in the screenshot. As we inputted README for the `cat` command, it had outputted the contents of the file which said 
```
javac Hello.java
java Hello messages/en-us.txt
```
> With all of these 9 examples, we can see how these commands work with no arguments, with a path to a directory as an argument and a path to a file as an argument. 

