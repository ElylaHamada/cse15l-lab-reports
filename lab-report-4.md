# Lab Report 4

## Step 4

ssh echamada@ieng6.ucsd.edu

<img width="751" alt="Screenshot 2024-06-04 at 12 41 25" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/91c1fd11-6abc-4199-995f-5527992545d4">

## Step 5
First step was that I forked the given repository into my GitHub account and then cloned the repository into VSCode in my ssh account.

<img width="751" alt="Screenshot 2024-06-04 at 12 43 09" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/9617a446-fab0-4194-877d-f44a93db1983">

## Step 6

To run tests, I changed directory into lab7 by `cd lab7` and then did `bash test.sh` to run the tests and it showed one failure.

<img width="751" alt="Screenshot 2024-06-04 at 12 43 53" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/7d079b12-9168-4ce4-bb7e-fe48d6cafb71">

## Step 7

I typed ```vim ListExamples.java```, to fix the errors. My keystrokes were ```<shift + G>, <up>, <up>, <up>, <up>, <up>, <up>, e, x, i, 2, <esc>, <:wq>```.

To fix the first error, I removed the 0 in the line 15 which was initially `result.add(0, s);` and changed it to `result.add(s);`

The second error was in line 44 where the code stated `index1 += 1;` in reference to index2, so I changed it to `index2 += 1;`

<img width="751" alt="Screenshot 2024-06-04 at 12 48 24" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/b73dd800-e101-4e33-bc60-f5d9063c24a5">

<img width="751" alt="Screenshot 2024-06-04 at 12 48 10" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/52fb5626-af18-45c4-b62b-06a7b6cbc2a0">

## Step 8
To retest the tests after fixing them, I inputted the bash command `bash test.sh` again to see that there is no more errors
<img width="751" alt="Screenshot 2024-06-04 at 13 15 37" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/5c283c04-0e57-47cf-80e3-0f6108e9fa64">

## Step 9

To commit and push the changes onto github i first put the commang `git add *.java` which will ready all the fiels in the lab7 directory. Then I used `git commit -m "now passing both tests"` which saves all the changes we did and also commits the messages "now passing both tests".
Lastly, to upload these changes to the lab7 repo on github, I used the command `git push origin  main`

<img width="751" alt="Screenshot 2024-06-04 at 13 14 44" src="https://github.com/ElylaHamada/cse15l-lab-reports/assets/130731509/2de5b67f-dbcb-4276-8bbf-69aab7f54d64">
