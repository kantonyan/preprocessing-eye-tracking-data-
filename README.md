# preprocessing-eye-tracking-data-
I share my codes on extraction of fixations and saccades on ROIs of a stimuli. 
I created and used the codes for my dissertation. See the example of the stimuli I used (Set1.pptx, infographic). 

First, I run edf2asc64.exe program and converted edf files extracted from eye-tracker to asc files. 

Second, I created csv files (use ascii2csv.ipynb file). Each asc file contained data from one subject, but each subject completed 12 experiemnts. Hence, for each subject I created 12 csv files for each experiment and a combined csv file.  

Third, I estimated 4 ROIs for stimuli. I used the central point of each stimuli, the coordinates of the pixel are (840, 345). 
I followed the recommendations of Salvucci and Goldberg (2000) and created my codes for dispersion-threshold identification (I-DT) method (fixations_saccades_ROI.ipynb). 

(a) The x and y points of the pixels on stimuli were identified by calculating the average of the left and right eyes’ x and y points, respectively. 

(b) The dispersion threshold was calculated for the fixations by calculating the visual angle with the screen resolution (1680 X 1050 pixels) and the subject’s eye distance from the screen (690 mm). In the result, the 47 pixels threshold was accepted. 

(c) The minimum duration of an eye-fixation of 100 ms (Salvucci and Goldberg, 2000; Widdel, 1984; Manor and Gordon, 2003 etc.), and the minimum acceptable duration of an average saccade of 20 ms (Rayner, 2009; Land and Tatler, 2009) were accepted.

The algorithm used the moving window that spans consecutive data points and detects potential fixations. The moving window starts from the first point and accepts the first 100 points. Then the maximum and minimum x and y points are identified in that range and differences between those points are checked using dispersion D = [max(x) - rain(x)] +[max(y) - rain(y)] formula. D is then compared with a 47 pixels threshold, and if it is less than or equal to 47, the window accepts the consecutive data and repeats the steps. If D > 47, the window continues the calculations for the consecutive 20 points. If D > 47 remains true for these 20 points, then the centroid is calculated in the window and classified as a fixation. The following window starts 20 points apart, and the algorithm repeats the steps. The program then iterates several times and if the dispersion between the classified fixations is less than or equal to 47, the two points are merged. In the final stage, once the iterations were completed, the program classified the results as ROI fixations. 

References: 
1. Salvucci, D. D., & Goldberg, J. H. (2000, November). Identifying fixations and saccades in eye-tracking protocols. In Proceedings of the 2000 symposium on Eye tracking research & applications (pp. 71-78).
2. Widdel, H. (1984). Operational problems in analysing eye movements. In Advances in psychology (Vol. 22, pp. 21-29). North-Holland.
3. Manor, B. R., & Gordon, E. (2003). Defining the temporal threshold for ocular fixation in free-viewing visuocognitive tasks. Journal of neuroscience methods, 128(1-2), 85-93.
4. Rayner, K. (2009). Eye movements and attention in reading, scene perception, and visual search. The quarterly journal of experimental psychology, 62(8), 1457-1506.
5. Land, M., & Tatler, B. (2009). Looking and acting: vision and eye movements in natural behaviour. Oxford University Press.
