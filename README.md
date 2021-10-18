# Thyroid-Detection
Thyroid-Detection
Problem Statement
To build a classification methodology to predict the type of Thyroid based on the given training data.
Data Description
The client will send data in multiple sets of files in batches at a given location. Data will contain different classes of thyroid and 30 columns of different values. "Class" column will have four unique values “negative, compensated_hypothyroid, primary_hypothyroid, secondary_hypothyroid”. Apart from training files, we also require a "schema" file from the client, which contains all the relevant information about the training files such as: Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns, and their datatype.

Data Validation
In this step, we perform different sets of validation on the given set of training files.

Name Validation
Number of Columns
Name of Columns
The datatype of columns
Null values in columns
Data Insertion in Database
Database Creation and connection - Create a database with the given name passed. If the database is already created, open the connection to the database.
Table creation in the database - Table with name
Insertion of files in the table
Model Training
Data Export from Db
Data Preprocessing
a) Drop columns not useful for training the model. Such columns were selected while doing the EDA. b) Replace the invalid values with numpy “nan” so we can use imputer on such values. c) Encode the categorical values d) Check for null values in the columns. If present, impute the null values using the KNN imputer. e) After imputing, handle the imbalanced dataset by using RandomOverSampler.
Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction.
Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Random Forest" and "KNN". For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the AUC scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction.
Prediction Data Description
Client will send the data in multiple set of files in batches at a given location. Apart from prediction files, we also require a "schema" file from client which contains all the relevant information about the training files such as:Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns and their datatype.

Data Validation - For Prediction Data
In this step, we perform different sets of validation on the given set of training files.

Name Validation
Number of Columns
Name of Columns
The datatype of columns
Null values in columns
Data Insertion in Database - For Prediction Data
Database Creation and connection - Create a database with the given name passed. If the database is already created, open the connection to the database.
Table creation in the database - Table with name
Insertion of files in the table
Prediction
Data Export from Db
Data Preprocessing
a) Drop columns not useful for training the model. Such columns were selected while doing the EDA. b) Replace the invalid values with numpy “nan” so we can use imputer on such values. c) Encode the categorical values d) Check for null values in the columns. If present, impute the null values using the KNN imputer.
Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.
Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.
Once the prediction is made for all the clusters, the predictions along with the original names before label encoder are saved in a CSV file at a given location and the location is returned to the client.
Deployment
We will be deploying the model to the any Cloud Based Service Platform for example, AWS, Azure, GCP, Heroku or Pivotal Web Services. This is a workflow diagram for the prediction of using the trained model.
