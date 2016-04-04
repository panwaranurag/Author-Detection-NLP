# Author-Detection-NLP


This project contains a procedure which takes text files (whose filename is named after the author), and learns the author's style, paragraph by paragraph, in order to make predictions on unseen paragraphs.

The file ``author_classify.py`` defines a class ``data_builder`` which initializes with a folder name, and extracts text from all the pre-processed text files in the folder that end with ``_pcd.txt.`` Calling the ``pos_vectorize()`` method will then extract the tagword features from the already extracted text and turn them into vectors for the SVM. The vectors will then be stored in the class variable ``vec_list.``

The ``clf_data`` is a class that acts as a container for the data to be classified, after the data has been gathered in a data_builder. On initializing, it splits the data from ``vec_list`` into training and test data. 

The ``subs_xval`` function takes as argument a ``data_builder`` instance and integer ``iters``, automatically converts it to a ``clf_data`` container, and performs subsample cross-validation ``iters`` times. It prints the Fscore, precision and recall.

This project uses `scikit learn`_ module's SVM, and POS tagger, WordNetLemmatizer and PorterStemmer from the NLTK_ (natural language toolkit)

#Test run result

Extracting data from files...
['test\\ElbertHubbard_JohnJacobAstor.txt', 'test\\HenryDavidThoreau_OntheDutyofCivilDisobedience.txt']<br />
    Opening file ElbertHubbard_JohnJacobAstor.txt<br />
    Opening file HenryDavidThoreau_OntheDutyofCivilDisobedience.txt<br />
extract_data() 586.21 sec<br />

 Adding info from author "HenryDavidThoreau_OntheDutyofCivilDisobedience" into master tag dict<br />
 Adding info from author "ElbertHubbard_JohnJacobAstor" into master tag dict<br />
 Processing tag vectors for author "HenryDavidThoreau_OntheDutyofCivilDisobedience"<br />
Dumping to test\svec\HenryDavidThoreau_OntheDutyofCivilDisobedience_svec.txt<br />
 Processing tag vectors for author "ElbertHubbard_JohnJacobAstor"<br />
Dumping to test\svec\ElbertHubbard_JohnJacobAstor_svec.txt<br />
Labeling vectors<br />
Adding vec for HenryDavidThoreau_OntheDutyofCivilDisobedience<br />
Adding vec for ElbertHubbard_JohnJacobAstor<br />
Completed in 0.23300 seconds<br />
pos_vectorize() 2.25 sec<br />

HenryDavidThoreau_OntheDutyofCivilDisobedi:<br />
Overall Fscore: 0.9091<br />
Overall Precision: 1.0000<br />
Overall Recall: 0.8333<br />
[[16  0]<br />
 [ 1  5]]<br />

ElbertHubbard_JohnJacobA:<br />
Overall Fscore: 0.8148<br />
Overall Precision: 0.9167<br />
Overall Recall: 0.7333<br />
[[11  4]<br />
 [ 1  6]]<br />

subs_xval() 0.25 sec<br />

main() 588.92 sec<br />

#Steps followed:
*Define classes (In our case we used file name as Author name)<br />
*Extract features<br />
*Train ML classifier (Used SVM from scikit-learn library)<br />
*Evaluation<br />

Class definition:<br />
*AuthorA, AuthorB, AuthorC,………, AuthorN<br />
Feature extraction:<br />
*Lexical features<br />
*Character features<br />
*Syntactic features<br />
*Application specific<br />
 
 #Features used in our scenario:<br />
1.	Lexical features (word frequencies(tf-idf))<br />
2.	Syntactic features (POS tags)<br />

Lexical features:<br />
*Word length, sentence length<br />
*Word frequencies (tf-idf)<br />
*Vocabulary richness<br />
*Word n-grams<br />
         Syntactic features:<br />
*POS tags(eg VB, NN etc)<br />
*Sentence and phrase structure<br />
          ML classifier:<br />
	We used Linear SVM from scikit-learn<br />
          Evaluation:<br />
Confusion matrix for two author test case<br />
ElbertHubbard_JohnJacobAstor:<br />
Overall Fscore: 0.9412<br />
Overall Precision: 0.8889<br />
Overall Recall: 1.0000<br />
Confusion matrix<br />
[[16  0]<br />
 [ 2  4]]<br />

HenryDavidThoreau_OntheDutyofCivilDisobedience:<br />
Overall Fscore: 0.8571<br />
Overall Precision: 1.0000<br />
Overall Recall: 0.7500<br />
Confusion matrix<br />
[[18  0]<br />
 [ 1  3]<br />
