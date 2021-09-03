# INTRODUCTION
																			 
Recognizing of emotional conditions in speech signals are so challengeable area for several reason. First issue of
all speech emotional methods is selecting the best features, which is powerful enough to distinguish between
different emotions. The presence of various language, accent, sentences, speaking style, speakers also add another
difficulty because these characteristics directly change most of the extracted features include pitch, energy.
Furthermore, it is possible to have a more than one specific emotion at the same in the same speech signal, each
emotion correlate with a different part of speech signals. Therefore, defines the boundaries between parts of emotion
in very challenging task. The majority of works are concentrated on monolingual emotion recognition, and making a
presumption that there are no cultural diversity between utterers. However, the multi-lingual emotion classification
process have been considered in some research.
![image](https://user-images.githubusercontent.com/57681167/132043303-47032033-5d6d-48af-8274-688bb02b0f4c.png)

# Datasets:
++RAVDESS is released under a Creative Commons Attribution license, so please cite the RAVDESS if it is used in your work in any form.  Published academic papers should use the academic paper citation for our PLoS1 paper.  Personal works, such as machine learning projects/blog posts, should provide a URL to this Zenodo page, though a reference to our PLoS1 paper would also be appreciated 
You can find the dataset here:
## https://smartlaboratory.org/ravdess/

++Toronto emotional speech set (TESS) Collection These stimuli were modeled on the Northwestern University Auditory Test No. 6 (NU-6; Tillman & Carhart, 1966). A set of 200 target words were spoken in the carrier phrase "Say the word _____' by two actresses (aged 26 and 64 years) and recordings were made of the set portraying each of seven emotions (anger, disgust, fear, happiness, pleasant surprise, sadness, and neutral). There are 2800 stimuli in total. Two actresses were recruited from the Toronto area. Both actresses speak English as their first language, are university educated, and have musical training. Audiometric testing indicated that both actresses have thresholds within the normal range.
You can find the dataset here:
## https://tspace.library.utoronto.ca/handle/1807/24487

++CREMA-D est un ensemble de données audiovisuelles pour la reconnaissance des émotions. L'ensemble de données se compose d'expressions émotionnelles faciales et vocales dans des phrases prononcées dans une gamme d'états émotionnels de base (heureux, triste, colère, peur, dégoût et neutre). 7 442 clips de 91 acteurs d'origines ethniques diverses ont été collectés. Cette version ne contient que le flux audio de l'enregistrement audiovisuel original. Les échantillons sont répartis entre l'apprentissage, la validation et le test, de sorte que les échantillons de chaque locuteur appartiennent à exactement une division.
You can find the dataset here:
## https://github.com/CheyneyComputerScience/CREMA-D
++ Surrey Audio-Visual Expressed Emotion (SAVEE) database has been recorded as a pre-requisite for the development of an automatic emotion recognition system. The database consists of recordings from 4 male actors in 7 different emotions, 480 British English utterances in total. The sentences were chosen from the standard TIMIT corpus and phonetically-balanced for each emotion. The data were recorded in a visual media lab with high quality audio-visual equipment, processed and labeled. To check the quality of performance, the recordings were evaluated by 10 subjects under audio, visual and audio-visual conditions. Classification systems were built using standard features and classifiers for each of the audio, visual and audio-visual modalities, and speaker-independent recognition rates of 61%, 65% and 84% achieved respectively.
you can find the dataset here:
## http://kahlan.eps.surrey.ac.uk/savee/
### Our data after some preprocessing looks like
![image](https://user-images.githubusercontent.com/57681167/132044483-36aa02e6-6cb0-47bb-9d85-d7c40ea69f80.png)
### overviow of the number of samples per classe :
![image](https://user-images.githubusercontent.com/57681167/132044611-c6c3e3fe-1b7f-429a-8c5a-50c048959a90.png)
### We can also plot waveplots and spectograms for audio signals

Waveplots - Waveplots let us know the loudness of the audio at a given time.
![image](https://user-images.githubusercontent.com/57681167/132044703-14f7390b-8499-4c86-8267-7c7b6dc32213.png)

Spectograms - A spectrogram is a visual representation of the spectrum of frequencies of sound or other signals as they vary with time. It’s a representation of frequencies changing with respect to time for given audio/music signals.
![image](https://user-images.githubusercontent.com/57681167/132044735-25d89dfe-989b-4477-bc19-a827b233c873.png)
## Data Augmentation
Data augmentation is the process by which we create new synthetic data samples by adding small perturbations on our initial training set.
To generate syntactic data for audio, we can apply noise injection, shifting time, changing pitch and speed.
The objective is to make our model invariant to those perturbations and enhace its ability to generalize.
In order to this to work adding the perturbations must conserve the same label as the original training sample.
In images data augmention can be performed by shifting the image, zooming, rotating ...
First, let's check which augmentation techniques works better for our dataset.
### 1. Simple Audio
![image](https://user-images.githubusercontent.com/57681167/132044875-a34dba5c-cb72-476f-b024-ecd42431bd5f.png)
### 2. Noise Injection
![image](https://user-images.githubusercontent.com/57681167/132044907-272ddbf5-0061-4e97-8d26-f47085010374.png)
### 3. Stretching
![image](https://user-images.githubusercontent.com/57681167/132044947-19b07b53-19c4-40ca-8c6a-cb26e6f9951e.png)
### 4. Shifting
![image](https://user-images.githubusercontent.com/57681167/132044999-94a52069-f183-4b62-98f8-7e9da93fea1f.png)
###  5. Pitch
![image](https://user-images.githubusercontent.com/57681167/132045050-b3dcfcb5-82b9-43cc-955a-010d2f25cb06.png)
# Feature Extraction
Extraction of features is a very important part in analyzing and finding relations between different things. As we already know that the data provided of audio cannot be understood by the models directly so we need to convert them into an understandable format for which feature extraction is used.
The audio signal is a three-dimensional signal in which three axes represent time, amplitude and frequency.
![image](https://user-images.githubusercontent.com/57681167/132045157-05cf820e-5044-4121-b231-4357b4e376b7.png)
As stated there with the help of the sample rate and the sample data, one can perform several transformations on it to extract valuable features out of it.

Zero Crossing Rate : The rate of sign-changes of the signal during the duration of a particular frame.
Energy : The sum of squares of the signal values, normalized by the respective frame length.
Entropy of Energy : The entropy of sub-frames’ normalized energies. It can be interpreted as a measure of abrupt changes.
Spectral Centroid : The center of gravity of the spectrum.
Spectral Spread : The second central moment of the spectrum.
Spectral Entropy : Entropy of the normalized spectral energies for a set of sub-frames.
Spectral Flux : The squared difference between the normalized magnitudes of the spectra of the two successive frames.
Spectral Rolloff : The frequency below which 90% of the magnitude distribution of the spectrum is concentrated.
MFCCs Mel Frequency Cepstral Coefficients form a cepstral representation where the frequency bands are not linear but distributed according to the mel-scale.
Chroma Vector : A 12-element representation of the spectral energy where the bins represent the 12 equal-tempered pitch classes of western-type music (semitone spacing).
Chroma Deviation : The standard deviation of the 12 chroma coefficients.
In this project i am not going deep in feature selection process to check which features are good for our dataset rather i am only extracting 5 features:

Zero Crossing Rate
Chroma_stft
MFCC
RMS(root mean square) value
MelSpectogram to train our model.

We used the OneHotEncoder to encode labels.

### The Model is Sequantial model 
![image](https://user-images.githubusercontent.com/57681167/132046269-4ff7fe78-50be-48cf-8fc3-d840f1dbb6a2.png)

# Results: 
We did a  lot of experiments. The previous model was the best model.
### The result was: 0.68 for train - 0.65 for testing
The final confusion Matrix is : 
![image](https://user-images.githubusercontent.com/57681167/132046643-b8deebee-2e7a-4659-9a3d-c5c70d0de7a0.png)

# Conclusion:
Speech Em
