# Jump Rope Counter
A Python program that puts a jump counter over any jump rope video


## Introduction

During the pandemic, many people started to resort to at-home workouts in order to stay fit during the challenging times. As a result, jump roping saw a steep rise in popularity. People were attracted to jump roping because it is one of the most efficient forms of cardio that can be performed just about anywhere. I recently picked up jump roping myself, and I wanted to create a program that helped keep track of exactly how many jumps I perform during each one of my sets. I decided to use the keras and tensorflow libraries to help me construct a deep learning model that can count the number of 'jumps' I perform in a set. 

## Methodology

The workflow to develop this program was as follows:

1. Gather jump roping videos

   Before starting, I had to gather videos of people jump roping across the internet such as [this](https://www.youtube.com/watch?v=l-m-NxESSfc) one over here. In order to diversify the data, I also asked my friends to send videos of themselves jump roping so I can have data across different environments. It was important to ensure that the data I had was diversified because different people will have slightly different jump roping forms. Additionally, a deep learning algorithm may easily be confused by people jump roping in different environments (ex: a person jump roping in front of an ocean may confuse the program since there is something moving in the background). In total, I used approximatley 15 short clips (0:30 - 1:00 long) of people jump roping. 
   
2. Preprocess each video frame by frame using the Farneback Dense Optical Flow Algorithm
   
   Once I got the videos, I used the Farneback Dense Optical Flow Algorithm to help me process each video frame by frame. The code for this process can be found [here](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Code/Pre-processing%20Jump%20Rope%20videos.ipynb). An example of what some of the preprocessed frames looked like are shown in figure 1.
   
**Fig. 1**:

![alt text](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Images/example%20pic.png "Figure 1")

3. Manually sort and label the frames
   
   After obtaining the frames, I needed to sort and label the data. I broke down a jump into 3 separate movements. The upwards movement, the downwards movement and the landing movement. In order to accurately train the data, I decided to have at least 1000 images for each category of movement. An example of what all 3 of these movements looked like for a typical jump can be found in Figure 2. 
   
**Fig. 2**:

![alt text](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Images/updownland%20ex.png "Figure 2")

4. Train a Convlutional Neural Networkl using the sorted data
   
   After sorting and manually labeling the necessary number of images, I was finally ready to train a Convolutional Neural Network. Using the Keras and Tensorflow libraries, I could train a model that would recognize each of the different types of movements found in a jump. The code for this model can be found [here](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Code/Creating%20the%20Jump%20Rope%20Model%20-%20Final%20Vers..ipynb). The model obtained had an accuracy of 98.45%, which was excellent. Additionally, the model does not appear to be overfitting since the training loss and validation loss are both decreasing as the model gains experience. A graph of the training and validation loss can be found in Figure 3.  

**Fig. 3**:

![alt text](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Images/Loss%20Graph.png "Figure 3")


5. Develop a pipeline that can count the number of jumps
   
   Once I successfully trained the model to accurately determine which 'movement' someone is doing while jumping, I was ready to create a pipeline to count the number of jumps in a video. The program had to preprocess each video frame by frame using the Farneback method. As the video was being processed, each frame was being fed into our model to determine whether the person was moving up, down, or landing. The basic formula of a jump is someone jumping up, coming down and then landing. Once someone landed after jumping up, I would add one 'jump' to their jump counter. The model had some trouble recognizing movements of people before/after they started jump roping. So I had to also add some code that would prevent the model from falsely flagging random movements as jumps. After getting the current number of repetitions, I used OpenCV's VideoWriter feature to add text over the video that would display the current number of jumps. The full code for this pipeline can be found [here](https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Code/Creating%20the%20Jump%20Rope%20Model%20-%20Final%20Vers..ipynb). 
   
   
6. Run test videos through the pipeline to confirm model efficacy
   
   Finally, I had to test the pipeline to make sure that it was accurately counting my jumps. I recorded a video of myself jumping that can be found over [here](https://drive.google.com/file/d/1A0fhjJuwZqqdI97j_lODySHs5ibh7sNY/view?usp=sharing) in order to run them through the algorithm to determine it's true accuracy. Thankfully, the results seemed to be fairly accurate. In the above video, I jumped a total of 107 times, and the counter counted exactly 107 jumps. Figure 4 shows a screenshot of what the output video looked like. Clicking on the image will redirect you to the actual video the program returned.  
   
**Fig. 4**:

<a href="https://drive.google.com/file/d/1ScqBnpjudrtMHInzozW9GtLtHD4nA73d/view?usp=sharing
" target="_blank"><img src="https://github.com/danimaaz/Jump-Rope-Counter/blob/main/Images/example%20screenshot.png" 
alt="Figure 4" width="400" height="400" border="10" /></a>
      
## Conclusion

Overall, this program appeared to be a success, but it still has some work to do. As previously mentioned, the program has some trouble recognizing what some non-jump rope related movement are (such as someone walking in or out of the frame). In future versions, I will gather data to patch this minor bug. That being said, this program is useful enough to help people track their jump roping workouts.

## What's next?

As mentioned in the conclusion, I would like to improve the program's recognition of non-jump rope related movements. Additionally, I would like to also train the model to recognize different jump rope tricks such as the double under, the boxer skip and the alternate foot jump. That way, users can get a more accurate breakdown of what their session consisted of. 
