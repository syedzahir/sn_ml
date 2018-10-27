Smart Data Analytics to Predict ITSM Incident Task category based on Short description. 

A.	Concept
Incident Categorization
•	Use of Machine learning model to predict the categories using incident description
•	Use the AWS Lambda to create a machine learning microservice and have the endpoint triggered by service-Now Rest Message functionality.
•	Retrieve the Rest Message results through workflow and update the records.

Machine Learning –Text Classification Task
•	Data collection
•	Data cleaning / preparation
•	Converting into Document-Term matrix
•	Generating TF-IDF scores of terms
•	Using Classifier of your choice
•	Predictions / Accuracy scores

Approache to handle imbalanced datasets
-	Re-sampling techniques
  Random Oversampling
Increases the number of instances in the minority class by randomly replicating them in order to present a higher representation of the minority class in the data sample



Term-Frequency Inverse Document Frequency
•	TF (Term Frequency)
which measure how frequently a term occurs in a document
TF(t)=(Number of times t appears in a document)/(Total number of terms in the document)
•	IDF (Inverse Document Frequency)
Which measures how important a term is while computing TF, all terms are considered equally important. However it is known that certain terms , such as “is”, “of”, and “that”, may appear a lot of times but have little importance. Thus we need to weigh down the frequent terms while scale up the rare ones, by computing the following
IDF(t) = log_e(total no of document/Total no. of document with term 't' in it)



B.	ITSM Integration with AWS Lambda
1.	The first step is to create a Lambda Function in AWS
Navigate to Lambda > Create Function

2.	In Function Code, you have options to code entry type as:
•	Edit Code inline
•	Upload a zip file
•	Upload a file from S3
I have selected Edit code inline for now for the simple demonstration, then select the Runtime you want to run in and the handler information.
Handler should be of the definition lambda_function_{file_name}.{method_name}

For Example: my Python name is lambda_function and method is lambda_handler.

3.	Then, type the code and analysis you wish to perform. In the example , I am retrieving  the input from API call and returning the output after concatenating the string ‘’something’ to it.

def lambda_handler (event, context):
short_desc=event[‘token’];  //accessing the parameters from api call
return ‘something’+short_desc

4.	Create an execution role with accessing permissions to Lambda and save the functions.
5.	Now, select the API Gateway as the trigger and by default, ANY method is available in the Method Execution
6.	Add the GET method or any other method you wish to call the Lambda function through your API calls.
7.	Now for accessing the parameters from the API query/call, you need to set up the Integration Request from GET method.




C.	Steps to Create Lambda Function and API Gateway

1.	After you create lambda Function add API Gateway from:
Designer->Add trigger->API Gateway select Create API Gateway (from Create API module)
 
OR
We can also create API Gateway through Create API module:

2. NOW create Method->
 In Lambda Function select the lambda function you created, You can also use ‘ANY’ method instead.
