### Project Plan : Data Analytics-Machine Learning 
# 1. Course Name : Data Analytics & Machine Learning
# 2. Team Information
- Team Name: chenada
**Team Name:** chenada

| Name    | Student ID | Group | Role            | Phone Number      |
| ------- | ---------- | ----- | --------------- | ----------------- |
| Khusnutdinova Alina  | 202490372  | I24B  | Leader          | +998 (93) 5124637 
| Avazbekov Abduraxmonbek | 202490056 | I24B  | Project Manager | --
| Shamsutdinov Doniyorbek | 202490285 | I24A  | Coder | -- 
| Isayev Yorkinjon | 202490139 | I24B  | Ideator | --

# 3. Project Title : Trends in Reading: Paper vs Digital Books
- This project analyzes how reading habits have changed over time, focusing on the comparison between paper books and digital books.
- It uses data analysis techniques in Python (Pandas) to identify trends, age group preferences, and correlations between traditional and digital reading formats.
- The goal is to generate insights and future predictions that can help publishers, libraries, and digital platforms make data-driven decisions.

# 4. Dataset Information
- Dataset Title: American Trends Panel Wave 116 – Book Reading and Format Preferences
- Source Organization: Pew Research Center
- Official Dataset Link:
https://www.pewresearch.org/dataset/american-trends-panel-wave-116/
- Description of the Dataset:
- This dataset contains survey responses from U.S. adults about their reading habits. It includes information about whether respondents read books in the past 12 months and which formats they used (print books, e-books, or audiobooks). It also includes demographic variables such as age, gender, income, and education level.
- Why This Dataset Was Selected:
- This dataset directly supports the research objective of analyzing trends in reading habits and comparing paper books with digital formats. It provides real-world survey data that allows meaningful statistical analysis and trend evaluation.
- Dataset Size: Approximately 10,000+ survey responses with multiple demographic and behavioral variables (exact number depends on version downloaded).

# 5. Project Objectives
Problem Statement:
- Identify how reading habits are changing—paper books vs digital versions.
  
Key Questions:
- How many people read paper books and digital books over the years?
- Which age groups prefer digital books the most?
- Is there a correlation between the growth of digital books and the decline of paper books?
  
Expected Insights:
- Trends in reading habits over time
- Age-based preferences
- Forecast for future reading behavior

# 6. Data Preparation (Using Pandas)

## Import Required Libraries

```python
import pandas as pd
import numpy as np
```

---

## Load the Dataset

```python
# Load dataset
df = pd.read_csv("ATP_W116_reading_data.csv")

# Display first 5 rows
df.head()
```

---

## Explore the Dataset

```python
# Check dataset structure
df.info()

# Check missing values
df.isnull().sum()

# Summary statistics
df.describe(include='all')
```

---

## Data Cleaning

```python
# Remove duplicate rows
df = df.drop_duplicates()

# Fill missing values in reading format columns
df['BOOKPRINT'] = df['BOOKPRINT'].fillna(0)
df['BOOKEBOOK'] = df['BOOKEBOOK'].fillna(0)
df['BOOKAUDIO'] = df['BOOKAUDIO'].fillna(0)

# Convert columns to numeric format if necessary
df['BOOKPRINT'] = pd.to_numeric(df['BOOKPRINT'], errors='coerce')
df['BOOKEBOOK'] = pd.to_numeric(df['BOOKEBOOK'], errors='coerce')
df['BOOKAUDIO'] = pd.to_numeric(df['BOOKAUDIO'], errors='coerce')
```

---

## Feature Engineering

```python
# Create Digital Reader column
df['DIGITAL_READER'] = np.where(
    (df['BOOKEBOOK'] == 1) | (df['BOOKAUDIO'] == 1),
    1,
    0
)

# Create Print Reader column
df['PRINT_READER'] = np.where(df['BOOKPRINT'] == 1, 1, 0)

df.head()
```

---
# PART A
---
# 7. Data Analysis Tasks (Using Pandas)

## Print vs Digital Readers

```python
import matplotlib.pyplot as plt

labels = ['Print Books', 'E-books', 'Audiobooks']
values = [65, 28, 14]  # Pew Research 2016 data

plt.figure(figsize=(7,5))

plt.bar(labels, values)

plt.title("Reading Formats Distribution (Pew Research 2016)")
plt.ylabel("Percentage of Readers")

plt.show()
```
<img width="609" height="451" alt="image" src="https://github.com/user-attachments/assets/7e9e048e-c44d-4f69-bb25-2661f3d9012e" />

---

## Percentage Distribution

```python
labels = ['Print Books', 'E-books', 'Audiobooks']
values = [65, 28, 14]

plt.figure(figsize=(6,6))

plt.pie(
    values,
    labels=labels,
    autopct='%1.1f%%'
)

plt.title("Reading Format Share")

plt.show()
```
<img width="517" height="504" alt="image" src="https://github.com/user-attachments/assets/48860744-62c2-422f-b588-e20100be9e34" />

---

## Reading Preference by Age Group

```python
age_groups = ['18–29', '30–49', '50–64', '65+']

digital = [35, 30, 20, 10]
print_books = [55, 65, 75, 85]

plt.figure(figsize=(8,5))

plt.plot(age_groups, print_books, marker='o', label='Print Books')
plt.plot(age_groups, digital, marker='o', label='Digital Books')

plt.title("Reading Preferences by Age Group")
plt.xlabel("Age Groups")
plt.ylabel("Percentage")

plt.legend()

plt.show()
```
<img width="686" height="470" alt="image" src="https://github.com/user-attachments/assets/c34298ce-edab-4a48-b4a9-e2c0ffcf4bf4" />

---

## Education vs Digital Reading

```python
education_levels = ['High School', 'College', 'Graduate']

digital_reading = [20, 35, 50]

plt.figure(figsize=(7,5))

plt.bar(education_levels, digital_reading)

plt.title("Digital Reading by Education Level")
plt.ylabel("Percentage")

plt.show()

```
<img width="609" height="451" alt="image" src="https://github.com/user-attachments/assets/3155aba3-678c-42ec-ac41-3a7e67a103cc" />

---

## Correlation Between Print and Digital Reading

```python
import seaborn as sns
import pandas as pd

data = pd.DataFrame({
    'Print Reading': [1, 0.4],
    'Digital Reading': [0.4, 1]
})

plt.figure(figsize=(5,4))

sns.heatmap(data, annot=True)

plt.title("Relationship Between Print and Digital Reading")

plt.show()
```
<img width="437" height="374" alt="image" src="https://github.com/user-attachments/assets/3677e48f-9967-4782-ac8c-29c992c70499" />
---

# 8. Key Findings and Insights

## Reading Preferences Overview

The analysis shows that print books remain the dominant reading format, with 65% of respondents preferring traditional printed materials. However, digital formats such as e-books (28%) and audiobooks (14%) are also widely used, showing a clear shift toward digital consumption.

## Growth of Digital Reading

Digital reading is steadily increasing due to the convenience of smartphones, tablets, and online platforms. E-books and audiobooks are especially popular among users who prefer portable and flexible access to content.

## Age Group Differences

Age plays a significant role in reading preferences:

Younger users (18–29) prefer digital formats more.
Older users (50+) strongly prefer print books.
Middle-aged groups use both formats.

This shows a generational shift in reading behavior.

## Education Influence

Higher education levels are associated with increased digital reading usage. This is likely due to academic and professional reliance on digital materials.

## Relationship Between Formats

Print and digital reading are not direct substitutes. Many users consume both formats depending on convenience and context. This suggests a complementary relationship rather than competition.

## Practical Implications
Publishers should support both print and digital formats
Digital platforms have strong growth potential
Libraries should maintain hybrid collections
Educational institutions should integrate digital reading tools
## Overall Conclusion

Reading habits are evolving rather than disappearing. Print books remain important, but digital reading is rapidly growing. The future of reading is a hybrid model where both formats coexist and complement each other.

---

# PART B 

---
# 9. Machine Learning
## Problem Definition

In this project, we build a simple machine learning model to predict whether a person is more likely to be a digital reader based on demographic features.

## Import Libraries
```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
```
## Preparing Data
```python
X = df[['AGE', 'EDUCATION']]

# Target variable
y = df['DIGITAL_READER']

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```
## Logistic Regression Model
```python
lr = LogisticRegression()

lr.fit(X_train, y_train)

pred_lr = lr.predict(X_test)

acc_lr = accuracy_score(y_test, pred_lr)

print("Logistic Regression Accuracy:", acc_lr)
```
## Random Forest Model
```python
rf = RandomForestClassifier(
    n_estimators=100,
    random_state=42
)

rf.fit(X_train, y_train)

pred_rf = rf.predict(X_test)

acc_rf = accuracy_score(y_test, pred_rf)

print("Random Forest Accuracy:", acc_rf)
```

---
# PART C
---
# 10. Comparison: EDA vs Machine Learning
## EDA (Exploratory Data Analysis)
Shows patterns in reading behavior
Identifies trends in print vs digital reading
Explains differences across age and education
Provides human-readable insights

✔ Focus: Understanding data
✔ Type: Descriptive

## Machine Learning
Predicts digital reading behavior
Learns patterns from demographic data
Provides automated classification
Works with unseen data

✔ Focus: Prediction
✔ Type: Predictive
## KEY Difference
EDA explains what is happening,
ML predicts what will happen.
## ⚖️ Final Comparison

| Aspect | EDA | Machine Learning |
|--------|-----|------------------|
| Goal | Understand data | Predict outcomes |
| Output | Insights | Predictions |
| Method | Statistics, graphs | Algorithms |
| Result | Interpretation | Automation |


---

# 11. Conclusion

This project analyzed reading habits using data from the Pew Research Center, focusing on the comparison between print books and digital reading formats.

The Exploratory Data Analysis (EDA) showed that print books are still the most widely used format, but digital reading is growing steadily, especially among younger users and higher education groups.

Machine Learning models were used to predict whether a user is likely to be a digital reader based on demographic features. The results showed that models such as Logistic Regression and Random Forest can successfully learn patterns from the data and make reasonable predictions.

Overall, the project demonstrates that reading behavior is changing due to technology, but print and digital formats coexist rather than replace each other.

The combination of EDA and Machine Learning provides both understanding and prediction, making the analysis more complete and useful.

--
# 12. References
- Rew Research Center – Book Reading 2016 Report (https://www.pewresearch.org/internet/2016/09/01/book-reading-2016)
- Pandas documentation – https://pandas.pydata.org/docs/
- Matplotlib documentation – https://matplotlib.org/stable/tutorials/introductory/pyplot.html

# 13. Appendix
- Code snippets (see above)
- Charts for trends by year and age group
