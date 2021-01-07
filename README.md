# Operationalizing Machine Learning

## Table of contents
   * [Overview](#Overview)
   * [Architectural Diagram](#Architectural-Diagram)
   * [Key Steps](#Key-Steps)
   * [Screenshots](#Screenshots)
   * [Screen Recording](#Screen-Recording)
   * [Future improvements](#Future-improvements-and-suggestions)
   * [Dataset Citation](#Dataset-Citation)
   * [References](#References)

***


## Overview

In this project, I used Azure Machine Learning to configure a cloud-based machine learning production model, deploy it, and consume it. After that, I created, published, and consumed a pipeline. The whole procedure is explained in this README file and is demonstrated in a screencast video.

The dataset used can be obtained from [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and contains marketing data about individuals. The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict whether the client will subscribe a bank term deposit. The result of the prediction appears in _`column y`_ and it is either _`yes`_ or _`no`_.

***
## Architectural Diagram

The diagram below is a visualization of the flow of operations from start to finish:

![Architectural Diagram](img/Architectural_diagram.png?raw=true "Architectural Diagram") 


***
## Key Steps

*TODO*: Write a short discription of the key steps. Remeber to include all the screenshots required to demonstrate key steps. 

The key steps of the project are described below:

- **Authentication:**
This step was actually omitted since it could not be implemented in the lab space provided by Udacity, because I am not authorized to create a security principal. However, I am still mentioning it here as it is a crucial step if one uses their own Azure account but, obviously, I am not including a screenshot.

- **Automated ML Experiment:**
At this point, security is enabled and authentication is completed. This step involves the creation of an experiment using Automated ML, configuring a compute cluster, and using that cluster to run the experiment.

- **Deploy the Best Model:**
After the completion of the experiment run, a summary of all the models and their metrics are shown, including explanations. The _Best Model_ will appear in the _Details_ tab, while it will appear first in the _Models_ tab. This is the model that should be selected for deployment. Its deployment allows to interact with the HTTP API service and interact with the model by sending data over POST requests.

- **Enable Logging:**
After the deployment of the Best Model, I enabled Application Insights and retrieve logs.

- **Swagger Documentation:**
This is the step where the deployed model will be consumed using Swagger. Azure provides a Swagger JSON file for deployed models. We can find the deployed model in the _Endpoints_ section, where it should be the first one on the list.

- **Consume Model Endpoints:**
Once the model is deployed, I am using the ```endpoint.py``` script to interact with the trained model. I run the script with the _scoring_uri_ that was generated after deployment and -since I enabled Authentication- the _key_ of the service. This URI is found in the _Details_ tab, above the Swagger URI.

- **Create and Publish a Pipeline:**
In this part of the project, I am using the Jupyter Notebook with the same keys, URI, dataset, cluster, and model names already created.

- **Documentation:**
The documentation includes: 1. the [screencast](YouTube-link) that shows the entire process of the working ML application; and 2. this README file that describes the project and documents the main steps.

***

## Screenshots

**Step 2: Automated ML Experiment**

![Step 2 required screenshots](img/Step2-required_screenshots.JPG?raw=true "Step 2 required screenshots")

**Step 4: Enable Application Insights**

![Step 4 required screenshots](img/Step4-required_screenshots.JPG?raw=true "Step 4 required screenshots")

**Step 5: Swagger Documentation**

![Step 5 required screenshots](img/Step5-required_screenshots.JPG?raw=true "Step 5 required screenshots")

**Step 6: Consume Model Endpoints**

![Step 6 required screenshots](img/Step6-required_screenshots.JPG?raw=true "Step 6 required screenshots")

**Step 7: Create, Publish and Consume a Pipeline**

![Step 7 required screenshots](img/Step7-required_screenshots.JPG?raw=true "Step 7 required screenshots")



***
## Screen Recording

The screen recording can be found [here](YouTube-link) and it shows the project in action. More specifically, the screencast demonstrates:

* The working deployed ML model endpoint
* The deployed Pipeline
* Available AutoML Model
* Successful API requests to the endpoint with a JSON payload


***
## Future improvements and suggestions

* As I have pointed out in the 1st project as well, the data is **highly imbalanced**:

![Highly imbalanced data](img/Imbalanced_data_plot.png?raw=true "Highly imbalanced data")

Although AutoML normally takes into account this imbalance automatically, there should be more room to improve the model's accuracy in predicting the minority class. For example, we could use Random Under-Sampling of majority class, or Random Over-Sampling of minority class, or even try different algorithms.

* Another factor that could improve the model is increasing the training time. This suggestion might be seen as a no-brainer, but it would also increase costs and there must always be a balance between minimum required accuracy and assigned budget.

* I could not help but wonder how more accurate would be the resulting model in case Deep Learning was used, as we were specifically instructed _NOT_ to enable it in the AutoML settings. While searching for more info, I found this very interesting article in Microsoft Docs: [Deep learning vs. machine learning in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-deep-learning-vs-machine-learning). There is says that deep learning excels at identifying patterns in unstructured data such as images, sound, video, and text. In my understanding, it might be an overkill to use it in a classification problem like this.

* Lastly, a thing that could be taken into account is any future change(s) in the dataset that could impact the accuracy of the model. I do not have any experience on how this could be done in an automated way, but I am sure that a method exists and can be spotted if/when such a need arises.

***
## Dataset Citation

[Moro et al., 2014] S. Moro, P. Cortez and P. Rita. A Data-Driven Approach to Predict the Success of Bank Telemarketing. Decision Support Systems, Elsevier, 62:22-31, June 2014.

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
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-consume-web-service?tabs=python)
- [Deep learning vs. machine learning in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-deep-learning-vs-machine-learning)

