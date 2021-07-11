# Jump Rope Counter
A Python program that puts a jump counter over any jump rope video


## Introduction

During the pandemic, many people started to resort to at-home workouts in order to stay fit during the challenging times. As a result, jump roping saw a steep rise in popularity. People were attracted to jump roping because it is one of the most efficient forms of cardio that can be performed just about anywhere. I recently picked up jump roping myself, and I wanted to create a program that helped keep track of exactly how many jumps I perform during each one of my sets. I decided to use the keras and tensorflow libraries to help me construct a deep learning model that can count the number of 'jumps' I perform in a set. 

## Workflow

The workflow to develop this program was as follows:

1. Gather jump roping videos

   Before starting, I had to gather videos of people jump roping across the internet such as [this](https://www.youtube.com/watch?v=l-m-NxESSfc) one over here. In order to diversify the data, I also asked my friends to send videos of themselves jump roping so I can have data across different environments. It was important to ensure that the data I had was diversified because different people will have slightly different jump roping forms. Additionally, a deep learning algorithm may easily be confused by people jump roping in different environments (ex: a person jump roping in front of an ocean may confuse the program since there is something moving in the background). In total, I used approximatley 15 short clips (0:30 - 1:00 long) of people jump roping. 
   
2. Preprocess each video frame by frame using the Farneback Dense Optical Flow Algorithm
   
   Once I got the data, I used the Farneback Dense Optical Flow Algorithm to help me process each video frame by frame. I 
