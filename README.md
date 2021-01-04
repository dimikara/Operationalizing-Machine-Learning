# Operationalizing Machine Learning

## Table of contents
   * [Overview](#Overview)
   * [Architectural Diagram](#Architectural-Diagram)
   * [Key Steps](#Key-Steps)
   * [Screen Recording](#Screen-Recording)
   * [Future work](#Future-work)
   * [Standout Suggestions](#Standout-Suggestions)
   * [Dataset Citation](#Dataset-Citation)
   * [References](#References)

***


## Overview

In this project, I used Azure to configure a cloud-based machine learning production model, deploy it, and consume it. After that, I created, published, and consumed a pipeline. The whole procedure is explained in this README file and is demonstrated in a screencast video.

The dataset used can be obtained from [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and contains marketing data about individuals. The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict whether the client will subscribe a bank term deposit (column y).

***
## Architectural Diagram

The diagram below is a visualization of the flow of operations from start to finish:

![Architectural Diagram](img/Architectural_diagram.png?raw=true "Architectural Diagram") 


***
## Key Steps

*TODO*: Write a short discription of the key steps. Remeber to include all the screenshots required to demonstrate key steps. 

The key steps of the project are described below:

- **Authentication:**
This step was actually omitted since it could not be implemented in the lab provided by Udacity. However, I am still mentioning it here as it is a crucial step if one uses their own Azure account.

- **Automated ML Experiment:**
At this point, security is enabled and authentication is completed. This step involves the creation of an experiment using Automated ML, configuring a compute cluster, and using that cluster to run the experiment.

- **Deploy the Best Model:**
After the completion of the experiment run, a summary of all the models and their metrics are shown, including explanations. The _Best Model_ will appear in the _Details_ tab, while it will appear first in the _Models_ tab. This is the model that should be selected for deployment. Its deployment allows to interact with the HTTP API service and interact with the model by sending data over POST requests.

- **Enable Logging:**
After the deployment of the Best Model, I enabled Application Insights and retrieve logs.

- **Swagger Documentation:**
This is the step where the deployed model will be consumed using Swagger. Azure provides a Swagger JSON file for deployed models. We can find the deployed model in the _Endpoints_ section, where it should be the first one on the list.

- **Consume Model Endpoints:**
Once the model is deployed, I am using the ```endpoint.py``` script to interact with the trained model. I run the script with the _scoring_uri_ that was generated after deployment and the _key_ of the service. This URI is found in the _Details_ tab, above the Swagger URI.

- **Create and Publish a Pipeline:**
In this part of the project, I am using the Jupyter Notebook with the same keys, URI, dataset, cluster, and model names already created.

- **Documentation:**
The documentation includes: 1. the [screencast](YouTube-link) that shows the entire process of the working ML application; and 2. this README file that describes the project and documents the main steps.

***
## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

[sadmi]
* The working deployed ML model endpoint.
* The deployed Pipeline
* Available AutoML Model
* Successful API requests to the endpoint with a JSON payload
* The Jupyter Notebook

***
## Future work ---->>>ΝΑ ΤΟ ΑΛΛΑΞΩ - ΕΙΝΑΙ ΙΔΙΟ ΜΕ ΤΟ PROJECT 1

* The data is **highly imbalanced**:

![Highly imbalanced data](img/Imbalanced_data_plot.png?raw=true "Highly imbalanced data")

Class imbalance is a very common issue in classification problems in machine learning. Imbalanced data negatively impact the model's accuracy because it is easy for the model to be very accurate just by predicting the majority class, while the accuracy for the minority class can fail miserably.

There are many ways to deal with imbalanced data. These include using: 
1. A different metric; for example, AUC_weighted which is more fit for imbalanced data
2. A different algorithm
3. Random Under-Sampling of majority class 
4. Random Over-Sampling of minority class
5. The [imbalanced-learn package](https://imbalanced-learn.readthedocs.io/en/stable/)

There are many other methods as well, but I will not get into much details here as it is out of scope. 

Concluding, the high data imbalance is something that can be handled in a future execution, leading to an obvious improvement of the model.

* Another factor that I would improve is **n_cross_validations**. As cross-validation is the process of taking many subsets of the full training data and training a model on each subset, the higher the number of cross validations is, the higher the accuracy achieved is. However, a high number also raises computation time (a.k.a. training time) thus costs so there must be a balance between the two factors.

    _Note_: In case I would be able to improve ```n_cross_validations```, I would also have to increase ```experiment_timeout_minutes``` as the current setting of 15 minutes would not be enough. 

***
## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.

***
## Dataset Citation

[Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014

***
## References

- Udacity Nanodegree material
- [App](https://app.diagrams.net/) used for the creation of the Architectural Diagram
- [Prevent overfitting and imbalanced data with automated machine learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-manage-ml-pitfalls)
- [Dealing with Imbalanced Data in AutoML](https://www.drware.com/dealing-with-imbalanced-data-in-automl/)
- [Dealing with Imbalanced Data in AutoML](https://techcommunity.microsoft.com/t5/azure-ai/dealing-with-imbalanced-data-in-automl/ba-p/1625043)
- A very interesting paper on the imbalanced classes issue: [Analysis of Imbalance Strategies Recommendation using a
Meta-Learning Approach](https://www.automl.org/wp-content/uploads/2020/07/AutoML_2020_paper_34.pdf)
- [Imbalanced Data : How to handle Imbalanced Classification Problems](https://www.analyticsvidhya.com/blog/2017/03/imbalanced-data-classification/)



