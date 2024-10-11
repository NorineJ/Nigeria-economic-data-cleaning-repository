# Nigeria-economic-data-cleaning-repository
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load data
df = pd.read_csv('nigeria_economic_data.csv')

# Check for missing values
print(df.isnull().sum())

# Handle missing values
df['GDP (nominal)'].fillna(df['GDP (nominal)'].mean(), inplace=True)
df['GDP (PPP)'].fillna(df['GDP (PPP)'].mean(), inplace=True)
df['Inflation Rate'].fillna(df['Inflation Rate'].mean(), inplace=True)
df['Unemployment Rate'].fillna(df['Unemployment Rate'].mean(), inplace=True)

# Plot histogram for GDP (nominal)
plt.hist(df['GDP (nominal)'], bins=50)
plt.show()

# Remove outliers (values > 3 standard deviations from mean)
df = df[(np.abs(df['GDP (nominal)'] - df['GDP (nominal)'].mean()) <= 3 * df['GDP (nominal)'].std())]

# Check data types
print(df.dtypes)


# Convert Year to datetime
df['Year'] = pd.to_datetime(df['Year'], format='%Y')

# Verify data integrity
print(df.head())
print(df.info())
print(df.describe())
