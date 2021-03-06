# UFC Fight Predictor
###### A predictive model by Julia Cho, Kimberly Murphy, Daniel Urdaneta, and Adrian Zamora 

## Overview:
In this project, our goal is to create a machine learning model which can predict the winner of a UFC welterweight fight using historical fighter data.  We also hope to glean insight into the most successful fighter metrics such as stance and age. 

## [Group Presentation](https://docs.google.com/presentation/d/12g6ZuxoMSZnClPs9yp5jP-XTK2Ll4H4IA8F_h0Qpiwc/edit?usp=sharing)

## Machine Learning Models 
---
**The goal:**  Create a machine learning model which can predict which fighter will win in a given welterweight fight. We focused on the welterweight class, specifically, as it is among the largest division in terms of fighters and popularity over the years.  

**The dataset:**  The [Kaggle dataset](https://www.kaggle.com/rajeevw/ufcdata) we used contains fighter data from 1993-2021.  Each row is an individual fight with the fighter stats for both the blue and red fighter.

We approached this as a **supervised classification**—Will the winner be the red fighter, the blue fighter, or a draw?   With this idea in mind, we tested several different models including a Logistic regression, SVM, Random Forest, Gradient Boosted models.  From these the Gradient Boosted model generated the greatest accuracy.

[Preparing the data:](https://github.com/danielurdaneta/FinalProject/blob/e2fc10a1a8b80865a5743e9ff57515cdb10f4159/data_clean_926.ipynb) 
The original dataset was filtered using pandas to only include those fights classified within the welterweight division.  Any fights that had missing data or which were scheduled but did not happen were removed.  Additionally, any string data-- such as the Fighters’ Stance and the Winner of the fight – was converted to integers using LabelEncoder.  Finally, the data was manipulated in Excel to show the differences between the blue and red fighter in an individual fight. 
For example:
 
![image of calculation](https://github.com/danielurdaneta/FinalProject/blob/6ca8d8a994c6ae10f70699ddd2b265146d3dd6bd/Images/stance%20calculation.JPG)

[Building the Model:](https://github.com/danielurdaneta/FinalProject/blob/e2fc10a1a8b80865a5743e9ff57515cdb10f4159/Gradient_Boosted_Trees_Model_wk3_Final.ipynb)
The processed flat csv file was stored within postgres and accessed via SQLalchemy in the modeling.

![image of sqlalchemy](https://github.com/danielurdaneta/FinalProject/blob/884d36b024974074acd7e2a93eb230db089c9d74/Images/SQLAlchemy.JPG)

It was determined after many iterations that the following features were the most impactful and, therefore, included as the final *features(X):* 

 - Total time fought (16%)
 - Total rounds fought (12%)
 - Age(11%)
 - Current win streak (8%)
 - Weight (8%)
 - Total wins(7%)
 - Total losses(7%)
 - Reach (7%)
 - Total title bouts (4%)
 - Height(6%)
 - Stance(5%)
 - Current lose streak (4%)
 - Longest win streak(4%)

*Target(y):* Winner

The **sklearn library** was used to split the dataset such that 80% of the records were assigned to the training set and 20% assigned to the test set.  

**StandardScaler** was used to scale the data to reduce the chance of undue weight being applied to features with larger numbers (such as reach(cm) and total time fought) 

![image of split and scale](https://github.com/danielurdaneta/FinalProject/blob/884d36b024974074acd7e2a93eb230db089c9d74/Images/split%20and%20scale.JPG)

The model was trained using the **GradientBoostingClassifier**.  This model was chosen because each tree is built sequentially using the information from previous trees to build the next.  

**Model tuning:**  The following parameters were adjusted to optimize our model:

![image of model parameters](https://github.com/danielurdaneta/FinalProject/blob/de52beb00279168e6aa64b218980b549768ff931/Images/model%20tuning.JPG)

 
**Assessing the model:** A confusion matric, accuracy score, and classification report was generated using the sklearn library. 

![Image of the results](https://github.com/danielurdaneta/FinalProject/blob/216241c47569e91c64241c442cc01e3cf201a34f/Images/one_model%20accuracy.JPG)


## Dashboard 
---

The dashboard of this project will be a web application created using HTML, CSS, JavaScript and its library D3. The web app will consist of a description of the project, graphs created in the exploratory phase of the project, a table with fighters stats and the Machine Learning models. 

The user will be able to change the ML model using a drop off menu, and in this way to observe how we execute that specific model and the results we obtained, the user will also be able to select a fighter and see all his stats in a interactive table. Below we can see an image of the interactive elements of our web app:


![interactive elementes dashboard](https://user-images.githubusercontent.com/81272629/135006205-e9c9a780-0a93-49c1-b581-d61e4394924f.png)


You can follow the link to see our dashboard: https://danielurdaneta.github.io/FinalProject/







## Database

The below shows the relationship between the two tables creating the welterweight data used to perform the analysis
![ERD.JPG](https://github.com/danielurdaneta/FinalProject/blob/main/Images/ERD.JPG)


