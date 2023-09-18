Joseph Lucatorto and Mateus Toppin 
EC463 Senior Design Project
09/19/2023


Mini-Project #1

Exercise #1

A few milliseconds 
int- stands for integer; float- stands for float number; No, the program will not run without the use of these notations.
toc - tic may produce an inaccurate result because the values of toc and tic can wrap around. ticks_diff() can account for the changing values of toc and tic by using modular arithmetic. 

Results

Trial 1
How many times shall I loop? 1
How many times shall I sleep for each loop iteration? 1
Total time (measured, predicted) [s] 1.000 1.000
Trial 2
How many times shall I loop? 17
How many times shall I sleep for each loop iteration? 1
Total time (measured, predicted) [s] Answer: 17.020 17.000
Trial 3
How many times shall I loop? 3
How many times shall I sleep for each loop iteration? 3
Total time (measured, predicted) [s] Answer: 9.004 9.00

Exercise #2

We would use a JSON file for parameter storage instead of accepting the parameters as user input() for the ease of the user and speed of the program. By already having a stored JSON file that performs a specific command, this would negate the need for a user input(). 
Using a JSON file to store parameters allows for the user to use functions in the embedded system rather than having to hard-code these functions themselves.
is_regular_file() only returns true for regular files, while os.path.isfile returns true for both regular files and directories. exercise02.py can only work if it reads the parameters from a regular file.

Exercise #3

When the sample time relative to the “dot_dash_threshold” value increases, the user has more time to respond to the wake-up hello message that the Pico flashes in Morse Code.

Trial: 10x increase- 10→100 milliseconds 
Observation: Pace of Morse code lighting was the same, increase in time for the user to respond.  

Exercise #4

***exercise04.json in Git repository 

Voltage divider circuit
Photocell- connected to Pico pin 33 (GND) and 34 (GP28)
10k Ohm Resistor - connected to Pico pin 34 and 36 (“3V3 OUT” pin)

max_bright: 5000 Volts 
min_bright: 62000 Volts 

When a flashlight is shone onto the photocell, we can clearly observe Pico's LED flicker. When the photocell was covered by a finger, the LED did not flicker as obviously, and the results were polar to our former observation. 


Project 1

Have the LED blink at random intervals measure average, minimum, maximum response time for 10 flashes total.
Use a JSON file to store the parameters for the experiment as in the prior exercises. Write the response times to a JSON file along with min, max, average response time and "score" in number of misses vs. total light flashes.



# %% find avg, min, max and print results in JSON file
avg_show= sum(t_good)/len(t_good);
min_show= min(t_good);
max_show= max(t_good);
print(f“The average response time is {avg_show}”)
print(f“The minimum response time is {min_show}”)
print(f“The maximum response time is {max_show}”)
print(f“Number of misses v. Total light flashes: {misses} v. {N}”)
data= f“The average response time is {avg_show}” \n f“The minimum response time is {min_show}” \n f“The maximum response time is {max_show}” \n f“Number of misses v. Total light flashes: {misses} v. {N}”;
Trial 1:

MPY: soft reboot
You missed the light 0 / 5 times
[278, 222, 208, 202, 182]
The average response time is 218.4
The minimum response time is 182
The maximum response time is 278
Number of misses v. Total light flashes: 0 v. 5
write prob1-2023-9-15T11_54_9.json

Trial 2: 

MPY: soft reboot
You missed the light 0 / 5 times
[263, 209, 238, 204, 233]
The average response time is 229.4
The minimum response time is 204
The maximum response time is 263
Number of misses v. Total light flashes: 0 v. 5
write prob1-2023-9-15T12_25_59.json



prob1-2023-9-15T12_25_59.json
"You missed the light 0 / 5 times \n The average response time is 229.4 \n The minimum 
response time is 204 \n The maximum response time is 263 \n 0 v. 5"

Own project 

JSON file

avg_show= 

min_show= min(t_good);
max_show= max(t_good);


Project 2



Have the LED blink at random intervals. Measure average, minimum, maximum response time for 10 flashes total. Measure this using two switches, so that either you and a friend, or use two different fingers to see the response times for two different people / fingers. 
At the same time, in a separate thread, measure the light intensity as in exercise 04 periodically and log to its own JSON file. We are not using semaphores or locks (unless you are experienced and really want to), it's just to show we can run two threads at the same time.
Use a JSON file to store the parameters for the experiment as in the prior exercises. Write the response times to a JSON file along with min, max, average response time and "score" in number of misses vs. total light flashes.

Switch 1 is connected to GP16 (pin 21) and GND. Switch 2 is connected to GP20 (PIN 26) and GND. Resistor connected to GND (pin 23) and grounds both switches. 
Methodology:
First Trial – didn't work
We created a project01a.py that performed the same function that project01.py does but for a different switch. 
Then, we imported project01a into project02.py, editing the code so that this runs after project01 runs its code (project01- the button at GP16 playing the LED game). 
After project01 is performed, project01a runs (project01a- the button at GP16 playing the LED game).
Second Trial – Didn’t work
Change project01.py to incorporate both buttons
Import that onto project 2 
Output goes to JSON file specified in project01.py

Third Trial - Didn’t Work
Change projec01.py to assign switch outside of if statement 
Add switch to project02.py 
Assumption: after project01 runs, project02 will run after using the other switch
Fourth Trial - Success
In project 1
Create parameters P1 and P2 in project01.py; then align then with parameters from JSON file
P1, P2, sample_ms, on_ms= get params (“project.json”)
Set button1 and button2 
In project 2
Import project01 
Set button1 and button2
Align parameters from project01.json to porject02.json
for i in range(P1) and for i in range(P2) loops 

Results
Game works for both switches
One after the other - after one user gets 5 chances on button1, the other user has 5 chances on button2
Prints out misses out of 10

===================================================
