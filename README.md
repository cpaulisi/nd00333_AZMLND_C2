# Udacity Azure MLOps Project 2

## Overview

This objective of this project was to practice the consumption and generation of models, and model pipelines, using the AutoML and Pipeline features provided by Azure ML Studio. Using a variety of consumption tools, the endpoints created by this project were verified, benchmarked, and set on a schedule.

## Architecture

![Screen Shot 2022-01-15 at 3 10 38 PM](https://user-images.githubusercontent.com/87383001/149636325-8b028354-3a35-4aed-8053-bfee377b2e8d.png)

## Improvments

As a continuation of the project's development, changing which models are trained and how the endpoint is consumed could lead to improvements. By specifying a smaller subset of models (narrowed down from the best-performing models demostrated by AutoML), classification performance under all metrics could improve. Automation likewise could be aided by establishing a CRON job that periodically runs the model on new input data, and aggregates this output on some storage.

## Screenshots

First, the bank marketing data was uploaded to the registered datasets.

<img width="1439" alt="Screen Shot 2022-01-13 at 8 02 23 PM" src="https://user-images.githubusercontent.com/87383001/149636456-1488d28b-8960-4f06-b281-0db78d9aa362.png">
<img width="1414" alt="Screen Shot 2022-01-13 at 8 02 56 PM" src="https://user-images.githubusercontent.com/87383001/149636463-802f1f5b-a5f5-4827-9075-2b26c5000e12.png">

Then the AutoML run was completed and the best performing model was selected.

<img width="1431" alt="Screen Shot 2022-01-13 at 10 39 40 PM" src="https://user-images.githubusercontent.com/87383001/149636492-3799eae6-8ec5-4ecf-9df6-a1706a956036.png">
<img width="1426" alt="Screen Shot 2022-01-13 at 10 40 32 PM" src="https://user-images.githubusercontent.com/87383001/149636514-4d2564b3-4cb7-4c63-8fff-f12af317afb4.png">
