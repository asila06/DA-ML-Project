### Project Plan : Data Analytics-Machine Learning ###<<
#1. Course Name : Data Analytics & Machine Learning
#2. Team Information
- Team Name: chenada
| Name    | Student ID | Group | Role            | Phone Number      |
| ------- | ---------- | ----- | --------------- | ----------------- |
| Khusnutdinova Alina  | 202490372  | I24B  | Leader          | +998 (93) 5124637 
| Avazbekov Abduraxmonbek | 202490056 | I24B  | Project Manager | --
| Shamsutdinov Doniyorbek | 202490285 | I24A  | Coder | -- 
| Isayev Yorkinjon | 202490139 | I24B  | Ideator | --
#3. Project Title : Trends in Reading: Paper vs Digital Books
- This project analyzes how reading habits have changed over time, focusing on the comparison between paper books and digital books.
- It uses data analysis techniques in Python (Pandas) to identify trends, age group preferences, and correlations between traditional and digital reading formats.
- The goal is to generate insights and future predictions that can help publishers, libraries, and digital platforms make data-driven decisions.

#4. Dataset Information
- Dataset Title: American Trends Panel Wave 116 – Book Reading and Format Preferences
- Source Organization: Pew Research Center
- Official Dataset Link:
https://www.pewresearch.org/dataset/american-trends-panel-wave-116/
- Description of the Dataset:
- This dataset contains survey responses from U.S. adults about their reading habits. It includes information about whether respondents read books in the past 12 months and which formats they used (print books, e-books, or audiobooks). It also includes demographic variables such as age, gender, income, and education level.
- Why This Dataset Was Selected:
- This dataset directly supports the research objective of analyzing trends in reading habits and comparing paper books with digital formats. It provides real-world survey data that allows meaningful statistical analysis and trend evaluation.
- Dataset Size: Approximately 10,000+ survey responses with multiple demographic and behavioral variables (exact number depends on version downloaded).

#5. Project Objectives
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

#6. Data Preparation
Step 1: Import Libraries
# Import required libraries
import pandas as pd
import numpy as np
Step 2: Load the Dataset
# Load dataset 
df = pd.read_csv("ATP_W116_reading_data.csv")

# Display first 5 rows
df.head()
Step 3: Explore the Dataset
# Check structure
df.info()

# Check missing values
df.isnull().sum()

# Summary statistics
df.describe(include='all')
Step 4: Data Cleaning
# Remove duplicates
df = df.drop_duplicates()

# Fill missing values with 0 (for reading format columns)
df['BOOKPRINT'] = df['BOOKPRINT'].fillna(0)
df['BOOKEBOOK'] = df['BOOKEBOOK'].fillna(0)
df['BOOKAUDIO'] = df['BOOKAUDIO'].fillna(0)

# Convert reading columns to numeric if needed
df['BOOKPRINT'] = pd.to_numeric(df['BOOKPRINT'], errors='coerce')
df['BOOKEBOOK'] = pd.to_numeric(df['BOOKEBOOK'], errors='coerce')
df['BOOKAUDIO'] = pd.to_numeric(df['BOOKAUDIO'], errors='coerce')
Step 5: Feature Creation

Create a new column to classify readers:

# Create new column: Digital Reader (1 if uses ebook or audiobook)
df['DIGITAL_READER'] = np.where(
    (df['BOOKEBOOK'] == 1) | (df['BOOKAUDIO'] == 1),
    1,
    0
)

# Create Print Reader column
df['PRINT_READER'] = np.where(df['BOOKPRINT'] == 1, 1, 0)

df.head()

#7. Data Analysis Tasks (Using Pandas)
- 1. How many people read print vs digital books?
print_readers = df['PRINT_READER'].sum()
digital_readers = df['DIGITAL_READER'].sum()

print("Total Print Readers:", print_readers)
print("Total Digital Readers:", digital_readers)
- 2. Percentage of each format
total_respondents = len(df)

print("Print Readers Percentage:",
      round((print_readers / total_respondents) * 100, 2), "%")

print("Digital Readers Percentage:",
      round((digital_readers / total_respondents) * 100, 2), "%")
- 3. Reading Preference by Age Group
age_analysis = df.groupby('AGE')[['PRINT_READER', 'DIGITAL_READER']].mean() * 100

age_analysis

This shows percentage of print and digital readers in each age group.

- 4. Pivot Table (Education vs Digital Reading)
pivot_table = pd.pivot_table(
    df,
    values='DIGITAL_READER',
    index='EDUCATION',
    aggfunc='mean'
) * 100

pivot_table

This shows how education level affects digital reading preference.

- 5. Correlation Analysis
correlation = df[['PRINT_READER', 'DIGITAL_READER']].corr()

correlation

If correlation is negative → digital growth may reduce print usage.
If positive → many people use both formats.

#8. Key Findings and Insights
After analyzing the dataset using Pandas, several important observations were identified.

- General Reading Preferences
The results show that print books are still widely used among respondents. A large number of people continue to read physical books.
At the same time, digital formats (e-books and audiobooks) are also popular. Many respondents use both print and digital formats. This means that digital books are not completely replacing paper books, but are becoming an additional option.

- Digital Reading Usage
The analysis indicates that digital reading has a significant share among readers.
E-books and audiobooks are especially common among people who regularly use smartphones, tablets, or other digital devices. This suggests that technology plays an important role in reading behavior.
Digital formats are convenient, portable, and easy to access, which may explain their growing popularity.

- Age Differences in Reading Habits
Age group analysis shows clear differences:
Younger respondents are more likely to read digital books.
Older respondents prefer print books more often.
Middle-aged groups often use both formats.
This suggests that younger generations are more comfortable with digital formats, while older generations remain attached to traditional print books.

- Education and Reading Format
The data shows that people with higher education levels tend to use digital reading formats more frequently.
This may be because they use digital materials for study or work purposes. It also suggests that education level may influence access to and use of technology.

- Relationship Between Print and Digital Reading
Correlation analysis shows that the relationship between print and digital reading is not strongly negative.
This means that people who read digital books do not necessarily stop reading print books. Many readers use both formats depending on situation and convenience.

- Practical Implications
The findings suggest several practical conclusions:
Publishers should continue offering both print and digital formats.
Digital platforms have strong potential for growth, especially among younger users.
Libraries and educational institutions should invest in both physical and digital collections.

- Overall Conclusion from Analysis
The main insight of this project is that reading habits are changing, but print books are not disappearing. Instead, digital reading is becoming an additional format that complements traditional books.
The reading industry is moving toward a mixed model where both paper and digital formats coexist.

#9. Project Timeline (5 Weeks)

| Week                     |        Activities                   |
|------------------------  |-------------------------------------|
| Week 1(06.Feb ~ 13.Feb)  | Dataset search and project planning |
| Week 2(13.Feb ~ 20.Feb)  | Data cleaning and preparation |
| Week 3(20.Feb ~ 06.March)  |  Data analysis and visualization |
| Week 5(06.March ~ 13.March)  | Report writing and presentation preparation |
Presentation: 16.March

#10. Outcome of the Project
- Learned to load, clean, and analyze datasets using Pandas
- Developed skills in grouping, pivot tables, filtering, and visualization
- Applied basic trend analysis and ML forecasting

#11. Conclusion
- The project demonstrates how data analysis helps understand changing reading habits, providing actionable insights for publishers, libraries, and digital platforms.

#12. References
- Rew Research Center – Book Reading 2016 Report (https://www.pewresearch.org/internet/2016/09/01/book-reading-2016)
- Pandas documentation – https://pandas.pydata.org/docs/
- Matplotlib documentation – https://matplotlib.org/stable/tutorials/introductory/pyplot.html

#13. Appendix
- Code snippets (see above)
- Charts for trends by year and age group
