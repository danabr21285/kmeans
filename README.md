## Project Goal: Segmenting E-Commerce Customers
The objective is to analyze a customer dataset to identify distinct groups or segments based on their purchasing behavior. The insights from this analysis will help the marketing team create targeted campaigns, improve customer retention, and personalize user experience. 🎯

---
## Technologies Used
- Programming Language: R

- Core Libraries: tidyverse (for data manipulation and visualization), cluster, factoextra (for clustering)

- Dataset:simulated data

- IDE: RStudio

----
## Step 1: Exploratory Data Analysis (EDA) & Preprocessing
Before clustering, you must understand and prepare your data. This is where the tidyverse shines.

Load and Clean Data:
```
# Load necessary libraries
library(tidyverse)
library(cluster)
library(factoextra)

# Load your data
rfm_data <- read_csv("your_rfm_data.csv")

# Inspect the data
glimpse(rfm_data)
summary(rfm_data)

# Check for missing values and remove any if necessary
rfm_data <- na.omit(rfm_data)

# Remove any logical inconsistencies (e.g., MonetaryValue <= 0)
rfm_data_clean <- rfm_data %>%
  filter(MonetaryValue > 0)
```
## Visualize Distributions: 
Check for outliers and skewness in your RFM variables using ggplot2. Highly skewed data can distort clusters. 
```
# Plot distribution of Monetary value
ggplot(rfm_data_clean, aes(x = MonetaryValue)) +
  geom_histogram(bins = 30, fill = "skyblue", color = "black") +
  ggtitle("Distribution of Monetary Value")
```
![Monetary Value Distributions Plot](monetaryvalue.png)

# Highly skewed, Applied a log transform.
```
rfm_data_clean$MonetaryLog <- log(rfm_data_clean$MonetaryValue)
```
---
## Step 2: Determine the Optimal Number of Clusters (K)
- Elbow Method: Calculates the variance explained as a function of the number of clusters. Look for an "elbow" in the plot where adding more clusters doesn't significantly improve the model.
```


