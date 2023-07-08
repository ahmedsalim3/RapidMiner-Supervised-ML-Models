**1.0 Introduction**
<div align="justify"> 
In today's competitive and saturated market, having an edge over the
competition translates into significant benefits for organizations. The battle among
suppliers of products and services to expand their consumer portfolio and retain
customers has been a constant throughout history. This competition has driven
companies to create countless strategies, actions, and models, leading to the emergence
of entire disciplines studied at universities worldwide. It is thanks to this competition
that statistical techniques and methods are increasingly common in companies. These
techniques enable the proper management of large volumes of data, leading to more
accurate conclusions and even the ability to anticipate events with a certain degree of
probability.
</div> <br>
<div align="justify">
Predictive models are the outcome of grouping statistical techniques and
utilizing them to analyse historical and current data, allowing us to make predictions
about uncertain events that are yet to happen. Through their application, predictions
and probabilities of occurrence can be obtained for each analysed subject. These
models are highly valuable in organizations as they provide crucial information for
decision-making. With their high levels of precision, predictions can be verified,
adjusted, and used to establish future areas of focus, ultimately leading to greater
benefits.
 </div> <br>
 <div align="justify">
Regarding the business insights obtained from the previous assignment,
particularly in relation to customer experience through reviews and satisfaction levels,
it is worth noting that the term "Customer Experience" has become commonplace in
today's business landscape.
 </div><br>
 <div align="justify"> 
This report is based on a database from Olist, an e-commerce company
headquartered in Curitiba, Brazil. The company's main activity is to offer sales
solutions and services to merchants and companies who wish to sell their products
online. They have developed a platform for shopkeepers of all sizes and segments to
register their products to be sold at Olist. Their mission, as stated on their website, is
to strengthen global trade. This part of the report aims to find ways to increase Olist’s
</div><br>
<div align="justify"> 
strength in its e-commerce customer’s experience using supervised machine learning
models. Specifically, our overarching question is: How does item review scores affect
the sale of the products? The software used for this purpose is called RapidMiner and
version 9.10 was used.
</div><br>

**2.0 Dataset Description**
<div align="justify">
The upcoming work will utilize the dataset available on the Kaggle website,
specifically the "Brazilian E-Commerce Public Dataset by Olist." This dataset contains
information about transactions conducted by clients of the company Olist between the
years 2016 and 2018. The dataset was published on September 21, 2018 by Andre
Sionek and Olist. It comprises data from 99,941 purchases made on the platform
between October 3, 2016, and August 29, 2018.
 </div><br>
 <div align="justify"> 
The dataset is organized into eight CSV (Comma Separated Values) structured
tables as seen in schema in Figure 1 below. These tables include a total of 36 mixed
variables, consisting of both categorical and numeric types. These variables provide
detailed information about each purchase, such as the order's final status, total amount
paid, product price, product attributes (e.g., type, description length, number of photos,
dimensions, and weight), as well as customer reviews about their experience. For a
comprehensive overview of the dataset's variables and their types, please refer to Table
1 below for detailed information.
</div><br>

<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/125073e1-7256-4810-bedb-083d2ffb6898">
</div>

**3.0 Data Processing**

 <div align="justify"> 
The data processing stage is crucial for conducting any supervised machine
learning analysis. In this section, we will describe the tasks undertaken and the
attributes used to implement the analysis criteria, four subfolders were created, where
“Data” is used to import the initial Olist datasets, “Process” is used to store the
operators process, “Results” stored the output of the Process using “Store” operator
and “Visuals” where the analytics visualisations were saved.
</div><br>

![2](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/1cb1e044-1eff-4a5b-a885-1439b677fbb6)

 <div align="justify"> 
The initial step of this investigation involved loading the various data sets into
the RapidMiner software using the "Read CSV" operator. Additionally, the "Join"
operator was used to combine the data sets based on their Primary/Foreign keys and
facilitate working with the structured data arrays. During this process, one of the data
sets named "olist_geolocalization_dataset" was excluded as it contained irrelevant data
for the analysis. As a result, the final dataset consisted of seven files instead of the
original eight. The following Figure 3 below shows the process of reading and joining
the datasets, this process is saved within “Process” subfolder under the name “1. Load
and Join the datasets (7 tables)” and its result is stored “Store” operator in Results
subfolder.
</div><br>

<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/6292a876-4426-46a8-a7cc-39bdaa33e6a6">
</div>

 <div align="justify"> 
Next, the "Generate Attribute" operator was employed to create additional
variables, and the "Select Attributes" operator was used to choose specific variables
for inclusion. The following Figures 4,5 are showing the steps of the process and the
functions of 11 new variables.
</div><br>

![4](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/ac2c18a4-b550-4f67-be42-80f36883373b)


<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/b61956ba-88e7-4d3e-8bee-983b2f2b9735">
</div>
<br>
 <div align="justify"> 
The eleven new variables as shown in Figure 5 where extracted from the union
of datasets from previous process and others that were created from the transformation
of others.
</div><br>

 <div align="justify"> 
In the data processing stage, several variables related to the waiting time
between purchase and delivery were generated using the "Generate Attribute"
</div><br>

 <div align="justify"> 
operator. These variables include the columns "estimated_delivery_days” and
"actual_delivery_days" as illustrated in Figure: 5.
</div><br>

 <div align="justify"> 
The " estimated_delivery_days " column indicates the number of days that
have passed between the day customers placed the purchase order (retrieved from the
"order_purchase_timestamp" column) and the day the platform provided as the
estimated arrival day (from the "order_estimated_delivery_date" column). Similarly,
the " actual_delivery_days " column represents the number of days it took for the order
to be delivered to the customer (from the "order_delivered_customer_date" column).
</div><br>

<div align="justify">
The first categorical variable is called " delivery_process," which categorizes
the orders as either “In Advance”, "On Time" or "Late" based on the comparison of
the estimated delivery days and the actual delivery days. If the difference is less than
zero, indicating a delay in delivery, the variable is assigned the value "Late." If the
difference is exactly zero, indicating an on-time delivery, the variable is assigned the
value "On Time". Otherwise, if the difference is greater than zero and not equal to one,
indicating an early delivery, the variable is assigned the value "In Advance.
</div><br>

<div align="justify">
The second variable is a quantitative variable called "late_deliveries." It takes
a value of 1 if the delivery was made later than the estimated date communicated to
the customer and 0 if it was made within the stipulated timeframe. Consequently, the
"early_deliveries" variable represents the opposite scenario, resulting in a qualitative
variable with values of either "true" or "false."
</div><br>
<div align="justify">
On the other hand, "same_city" and “same_state” were incorporated as a
binomial variable to show (with 1 and 0) if the client and the seller are from the same
city/state or not. This seeks to identify if the distance between supply and demand is a
relevant driver for the experience of the users. Also, it was investigated if the size of
the product was a relevant factor for the qualify the experience, for this reason the
variable "product_volumen_cm3" was included, which arises from the multiplication
of the height, width, and depth in centimeters of the product bought.
</div><br>
<div align="justify">
Subsequently, one variable "Relative Delivery Cost" were added to corroborate
if the cost of delivery over the total amount paid was relevant. And, finally, the variable
to be predicted was created: “Experience”. This can take two values: promoter or
detractors, the promoters are the customers with review scores 4 and 5 in the survey;
the detractors, therefore, are the users who scored between 1 and 3. Table 2 below
illustrates the selection of the 29 variables along with the new ones generated.
</div><br>

<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/a7a73741-23f8-4f90-9b8a-c20161b15a1b">
</div>

<div align="justify">
Once the bases were unified and the variables to be considered selected, the
next stage began. remove invalid values. There, more than 2000 orders that had values
were eliminated null in the field "order_delivered_customer_date" and. In addition,
only payment orders were considered with status delivered to have as many dates as
possible with non-empty values and, in the cases in which the date of approval of the
order was null, it was not selected.
</div><br>

<div align="justify">
One of the consequences of the filter to include only the shipments made and
the removal of null values is that the atypical values or outliers that came from the
given by wrongly imputed dates. Figure 6 below shows the third process which is Data
Cleaning after retrieving the selected attributes described in Table 2 previously.
</div><br>

![7](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/c8a30f5f-d65f-4988-8137-267f7d1c2354)
![8](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/0fef34f0-d382-4b15-807a-10eac687ef30)

<div align="justify">
There were also customers who chose to use multiple payment methods or
vouchers. This caused orders to be duplicated, along with the survey responses from
those customers. This issue was resolved by selecting the payment method with the
highest weight in the total amount paid. After making this change, the total payments
were adjusted to reflect that customer paid the full amount using only that payment
method. This ensured that the Relative Delivery Cost variable was not affected.
</div><br>

<div align="justify">
The data cleaning process resulted in a total of 9 0 , 907 orders to be classified
based on the obtained experience, along with 28 variables that will be used to feed the
selected models to achieve the best results.
</div><br>

**4.0 Analysis of data**

<div align="justify">
The results of the data processing led to almost 91,000 orders compared to the
original dataset with 112,516 orders, in order to predict according to the experience
obtained and variables that will feed the models selected. However, the cleaned dataset
has 2 8 variables of mixed origin. In the next lines, a descriptive analysis of the
quantitative variables and qualities considered for the analysis.
</div><br>

<div align="justify">

The first variable to define is order_id. This works as the primary key in the
database of data since it identifies each purchase order sent to customers with a unique
name. This variable was used as ID in RapidMiner to make predictions and it is of type
nominal.
</div><br>

<div align="justify">
On the other hand, we present the attribute to predict: Experience. As we
mentioned in the previous section, this arises as a result of the transformation of the
numerical variable score, and it is of the binomial type since it can take two values,
promoter and detractor. In RapidMiner, this variable was defined as a label to indicate
that it was on which it should calculate the performance of the models. Figure 7 shows
the frequency and the percentages that were the base from which the algorithms carry
out the predictions.
</div><br>

![9](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/e70e8c59-b50f-48bd-a080-4d6863d1ff08)

<div align="justify">
The customers of this dataset made their purchases with four different forms
of payment, and this was recorded in the variable payment_type. The types of payment
used were: credit card, debit card, boleto and vouchers. The participation of each
means of payment on the total purchases can can be seen below in Figure 8.
</div><br>

![10](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/08b03b5b-e24b-4894-a93f-776fb846f0e1)

<div align="justify">
In addition to the variable to be predicted, there are two other binomial
variables that take a value when a condition is met and another when it is not. In this
case the variables took numeric values, therefore the value is 1 if the condition is true
and 0 otherwise. These variables are: late_deliveries, same_state and same_city. In the
first one, it is verified that the number of late shipments, shipments delivered after the
estimated date to the customer, totaled 6, 859 cases (7.5% of the total purchases).
Regarding the number of customers who bought from vendors in the same city, the
records add up to 4, 651 sales that in relative terms is 5.1% of the total. While those
whom are from same state 35.9% (32675 records).
</div><br>

<div align="justify">
Continuing with the detail of the attributes, we find four variables that they are
of the type date: “order_purchase_timestamp”, “order_approved_at”,
“order_delivered_carrier_date”, “order_estimated_delivery_date” and
“order_delivered_customer_date”. None of these variables was considered as input
variables of the models since that did not improve the results. Regarding its
description, Table 3 details the minimum and maximum values, along with the
duration of days.
</div><br>

<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/59d8ea46-00b1-425e-b090-fac32a440100">
</div>

<div align="justify">
The process of obtaining satisfactory results involves multiple iterations, where
small changes are made to determine whether the implementations improve accuracy.
First, we need to establish a baseline measurement. This baseline represents what we
would obtain if no model was applied and serves as our reference point for measuring
improvements. In this analysis, since the predicted variable is binary, the baseline is
determined by the most frequent value, which is the promoters. Their relative presence
in the total records is 7 9. 7 %.
</div><br>

**5.0 Applied Models**

<div align="justify">
In this section, we will first define the models used to carry out predictions
about customer experience, then, the variables of input selected for those models and
finally present the results of model performance.
</div><br>

<div align="justify">
The models applied to predict the customer experience were the following: K-
Nearest Neighbors (Knn), Naive Bayes, Random Forest, Decision Tree and Logistic
Regression. To test the variables and models, a sample of 6,000 orders was taken to
maintain the same proportion of promoters and detractors. This sample was used to
perform optimization tests on the models and make a proper selection of variables.
</div><br>

<div align="justify">

The next step involved normalizing the variables and dividing the sample into
a training set (80% of the total sample) and a test set using a Split Data or Split
Validation operator. To find the best model and parameters, an Optimize Parameters
operator was used to test different combinations and measure their accuracy. Attribute
selection was performed by observing variations in metrics when adding or removing
variables. The selected models and variables were then loaded into the operators, and
a cross-validation operator was used to divide the entire dataset into 10 equal parts.
Each part was tested with a random 10% sample while the remaining data served as
the training set. This process was repeated 10 times with replacement.
</div><br>

<div align="justify">
Regarding the attributes to consider, the selection process consisted of finding
the model that will derive in the greatest accuracy to later add or remove variables and
running the algorithms to observe the variations in the metric. This process helped
determine the input variables and parameters that resulted in the best performance and
improved results.
</div><br>

**5.1 K-Nearest Neighbors**

<div align="justify">
KNN is a non-parametric algorithm that classifies new data points based on
their similarity to existing data points in the training set. It assigns labels to new data
points by considering the labels of the K nearest neighbors. In this case, KNN is used
to predict whether a customer is a promoter, or a detractor based on the similarity of
their features to those of existing promoters and detractors in the training data.
</div><br>

<div align="justify">
The sub-figures below in Figure 9 illustrate the sup-processes flow of the KNN
Process. The first operator retrieves the data from a repository entry named "4. Clean
Selected Attributes" explained previously to be used in subsequent operations. Then
the Date-types were excluded with the Select Attributes operator. After that the
attribute "Experience" was set as the label, indicating it is the target variable to be
predicted. While the "order_id" attribute is assigned the role of "id."
</div><br>

![12](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/77b16f0d-0e4c-4064-9d7e-31c8bbb0ecd7)
![13](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/4aeb5f47-b610-4816-ae99-de7e85a16655)
![14](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/f3ab820e-0b60-4fa5-b87f-1363059fe6e0)

<div align="justify">
Next, stratified sampling was applied to ensure that the resulting sample
maintains the same proportion of promoters and detractors. The sample size is set to
6000 as mentioned previously, and a random seed of 1992 is used for reproducibility.
The whole dataset was normalized to numeric attributes. Where this operator applies
the Z-transformation method to scale the values between 0 and 1, making them
comparable and preventing any single attribute from dominating the analysis.
</div><br>

<div align="justify">
The "Optimize Parameters (Grid)" process performs parameter optimization
for the k-NN (K-Nearest Neighbors) model using a grid search. It splits the data into
training and testing sets, applies the k-NN algorithm to the training set to create a
model, and evaluates its performance on the testing set. The performance metrics
include accuracy, classification error, RSME and MSE. However, the model yielded
82.5% accuracy, 17.5% classification error and +/- 0.144 MSE. Going deeper into the
main problem of this model, what we can find is that it predicts the number of
</div><br>

<div align="justify">
promoters well, improving the starting point, now 79.7%.in 2.96 percentage points as
can be seen in the class precision column in Figure 10 and 11 below.
</div><br>

![15](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/f0f6706f-daf1-4adb-a0a6-32525c6a5585)
![16 (fig11)](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/5165bdb2-d92a-46bf-9b51-1a1260f7bca5)

**5.2 Logistic Regression**

<div align="justify">
Logistic Regression is a type of regression model used to predict non-
numeric variables, such as customer satisfaction (promoter or detractor). Unlike
linear regression, logistic regression applies a transformation function called logit
to handle non-linear relationships. It allows the output to be between negative and
positive infinity, providing adjusted results for analysis.
The sub-figures below in Figure 12 illustrate the sup-processes flow of
the Logistic Regression Process. Like the previous model, the processes from
retrieving data until normalizing is the same.
</div><br>

![Screenshot 2023-07-06 050541](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/39b35737-c5f9-429e-a167-011e165d0a04)
![Screenshot 2023-07-06 050557](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/0accad4f-289f-4e4e-8b14-bebeba16c3be)


<div align="justify">
In the “Split, Train, Test” subprocess we used Split Data to split the dataset
into training and testing sets. The split is performed automatically with a 80% training
set and a 20% testing set. The training set is then used as input for a logistic regression
model using the training set. The parameter for the model is shown in Table 4 below,
after applying the trained model. The model showed an accuracy of 82.83%. Figure
13 below shows the distribution of the class precision.
</div><br>

![19 (fig13](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/57f5fc7b-69e6-434c-8963-1e48e7d9be24)
<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/cf3de7c3-5cb6-4be4-acff-a17f8e7848b3">
</div>

**5.3 Decision Tree**

<div align="justify">
Decision Tree is a flowchart-like model where each internal node represents a
feature, each branch represents a decision rule, and each leaf node represents an
outcome or a class label. It partitions the feature space based on the feature values and
assigns a label to each leaf node. Decision Trees is used to be trained to predict whether
a customer is a promoter, or a detractor based on their feature values. The following
Figure 1 4 shows the process of the Decision Tree and it’s operators.
</div><br>

![21 (fig14](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/a66f8b46-094c-4c22-b860-70b28f564e4c)
![22 (fig14](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/a77f955a-d7fe-4f8d-8310-f30cc78a32c4)
![23 (fig14](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/94194227-6625-41f8-b049-569411f99f22)


<div align="justify">
This Decision Tree model achieved 83.60% accuracy and 16.40 classification
error as shown in Figure 15 below.
</div><br>

![24 (fig15](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/a4e66c2a-4b35-4a5c-90ff-c0c249abb935)
![25 (fig15](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/ab8a73dd-2fb6-4f28-8076-199a7b504ae4)
<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/3f6a1310-f7fc-4df3-bc8d-2756f019a794">
</div>

**5.4 Naïve Bayes**

<div align="justify">
Naive Bayes is a probabilistic algorithm that applies Bayes' theorem with the
assumption of independence between features. It calculates the probability of a new
data point belonging to a specific class based on the joint probabilities of its features.
Naive Bayes is used to predict whether a customer is a promoter or a detractor by
estimating the probability of each class based on the customer's feature values. The
model performed an accuracy of 77% and a classification error of 23%, the following
Figure 17 below shows the operator processes and Figure 1 8 shows the testing results.
</div><br>

![27 (fg17](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/df4178a3-709d-439e-a09a-75de2013981b)
![28 (fig 17](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/1eaee672-152d-43a4-ace2-93331941dc44)

![29 (fig18](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/729cee45-597f-4cf9-ac2b-9336aae7312d)
![30 (fig 18](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/fb3ae928-b13a-46b0-ae68-3945ff2c0387)


**5.5 Stacking**

<div align="justify">
Finally, the assembly of the previously detailed models was carried out using
the stacking model. “stacking" operator, which combines models to improve the final
accuracy. It uses another algorithm, random forest, and achieved an accuracy of
81.88% compared to the initial value of 79.7% of promoters. The following Figures
19 , 20 show its process and results.
</div><br>

![31( fig 19](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/78f30b57-7c05-4d50-9767-3e8ba22a1269)
![32 (fig19](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/f28a3d0f-8b24-4e94-8a20-ff5e1024af96)
![33 (fig19](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/5a337a81-58f8-4da6-a450-7a71df0281b6)
![34 (fig 20](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/65f90d4f-c065-445d-a949-64c2cd39563d)
![35 (fig20](https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/aac8c2ed-3143-4e90-9c56-bcb05d9d7843)

<div align="justify">
Although the overall accuracy of the model did not improve scored 81.88%,
the accuracy of the detractors increased compared to Naïve Bayes and the variance
also improved a little, down 27.03 %. In this way, Table 5 shows a summary of the
results obtained in the models having run them individually compared to the assembled
model that was finally used.
</div><br>
<div align="center">
  <img src="https://github.com/ahvshim/RapidMiner-Supervised-ML-Models/assets/126220185/40201db0-7add-4671-bc80-64727b82c908">
</div>

**6.0 Conclusions**

<div align="justify">
At the beginning of this work, the objective of this report was stated: to predict
the end consumers' experience of Olist using supervised machine learning models.
Being able to use predictive models in Olist opens the possibility of applying them to
other organizations and even sectors. This is thanks to the fact that the company has a
complex data architecture, integrating different types of data (structured, semi-
structured, and unstructured), and belongs to one of the industries with the highest
economic growth of the year. Implementing this prediction in a company that is at the
forefront of technology and data and in a highly dynamic market demonstrates the
importance of including quantitative analysis based on data mining in the customer
experience areas of all organizations.
</div><br>

<div align="justify">
To achieve the proposed goal, transactional user information was used as it
allowed identifying the main drivers of experience, generating specific focus areas for
decision-makers in companies. It should be noted that to reach these results, the
decision was made to analyze the experience of those users who had received their
purchase. This decision was based on the need to simplify data cleaning work and to
form a single database.
</div><br>

<div align="justify">
The data processing resulted in joining the seven tables of the database into
one dataset, with the Read CSV and Join operators with the Primary and Foreign keys.
This resulted in variables of four main groups. Variables related to cost, variables
related to delivery, variables related to the characteristics of the purchased product,
and variables related to the date of purchase. The selection of the variables was based
on deriving the greatest accuracy to later add or remove variables. Additionally, the
models, parameters, and attributes to be included for the selected models were
determined. While some were previously adjusted using an operator called "optimize
parameters," which allows iterating on the parameters to achieve the best fit for the
chosen metric. This way, the models and parameters with the highest predictive
accuracy were selected: logistic regression, random forest, rule induction, and
stacking.
</div><br>

<div align="justify">
The results of the quantitative analysis were obtained using the "stacking"
operator, which combines models to improve the final accuracy. It uses another
algorithm, random forest, and achieved an accuracy of 81.88% compared to the initial
value of 79.7% of promoters.
</div><br>
