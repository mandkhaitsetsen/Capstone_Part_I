# Capstone_Part_I
Capstone Project - Part 1 for the Professional Certificate for Machine Learning by HAAS Business School


The purpose of this exercise is to examine and predict the most important factors prospective MBA applicants should consider when applying for top business schools in the United States. Every year thousands of people take the Graduate Management Admissions Test (GMAT) in hopes of getting spots in extremely competitive and prestigious business schools around the world. In 2024, nearly 80,000 unique applicants took the GMAT test. The most reputable MBA Curriculum ranking is published by the U.S. News, which weighs average class GMAT scores in its ranking calculations. Which puts pressure on admission directors to over-index the scores in admission decisions. It is a very common knowledge for aspiring MBA candidates to beat 700 scores in the GMAT to secure a spot in the most prestigious schools. There is also a known secret in the industry that men have to score far above 700 in the GMAT while women would be in the sweet spot if she is near the 700 mark. 

However, admissions officers in these institutions encourage candidates to apply because they say the GMAT score represents only a part of their "holistic view" of each candidate. This project examines how "holistic" admissions officers' decisions actually are. Admissions officers safeguard their applicants' information and the data is hard to find in the public domain, especially from top business schools. Synthetic data generated from the Wharton Class of 2025's statistics was published on Kaggle.com. 
https://www.kaggle.com/datasets/taweilo/mba-admission-dataset

Wharton, Harvard, and Stanford are considered to be the top three business schools in the world. This synthetic set closely resembles the statistics of the real student profile of Wharton Business School's Class of 2025 are publicly available in the following link below.
https://admitstreet.com/blog/wharton-mba/

Metrics that match the synthetic data vs. Wharton's published data:
•	Number of applicants: 6,194
•	Women: 50%
•	International Students: 31%
•	% Composure to previous work industry
There are a couple of discrepancies between the synthetic data set vs. the real Wharton School published data:
•	Admitted students' average GMAT was 728, while it was 693 for the synthetic dataset. 
•	Admitted students' average undergrad GPA was published as 3.6, while it was 3.4 for the synthetic dataset.
•	Slightly lower percentage of STEM students (33% vs 30% of total admitted students) in the synthetic dataset. 

I believe that the synthetic data is the real data of all the applicants at Wharton. However, the admissions decisions columns were scrambled to safeguard the real data. 
My project first examines correlations of applicants' features with a seaborn pair plot. Not surprisingly, those who were admitted had higher average GMAT scores than the overall applicant pool. Gender also showed an imbalance since 50% of the admitted students were female when they only made up 36% of the total applicant pool. Blacks (8.7%) and Hispanics (10.4%) also seem to be admitted at a lower rate than the average of other racial groups(16.2%). 

I tested four predictive models, Decision Tree, Logistic Regression, K-N Neighbors, and Support Vector Classifier. I initially ran them as a simple model without any arguments, then tried to improve their performances by adding GridSearchCV on each. All of the models showed tremendous improvement with GridSearchCV. The ROC curve for both simple and improved models is shown below. 
 

  <img width="560" alt="Screen Shot 2024-11-20 at 3 42 14 PM" src="https://github.com/user-attachments/assets/bf157094-14dc-4020-8071-d3aba0d0cb60">

 <img width="560" alt="Screen Shot 2024-11-20 at 3 44 48 PM" src="https://github.com/user-attachments/assets/34e0a2a5-b391-4fca-a5a5-0c71a3378dd7">


I also created a confusion matrix of each of the models to determine which model was appropriate. The performance of each model is shown in the table below.


                   Fit Time  Accuracy Score  Precision Score  Recall Score
Model                                                                       
Decision Tree        1.876318        0.852338         0.000000      0.000000
LogisticRegression  15.171215        0.844955         0.434783      0.166667
KNN                 19.768619        0.853979         0.527778      0.105556
SVC                  7.410734        0.855619         0.576923      0.083333


I decided that the Logistic Regression Model was the best and the most reliable choice given its high recall score, even though it took much larger computing resources. Decision Tree was the least usable model in the scenario. 

I also created a Ridge model to see which features were most important. The results show that GMAT scores followed by gender were the most important feature of the successful applicants, confirming the industry-wide suspicion.

Feature	                  Coefficient 
GMAT Score	               0.105394
Gender	                   -0.044487
Undergraduate GPA	        0.043777
Application ID	          -0.036945
Race	                    0.013942
Work Industry	            -0.002617
Work Experience in years	0.002532
Undergraduate Major	      -0.001315


The project also predicts the chances of admission for applicants who were waitlisted. The Logistic regression model predicts that 25 of the 100 waitlisted students will be admitted. Given the model’s confusion matrix, those who would be admitted might be higher. However, we should note that Wharton Class of 2025 had an enrollment of 874 while the synthetic dataset marked 900 applicants as admitted and another 100 applicants as waitlisted. Therefore, I believe a much smaller number of waitlisted applicants were eventually admitted.
