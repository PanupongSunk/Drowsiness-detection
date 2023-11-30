# Drowsiness-detection
This is the author's thesis work. if you need more details, please contact the email below.<br>
Email: panupong.sunk@gmail.com<br>
This is the drowsiness detection system based on the binary classification model created by a neural network. Physiological data (heart rate and pulse rate variability (prv)) acquired from a remote photoplethysmography (rPPG) signal retrieved from human facial video are used as inputs to the classification model. The result is determined as alert or drowsy.
# Model
The model is uploaded in the folder "model" along with the mean and standard deviation values of each feature acquired from the training data. <br>These two files need to be downloaded and imported to run the program.<br>
This model is trained by using a private dataset, which is a human facial video in alert and drowsy conditions. To use this model, the feature data extracted from facial video with dimension (11,) are used as inputs to the model.
# Example Videos
Two 5-minute videos (RGB lossless format) of the same person (one from an alert condition and one from a drowsy condition) are in a .zip file. Note that these two videos are completely new to the model, and you can use them to test this program. 
# Main file
The main file used to run this system is in the .ipynb notebook. The user is needed to upload the facial video to this file. The face mesh model from MediaPipe [1] is used to track and detect face.
<br>In this work, the author selected the forehead area as the region of interest (ROI). The RGB colors from each video frame are then extracted from the forehead area and collected until have a length equal to 20s.
These 20s RGB color data are used to calculate the rPPG signal using the modified POS method [2]. The 20s RGB color data is updated by removing the first 1s data from the beginning and appending the new 1s data to the end. 
<br>In this case, the author proposed the method used to improve the quality of the rPPG signal [3] by using a hair detection algorithm to remove the hair area on the forehead. The rPPG signal is extracted only from the skin area. The majority vote in subinterval is also used to improve the quality of rPPG signal by narrowing the passband frequency of the bandpass filter and using this new frequency band to filter the rPPG signal. <br>The heart rate is calculated by applying the Fast Fourier Transform to the improved rPPG signal and the prv is calculated based on the time, frequency, and nonlinear domain using the algorithm and equation shown in [4]. <br>After obtaining heart rate and prv, the average value of each 10s data from these features are provided to the classification model to find the condition of the subject.
# References
[1] MediaPipe: https://mediapipe-studio.webapps.google.com/home<br>
[2] Ryu, J., et al. (2021). "Research on the combination of color channels in heart rate measurement based on photoplethysmography imaging." J Biomed Opt 26(2).<br>
[3] Sunkom, P., Worasawate, D., Srisurangkul, C., and Nakayama, M. (2023). Improved Heart Rate Estimation From Facial Videos Using Hair Detection and Majority Vote in Subintervals. In Proceedings of  JCSSE 2023 the Twentieth International Joint Conference on Computer Science and Software Engineering, pp. 380-384. Phitsanulok, Thailand.<br>
[4] Neurokit2: https://github.com/neuropsychology/NeuroKit<br>










