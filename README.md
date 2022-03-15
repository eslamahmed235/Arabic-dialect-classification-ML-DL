# Arabic-dialect-classification-ML-DL

This project is dedicated to build a classification pipeline to the problem of Arabic dialects identification, labels contain 18 clasess/dialects, using a classic ML and modern DL approaches.


# Dataset

The dataset and the dialect identification problem were addressed by Qatar Computing Research Institute, moreover, they published a paper, feel free to get more insights from it, [Arabic Dialect Identification paper](https://arxiv.org/pdf/2005.06557.pdf)
![dialect distripution ](https://github.com/eslamahmed235/Arabic-dialect-classification-ML-DL/blob/main/doc/68747470733a2f2f6c68352e676f6f676c6575736572636f6e74656e742e636f6d2f4671586f56787455305042716347366a5a334130435a716b4f414a4f696f7831497a612d4f5948654c63757869694659763369394357364e467576326c36317a307a6e6f655.png)

# pipeline 

pipeline with the following steps from starting from git data set with Post request to evaluation 

##  1. DATA FETCHING

 - Load dialect Tweet ID file 
 - Create chunked List with fixed size 1000 recored
 - Create doc request with JSON as a list of IDs
 - Create API Post Request 5. Save output request response in csv file

##  2. DATA PRE-PROCESSING

In Data PRE-PROCESSING We have Two choice: 
 - Apply pre-processing and cleaning manually Using ex. Regex, NLTK, word iterations and Apply pre trained models and packages for preprocessing Using ex. Arabert, merbert, and Camel.
 I Decision to go throw manually pre-processing with Machine learning Model with the Following steps: 
 1. clean Hashtag and mention  { #, @ }
 2. remove emoji 😀
 3. remove Stop words {هو , انا , الذى }
 4. remove and replace Tashkeel {  فَتْحَة , ضَمَّة , كَسْرَة, سُكون }
 5. Insert white spaces and remove un-Arabic characters { "		" }
 6. collect All functions and apply some filters 
 7. Split words with “ + ” sign { " + "}
![Tweet before and After manually pre-processing](https://github.com/eslamahmed235/Arabic-dialect-classification-ML-DL/blob/main/doc/Picture1.png)

with Deeplearing Model I decided to use [** Arabert  v2**](https://github.com/aub-mind/arabert) 

1. Choose **Arabert V2**
2. Select ***AraBERTv0.2-Twitter-base*** Model

##  3. Machine learning Model

In **feature transformation** After several Attempts  
select to apply cominaation between two TfidfVectorizer for words and character.
In **Machine learning model** After several Attempts  
Select apply ensembleing with **VotingClassifier** with  the following models: “SGDClassifier”, “LinearSVC”, “MultinomialNB”, and “BernoulliNB”
![ML_model classification report](https://github.com/eslamahmed235/Arabic-dialect-classification-ML-DL/blob/main/doc/Picture3.png)


##  4. Deep learning Model

In **feature transformation** used **Arabert** tokenizer and padding
In Deep learning model select **AutoModelForSequenceClassification** from transformers from pytorch with batch_size = 60 and total steps = 6660
Using **Saturncloud GPU**

![DL_model  training Epoch](https://github.com/eslamahmed235/Arabic-dialect-classification-ML-DL/blob/main/doc/Picture4.png)


##  5. Evaluation
|model| F1_score  | Accuracy
|-- |--| --|
|Machine Learning Model| 51.3%  | 51.8%
|Deep Learning Model| 59.06%  | 59.7% 
