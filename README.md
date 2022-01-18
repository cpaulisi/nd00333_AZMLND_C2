<img align="right" width="100" height="100" src="https://visualstudiomagazine.com/articles/2021/05/18/~/media/ECG/visualstudiomagazine/Images/2021/05/new_azure_a.ashx">

# Udacity Azure MLOps Project 2
[View the screencast here.](https://youtu.be/Xx2r0VRO3e4)

## Overview

 This objective of this project was to practice the consumption and generation of models, and model pipelines, using the AutoML and Pipeline features provided by Azure ML Studio. Using a variety of consumption tools, the endpoints created by this project were verified, benchmarked, and set on a schedule.

## Architecture

![Screen Shot 2022-01-15 at 3 10 38 PM](https://user-images.githubusercontent.com/87383001/149636325-8b028354-3a35-4aed-8053-bfee377b2e8d.png)

## Improvements

 As a continuation of the project's development, changing which models are trained and how the endpoint is consumed could lead to improvements. By specifying a smaller subset of models (narrowed down from the best-performing models demostrated by AutoML), classification performance under all metrics could improve. Automation likewise could be aided by establishing a CRON job that periodically runs the model on new input data, and aggregates this output on some storage.

## Project Walkthrough

### Data

  First, the bank marketing data was uploaded to the registered datasets. The dataset allows for the training of classification models using customer data to infer their reaction to engagement efforts.

<img width="1439" alt="Screen Shot 2022-01-13 at 8 02 23 PM" src="https://user-images.githubusercontent.com/87383001/149636456-1488d28b-8960-4f06-b281-0db78d9aa362.png">
<img width="1414" alt="Screen Shot 2022-01-13 at 8 02 56 PM" src="https://user-images.githubusercontent.com/87383001/149636463-802f1f5b-a5f5-4827-9075-2b26c5000e12.png">

### AutoML Run

  An AutoML run was then completed, and the best performing model was selected. The computer cluster details for this run allocated a CPU cluster of configuration Standard_DS12_v2, with a minimum of 1 node. The exit criteria was specified as a 1-hour exit, and a concurrency of 5 processes. This allows for the AutoML run to find the optimal model in the fastest, yet most efficient, way possible.

<img width="1431" alt="Screen Shot 2022-01-13 at 10 39 40 PM" src="https://user-images.githubusercontent.com/87383001/149636492-3799eae6-8ec5-4ecf-9df6-a1706a956036.png">
<img width="1426" alt="Screen Shot 2022-01-13 at 10 40 32 PM" src="https://user-images.githubusercontent.com/87383001/149636514-4d2564b3-4cb7-4c63-8fff-f12af317afb4.png">

### Sample Deployment

  After that, the model was set for deployment. Authentication was enabled for the deployment, and the model was deployed using an Azure Container Instance for portability. By default, application insight are disabled within the container instance. The logs.py file allowed us to enable applications insights, after which  logs were generated tested.

<img width="1428" alt="Screen Shot 2022-01-13 at 10 47 55 PM" src="https://user-images.githubusercontent.com/87383001/149636544-e01fd4f1-1c30-4a1b-9898-488639ec9c61.png">
<img width="1249" alt="Screen Shot 2022-01-13 at 10 51 59 PM" src="https://user-images.githubusercontent.com/87383001/149636545-9a50ab52-7250-4a08-9fba-7654b0cd41d9.png">

### Swagger

  Swagger was then used to view the contents and documentation for the model, along with API methods and responses. The pedantics of HTTP request methods, including POST and GET, were outlined in the Swagger UI. The serve.py script and swagger.sh scripts, along with a swagger.json file downloaded from Azure, were used to construct and view the UI, which was ported to a localhost.

![Screen Shot 2022-01-15 at 2 21 11 PM](https://user-images.githubusercontent.com/87383001/149636579-ef9f6f54-f797-4493-9842-50ce19cc0338.png)
<img width="1427" alt="Screen Shot 2022-01-13 at 11 00 52 PM" src="https://user-images.githubusercontent.com/87383001/149636582-a03ab632-30f2-456e-a592-5ea05984f5be.png">
<img width="1424" alt="Screen Shot 2022-01-13 at 11 01 05 PM" src="https://user-images.githubusercontent.com/87383001/149636583-45511541-385f-4f01-8b17-e12bcf00ba60.png">
<img width="1421" alt="Screen Shot 2022-01-13 at 11 01 14 PM" src="https://user-images.githubusercontent.com/87383001/149636585-c8880bb2-d77b-4a81-80b5-f7180357508f.png">
<img width="1422" alt="Screen Shot 2022-01-13 at 11 01 21 PM" src="https://user-images.githubusercontent.com/87383001/149636586-00d938ff-f193-4e2b-931e-5c6ef06e8de1.png">

### Model Consumption

  The model was tested for consumption and benchmarked using sample input payload. A python script, endpoint.py, is used to create sample input data in .json form, and then queries the deployed webservice for classification. As shown below, the response recieved in commensurate with the expected output of a classification web service. The benchmark.sh script uses Apache Benchmark command line interface to test the speed and error coding of the deployment.

![Screen Shot 2022-01-15 at 1 48 35 PM](https://user-images.githubusercontent.com/87383001/149636627-2f98ff46-f16c-434a-81bb-79edd00d81e8.png)

![Screen Shot 2022-01-15 at 1 55 53 PM](https://user-images.githubusercontent.com/87383001/149636611-e5090062-4f01-40f6-a96f-3cb8a748f221.png)

![Screen Shot 2022-01-15 at 1 54 16 PM](https://user-images.githubusercontent.com/87383001/149636631-51a46dcc-4fe9-407d-817c-303ac58813df.png)

![Screen Shot 2022-01-15 at 1 54 46 PM](https://user-images.githubusercontent.com/87383001/149636636-4fc0c2dc-539f-4d6d-80aa-df64f846f9ab.png)

### Pipeline Publication

  A pipeline was established using the sample notebook provided. The provided configuration file (config.json) from Azure allows for environemnt and workspace details to become automatically accessible. Marketing data is accessed via the workspace details in the configuration file. The notebook runs on a compute instance, creates an AutoML run using a cluster as a compute target, and provided information on the run and the subsequent models that are made available through it. It automatically selects the best peforming model, saves it, and publishes a pipeline with that model in deployment. The publication of the pipeline creates a pipeline endpoint with which to access the model. The REST endpoint can be confirmed by viewing the Publish Pipeline overview and checking the endpoint for a status of "Active". Insights on the run progress and logging are provided through a number of widgets, including RunDetails and confusion_matrix. The pipeline can also be scheduled to run every 4 hours, automating the process even further.

<img width="1312" alt="Screen Shot 2022-01-13 at 9 11 56 PM" src="https://user-images.githubusercontent.com/87383001/149636673-0189cba4-2388-4293-9fad-3715863792f4.png">

![Screen Shot 2022-01-15 at 2 15 49 PM](https://user-images.githubusercontent.com/87383001/149636814-6b805c4c-eb1f-4e4d-ac52-69ab63d79aa1.png)

![Screen Shot 2022-01-15 at 1 59 48 PM](https://user-images.githubusercontent.com/87383001/149636718-6e0d80eb-a920-4996-985a-f0be6990644d.png)

<img width="1124" alt="Screen Shot 2022-01-13 at 9 43 59 PM" src="https://user-images.githubusercontent.com/87383001/149636728-6d40d287-0c79-4b71-96cf-fd8821a61428.png">

![Screen Shot 2022-01-15 at 2 05 22 PM](https://user-images.githubusercontent.com/87383001/149636744-b0fb3ec1-f31d-4faf-9e09-b8eae4bc420a.png)

  The RunDetails widget output sample is shown below. Logging and activity for the run are provided as output.

![Screen Shot 2022-01-15 at 1 50 07 PM](https://user-images.githubusercontent.com/87383001/149636761-ed856410-3196-4cf1-b033-a296361136b5.png)

![Screen Shot 2022-01-15 at 1 50 15 PM](https://user-images.githubusercontent.com/87383001/149636766-d361a4cf-a937-440d-97b2-b09ac6a84795.png)

  The pipeline was set on a regular schedule. Automation of this process occurs every 4 hours.

![Screen Shot 2022-01-15 at 2 13 54 PM](https://user-images.githubusercontent.com/87383001/149636799-bf679826-7b90-453d-970f-b9d1c9a711a5.png)

![Screen Shot 2022-01-15 at 2 13 41 PM](https://user-images.githubusercontent.com/87383001/149636817-d929a571-0831-4c04-abb6-3bc777377057.png)

