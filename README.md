# Titanic-Kaggle

Understanding given datasets (train.csv & test.csv)

Missing values

	- Train.csv
		: Age 177, Cabin : 687, Embarked : 2
	- Test.csv
		: Age : 86, Fare : 1, Cabin : 327

Find tendencies in dataset

	- Pclass ( train[ [ 'Pclass', ‘Survived' ] ].groupby( [ ‘Pclass' ], as_index = False ).mean( ) )

		: If Pclass == 1 : 62% survival rate
		: If Pclass == 2 : 47% survival rate
		: If Pclass == 3 : 24% survival rate

	- Sex ( train[ [ 'Sex', ‘Survived' ] ].groupby( [ ‘Sex' ], as_index = False ).mean( ) )
		: If Sex == ‘female’ : 70% survival rate
		: If Sex == ‘male’ : 18% survival rate

	- Embarked
		: If Embarked == ‘C’ : 55% survival rate
		: If Embarked == ‘Q’ : 38% survival rate
		: If Embarked == ’S’ : 33% survival rate
	
Feature Engineering

	- SibSp & Parch : Add a new column that contains information of family size which is a summed value of SibSp, Parch, and the ticket holder(self).
		: If FamilySize == 1 : 30% survival rate
		: If FamilySize == 2 : 55% survival rate … and so on. 
		So does having family members affect one’s survival? To find out, create another feature to see if the ticket holder is traveling alone or not.
		: If Alone == 0 : 50% survival rate
		: If Alone == 1 : 30% survival rate. So there’s 50% chance of surviving if you are alone, while 30% of those who have family survived.

	- Embarked : Since 70% of the people embarked from ’S’, fill missing values with ’S’.

	- Fare : Data of fare is missing in test.csv. So fill the missing values by median of group ‘Pclass’. If we divide ‘Fare’ into 4 groups that contain the same amount of datas, the range is same as below.
		: (-0.001, 7.91], (7.91, 14.454], (14.454, 31.0], (31.0, 512.329]

	- Age
		: First extract ‘title’ information from train[‘Name’], then fill in the missing datas of age with median values grouped by ‘title’. If we divide ‘Age’ into 5 groups that contain the same amount of datas, the range is same as below.
		: (0.419, 20.0], (20.0, 26.0], (26.0, 30.0], (30.0, 38.0], (38.0, 80]

Data Cleansing : Transforming categorical value into numerical values.

	- sexMap = {‘male’ : 0, ‘female’ : 1}
	- embarkedMap = {’S’ : 0, ‘C’ : 1, ‘Q’ : 2}
	- titleMap = {"Mr" : 0, "Miss" : 1, "Mrs" : 2, "Master" : 3, …. : 3}
	- Fare : 0 ~ 3
	- Age : 0 ~ 4
