# Operationalizing Machine Learning

## Table of contents
   * [Overview](#Overview)
   * [Architectural Diagram](#Architectural-Diagram)
   * [Key Steps](#Key-Steps)
   * [Screenshots](#Screenshots)
   * [Screen Recording](#Screen-Recording)
   * [Comments and future improvements](#Comments-and-future-improvements)
   * [Dataset Citation](#Dataset-Citation)
   * [References](#References)

***


## Overview

In this project, I used Azure Machine Learning to configure a cloud-based machine learning production model, deploy it, and consume it. After that, I created, published, and consumed a pipeline. The whole procedure is explained in this README file and is demonstrated in a screencast video.

The dataset used can be obtained from [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and contains marketing data about individuals. The data is related with direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict whether the client will subscribe a bank term deposit. The result of the prediction appears in _`column y`_ and it is either _`yes`_ or _`no`_.

***
## Architectural Diagram

The architectural diagram is not very detailed by nature; its purpose is to give a rough overview of the operations. The diagram below is a visualization of the flow of operations from start to finish:

![Architectural Diagram](img/Architectural_diagram.png?raw=true "Architectural Diagram") 
  

***
## Key Steps


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

_Required screenshots:_

![Step 2 required screenshots](img/Step2-required_screenshots.JPG?raw=true "Step 2 required screenshots")

_Taken screenshots:_

**1) Registered Datasets**

![Registered Datasets](img/01.JPG?raw=true "Registered Datasets")

![Registered Datasets](img/47.JPG?raw=true "Registered Datasets")

Creating a new Automated ML run 

![Experiment is completed](img/02.JPG?raw=true "Experiment is completed")

**2) Experiment is completed**

![AutoML completed](img/AutoML_Completed.JPG?raw=true "AutoML completed")

![Experiment is completed](img/03.JPG?raw=true "Experiment is completed")

Data guardrails

![Data guardrails](img/04.JPG?raw=true "Data guardrails")

![Data guardrails  - additional details](img/05.JPG?raw=true "Data guardrails - additional details")

**3) Best model**

![Best model](img/06.JPG?raw=true "Best model")

![Best model](img/07.JPG?raw=true "Best model")

![Best model graphs](img/08.JPG?raw=true "Best model graphs")

![Best model metrics](img/Best_model2_metrics.JPG?raw=true "Best model metrics")

Best model deployment


![Best model deployment](img/10.JPG?raw=true "Best model deployment - Start")

![Best model deployment](img/11.JPG?raw=true "Best model deployment - Success")

![Best model deployment](img/12.JPG?raw=true "Best model deployment - Logs")

![Best model - Consume tab](img/13.JPG?raw=true "Best model - Consume tab")

**Step 4: Enable Application Insights**

_Required screenshots:_

![Step 4 required screenshots](img/Step4-required_screenshots.JPG?raw=true "Step 4 required screenshots")

_Taken screenshots:_

**1) "Application Insights" enabled in the Details tab of the endpoint**

!["Application Insights" enabled](img/Best_model2_Application_Insights_enabled.JPG?raw=true "'Application Insights' enabled")

Screenshot of the tab running "Application Insights":

!["Application Insights" graphs](img/Best_model2_Application_Insights_tab.JPG?raw=true "'Application Insights' graphs")

We can see Failed requests, Server response time, Server requests & Availability graphs in real time.


**2) Running logs.py script**

![Running logs.py script](img/Best_model2-logs_py_running.JPG?raw=true "Running logs.py script")


**Step 5: Swagger Documentation**

_Required screenshots:_

![Step 5 required screenshots](img/Step5-required_screenshots.JPG?raw=true "Step 5 required screenshots")

_Taken screenshots:_

**1) Swagger runs on localhost - GET & POST/score endpoints**

![swagger.sh run](img/best_model2-Swagger1B.JPG?raw=true "swagger.sh run")

![swagger.sh run](img/best_model2-Swagger1A.JPG?raw=true "swagger.sh run")

![Swagger runs on localhost](img/61.JPG?raw=true "Swagger runs on localhost")

![Swagger runs on localhost](img/best_model2-Swagger1.JPG?raw=true "Swagger runs on localhost")

![Swagger runs on localhost - GET endpoint](img/best_model2-Swagger2.JPG?raw=true "Swagger runs on localhost - GET endpoint")

![Swagger runs on localhost - POST/score endpoint](img/best_model2-Swagger3.JPG?raw=true "Swagger runs on localhost - POST/score endpoint")


**Step 6: Consume Model Endpoints**

_Required screenshots:_

![Step 6 required screenshots](img/Step6-required_screenshots.JPG?raw=true "Step 6 required screenshots")

_Taken screenshots:_

**1) Consume Model Endpoints: endpoint.py runs**

![endpoint.py](img/best_model2_enpoint_py.JPG?raw=true "endpoint.py")

![endpoint.py runs](img/best_model2_enpoint_py_run.JPG?raw=true "endpoint.py runs")

**Step 7: Create, Publish and Consume a Pipeline**

_Required screenshots:_

![Step 7 required screenshots](img/Step7-required_screenshots.JPG?raw=true "Step 7 required screenshots")

_Taken screenshots:_

**1+2) The Pipelines section of Azure ML Studio**

![Pipeline has been created](img/Pipeline_has_been_created.JPG?raw=true "Pipeline has been created")

![Pipeline Endpoint](img/Pipeline_Endpoint.JPG?raw=true "Pipeline Endpoint")

**3) Bankmarketing dataset with the AutoML module** 

![Bankmarketing dataset with the AutoML module](img/Bankmarketing_Dataset+AutoML_module.JPG?raw=true "Bankmarketing dataset with the AutoML module")

**4) Published Pipeline Overview showing a REST endpoint and an ACTIVE status** 

![Published Pipeline Overview showing a REST endpoint and an ACTIVE status](img/41.JPG?raw=true "Published Pipeline Overview showing a REST endpoint and an ACTIVE status")

![Published Pipeline Overview showing a REST endpoint and an ACTIVE status](img/42.JPG?raw=true "Published Pipeline Overview showing a REST endpoint and an ACTIVE status")

**5) Jupyter Notebook: RunDetails Widget shows the step runs** 

![Jupyter Notebook: RunDetails Widget shows the step runs](img/RunDetailsWidget1.JPG?raw=true "Jupyter Notebook: RunDetails Widget shows the step runs")

![Jupyter Notebook: RunDetails Widget shows the step runs](img/RunDetailsWidget2.JPG?raw=true "Jupyter Notebook: RunDetails Widget shows the step runs")

**6) In ML Studio: Completed run** 

![In ML Studio](img/40.JPG?raw=true "In ML Studio")

![In ML Studio](img/50.JPG?raw=true "In ML Studio")

![In ML Studio](img/51.JPG?raw=true "In ML Studio")

**Extra Screenshots**

Although not explicitly asked, I am adding these here as a reference.

_Best model screenshots:_

![Best model](img/33.JPG?raw=true "Best model")

![Best model](img/34.JPG?raw=true "Best model")

![Best model](img/35.JPG?raw=true "Best model")

![Best model](img/36.JPG?raw=true "Best model")

![Best model](img/37.JPG?raw=true "Best model")

_"Data guardrails" tab screenshots:_

!['Data guardrails' tab](img/44.JPG?raw=true "'Data guardrails' tab")

!['Data guardrails' tab](img/45.JPG?raw=true "'Data guardrails' tab")

***
## Screen Recording

The screen recording can be found [here]() and it shows the project in action. More specifically, the screencast demonstrates:

* The working deployed ML model endpoint
* The deployed Pipeline
* Available AutoML Model
* Successful API requests to the endpoint with a JSON payload


***
## Comments and future improvements

* As I have pointed out in the 1st project as well, the data is **highly imbalanced**:

![Highly imbalanced data](img/Imbalanced_data_plot.png?raw=true "Highly imbalanced data")

Although AutoML normally takes into account this imbalance automatically, there should be more room to improve the model's accuracy in predicting the minority class. For example, we could use Random Under-Sampling of majority class, or Random Over-Sampling of minority class, or even try different algorithms.

A side note here: out of curiosity, I clicked the 'Data guardrails' tab (see screenshots above) and found many interesting observations done by Azure analysis. Unfortunately, I ran out of time and was not able to look into this with more detail. My remark here is that even though I can understand that there must be time contraints in our runs, this can impede our in depth learning because we miss the chance to browse around looking for the many extra but less important things; this is really a shame. As a suggestion, it would be interesting to create a virtual environment with everything running in simulation -thus running with no actual cost- where the learner could freely look around.

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
- [Dr. Ware: Dealing with Imbalanced Data in AutoML](https://www.drware.com/dealing-with-imbalanced-data-in-automl/)
- [Microsoft Tech Community: Dealing with Imbalanced Data in AutoML](https://techcommunity.microsoft.com/t5/azure-ai/dealing-with-imbalanced-data-in-automl/ba-p/1625043)
- A very interesting paper on the imbalanced classes issue: [Analysis of Imbalance Strategies Recommendation using a
Meta-Learning Approach](https://www.automl.org/wp-content/uploads/2020/07/AutoML_2020_paper_34.pdf)
- [Imbalanced Data : How to handle Imbalanced Classification Problems](https://www.analyticsvidhya.com/blog/2017/03/imbalanced-data-classification/)
- [Consume an Azure Machine Learning model deployed as a web service](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-consume-web-service?tabs=python)
- [Deep learning vs. machine learning in Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/concept-deep-learning-vs-machine-learning)

