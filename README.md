CS 4641 Project Final Report: Playlist Creation and Similarity
Introduction/Background
Music is a constantly growing and changing field with new artists and songs popping up everyday. As more and more people have begun using different applications such as Apple Music, Spotify, etc., the process of sharing that music with their friends has grown more complex. With the sheer amount of music now available in the world, automatically curated playlists are becoming increasingly more important to both user enjoyment and artist exposure. Being able to generate playlists based on the tastes of two distinct users opens up multiple venues and could have great potential for the future of music streaming and sharing.

Problem Statement
The problem that we are trying to solve is the “blending” of two playlists from separate users in order to create a combined playlist that both people would enjoy listening to. Our goal is to make use of the GTZAN dataset in order to implement a supervised learning model that would be able to classify music into 10 distinct genres. From there, we obtain Spotify song attributes through the Spotify API and build a model that will accept audio tracks of songs from two separate playlists and combine them together. We also plan to give a percentage score that will be based on how much the two playlists match in music taste which will be based on track genre and other Spotify song attributes.

Data Collection
We used the GTZAN dataset to build a model that would allow us to accurately predict the genre of music of various songs given their audio qualities. The GTZAN dataset is a famous dataset in ML projects due to its accuracy and diversity of data. Since the set is so widely available and has been consumed by several users, we found there were a few issues with the data itself, such as files being corrupted and needing to be removed. Nevertheless, other than this, we faced no other issues and processed the audio files accordingly. This preprocessing for the audio consisted of finding the MFCCs (Mel-frequency cepstrum coefficient) for the GTZAN audio files and the test tracks for which we would predict the genre. .

Furthermore, we also gathered 10,000 tracks from Spotify by using its API. For each track, we gathered its attributes such as danceability, popularity, tempo as well as the indicated genre. We then choose the 10 most common genres from the 10,000 tracks and decide those to be the genres that we are looking for. Tracks whose genres were not part of the 10 genres were filtered out, leaving the model with around 6,000 left to train and test.

Methods
With regard to the GTZAN Dataset, two separate models were constructed. The first was the Random Forest Classifier (RFC), while the second was the Convolutional Neural Network (CNN) which was set up to classify the different types of music based on their MFCCs. The PCA conducted on this dataset showed that to retain 90% of the variance in the dataset, we need to retain 30 features (58 in total). Nonetheless, the classifiers worked better with the 58 total features instead of the 30 previously mentioned, so we decided to stick with 58 features instead.

For the Spotify data, we utilized EDA to summarize its main characteristics. The visualization of distribution popularity, duration, and genre count provided an in-depth understanding of the dataset. As a result of the PCA conducted on this dataset, the accuracy of the prediction was not significantly impacted: to retain 90% of the variance in the dataset, we need to retain 12 features (14 in total). Moreover, we applied three different machine learning algorithms: Random Forest, KNN, and SVM. In general, the accuracy of results falls within the range of 50-60% (the fraction of correctly predicted events or the number of correctly predicted events), which is unacceptable.



Figure 1. Accuracy of KNN model





Figure 2. Accuracy of SVM model



Results/Discussion
The CNN model ended with a training accuracy of 0.9299 and a testing accuracy of 0.7483. Since we were focusing on a single feature for classification, using a CNN gave us an advantage in achieving this due to the CNN’s inherent understanding of differentiating between features with similar structures. The way the CNN is built allows the model to understand that every MFCC represents a song. Then, to take that knowledge and discern their differences to classify them into separate sections. Traditional neural networks, on the other hand, would have to learn that the MFCC represents a song each time it attempts to classify a new one. The RFC model ended with an accuracy of around 0.78 without reducing the number of features from their MFCCs. This model works better than a decision tree since it is less prone to overfitting the training data as compared to a normal decision tree.

There are several problems associated with Spotify data, including those arising from the dataset itself and the algorithms used to extract it. The first problem is that the data sample is not sufficiently representative. As Spotify limits the number of retrievals, our data is not comprehensive, encompassing only 10,000 caches over the past decade. A second problem is that the genre labels are not evenly distributed because randomness is not properly utilized when data collection occurs. In conclusion, due to GTZAN's excellent performance, we decided to use it as the main dataset.



Figure 3. Accuracy of CNN model





Figure 4. Accuracy of RFC model

Conclusions
With both the CNN and the RFC giving a good approximation of the data, we decided that implementing a blending algorithm for both would be useful. The RFC’s superior accuracy in classifying shone through when attempting to create the mixed playlists. With the help of the final algorithm, we were able to create a blended playlist of 25 songs from the ‘Liked Songs’ playlists of two users. The RFC generated playlist guarantees with almost 80% certainty that the genres of the songs in the playlist are enjoyed by both users.


Another model that was used based off of the CNN was able to also created a blended playlist based off of the music tastes in two specific playlists of the users. This blend, when analyzing the perceived music preferences of the two playlists, was unable to find a high match. The tested data gave a match of only 37.5%. Thus in order to choose the model and algorithm that was able to provide a playlist that would be more enjoyable by both users, we have decided that the RFC is indeed the superior method to sue in this case.
