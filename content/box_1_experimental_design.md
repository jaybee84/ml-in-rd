# Understanding experimental design of machine learning to inform requirements for data

### Components of ML experiments

Machine learning algorithms identify patterns that explain or fit a given dataset.
Every machine learning algorithm (_model_) goes through a _training_ phase where it identifies underlying patterns in a given dataset, and a _testing_ phase where the model applies the identified patterns to unseen data points.
So every model should be provided with the following fundamental parts as input: 1. a _training dataset_ , 2. an _evaluation dataset_ , 3. a _held-out validation dataset_ .
Typically each of these input datasets consists of a matrix (or dataframe or table) where features form the rows and samples form the columns.
A _training dataset_ is used to expose the model to underlying patterns among the features present in the data of interest.
An _evaluation dataset_ is a small test dataset which is used during the training phase to help the model iteratively update its parameters (i.e., _hyperparameter_tuning_ or _model tuning_).
A large training set may be subdivided to form a smaller training dataset and the evaluation dataset and both used to train the model (see next section for more details on cross-validation).
In the testing phase, a new or unseen test dataset or _held-out validation set_ is used to test whether the patterns learned by the model can be generalized to new data points.
While the evaluation dataset helps the model iteratively update its parameters to learn important patterns in the training data, the held-out validation set helps test the generalizability of the model.
Generalizability of a model is its ability to recognize patterns that can help predict the class or an outcome for previously unseen data.
High generalizability of a model on previously unseen data suggest that the model has identified fundamental patterns in the data that may also inform our knowledge regarding the question of interest for which the experiment was designed.
Generalizability can be affected if _data leakage_ occurs during training of the model, i.e., if a model is exposed to the same or similar data points in both the training set and the held-out test set.
Ensuring absence of any overlap or relatedness among data points or samples (e.g., samples with familial relationship, samples from same patient) used in the training set and held-out test set is important to avoid _data leakage_ during model training.
Specifically in cases of rare genetic diseases where many samples can contain familial relationships, special care should be taken while crafting the training and testing sets to ensure that no data leakage occurs and the trained model has high generalizability.


### Training and testing

The implementation of a machine learning experiment begins with splitting a single dataset of interest such that 90% of the data is used for training (generally subdivided into the _training dataset_ and the _evaluation dataset_), and remaining 10% of the data is used for testing or validation (as the _held-out validation dataset_).
This makes sure that all the datasets involved in training and testing a model maintain uniformity in the features.
In case of rare diseases where multiple datasets may be combined to make a large enough training dataset, special care is taken to standardize the features and the patterns therein.
The iterative training stage helps the model learn important patterns in the training dataset and then use the evaluation dataset to test for errors in prediction and update its learning parameters (_hyperparameter tuning_).
The method by which the evaluation dataset tests the performance of the trained model and helps update the hyperparameters is called _cross-validation_.
To maximally utilize the available data for cross-validation, there can be multiple approaches to form the training and evaluation datasets e.g. leave-p-out cross-validation, leave-one-out cross-validation, k-fold cross-validation, Monte-Carlo random subsampling cross-validation [@doi:10.1007/978-1-4614-6849-3].
In case of k-fold cross-validation, a given dataset is shuffled randomly and split into _k_ parts.
One of the _k_ parts is reserved as the _evaluation dataset_ and the rest are cumulatively used as the _training dataset_.
In the next iteration, a different part is used as the _evaluation dataset_, while the rest are used for training.
Once the model has iterated through all _k_ parts of the training and evaluation datasets, it is ready to be tested on the _held-out validation_ dataset. 

The held-out validation dataset is exposed to the model only once to estimate the accuracy of the model.
High accuracy of a model on the training dataset but low accuracy on the held-out dataset is a sign that the model has become overfit to the training set and has low generalizability.
If this is encountered, the experimenter is advised to revisit the dataset construction to make sure they meet the best practices outlined above.




