
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
import warnings
warnings.filterwarnings('ignore')

sd=pd.read_csv("StoreData.csv")
sd
sd.head(10)
sd.columns
sd.shape
sd.isnull().sum()
Q1 = sd['Age'].quantile(0.25)
Q3 = sd['Age'].quantile(0.75)
IQR = Q3 - Q1
# Identify and remove outliers
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
df = sd[(sd['Age'] >= lower_bound) & (sd['Age'] <= upper_bound)]
df
sd.describe()
df.describe()
sd.describe(include='object')
sd['Age'].mean()

most_common_Age = sd['Age'].mode()
print(most_common_Age)

# Gender and Age
gender_counts = df['Gender'].value_counts()
age_statistics = df['Age'].describe()
# Date and Month
earliest_date = df['Date'].min()
latest_date = df['Date'].max()
month_counts = df['Month'].value_counts()
# Status
status_counts = df['Status'].value_counts()
# Category (type of dress)
category_counts = df['Category'].value_counts()
# Size
most_common_size = df['Age'].mode()
# Quantity and Amount
quantity_statistics = df['Qty'].describe()
amount_statistics = df['Amount'].describe()
# Shipping city state and Shipping postal code
city_state_counts = df['ship-state'].value_counts()
postal_code_counts = df['ship-postal-code'].value_counts()
# Print the results
print("Gender Counts:\n", gender_counts)
print("\nAge Statistics:\n", age_statistics)
print("\nEarliest Date:", earliest_date)
print("Latest Date:", latest_date)
print("\nMonth Counts:\n", month_counts)
print("\nStatus Counts:\n", status_counts)
print("\nCategory Counts:\n", category_counts)
print("\nMost Common Size:", most_common_size[0])
print("\nQuantity Statistics:\n", quantity_statistics)
print("\nAmount Statistics:\n", amount_statistics)
print("\nCity/State Counts:\n", city_state_counts)
print("\nPostal Code Counts:\n", postal_code_counts)


sns.histplot(data=df, x='Age', bins=20)
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Age Distribution')
plt.show()


sns.boxplot(data=df, x='Category', y='Amount')
plt.xlabel('Category')
plt.ylabel('Amount')
plt.title('Amount Distribution by Category')
plt.xticks(rotation=45)
plt.show()


sns.countplot(data=df, x='Gender')
plt.xlabel('Gender')
plt.ylabel('Count')
plt.title('Gender Distribution')
plt.show()

sns.scatterplot(data=df, x='Age', y='Amount')
plt.xlabel('Age')
plt.ylabel('Amount')
plt.title('Scatter Plot of Age vs. Amount')
plt.show()

dd=df[['Age','Amount']]
correlation_matrix = dd.corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Correlation Heatmap')
plt.show()


channel_counts = sd['Category'].value_counts()
plt.pie(channel_counts, labels=channel_counts.index, autopct='%1.1f%%')
plt.axis('equal')
plt.title('Sales Type Distribution')
plt.show()

sns.violinplot(data=sd, x='Gender', y='Age')
plt.xlabel('Gender')
plt.ylabel('Age')
plt.title('Age Distribution by Gender')
plt.show()

