# Zomato-Data-Analysis
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# ** importing the dataset**
df=pd.read_csv(r'/Zomato data .csv')
df.head()

# **convert data type of rate column**
def handleRate(value):
  value=str(value).split('/')
  value=value[0]
  return float(value)
df['rate']=df['rate'].apply(handleRate)
print(df.head())

# **getting info about rows and columns
df.info()

# **Plotting Name vs Votes**
grouped_data = df.groupby('name')['votes'].sum()
result=pd.DataFrame({'votes':grouped_data})
result
plt.figure(figsize=(25,8))
plt.bar(result.index,result['votes'],color='red')
plt.xticks(rotation=90)
plt.xlabel('Name of Restaurant')
plt.ylabel('votes')
plt.show()

# **Plotting Type of Restaurant vs Online order**
online_order = df[df['online_order']=="Yes"]
type_counts = online_order["listed_in(type)"].value_counts()
type_counts
plt.plot(type_counts,color='red')
plt.xlabel('Type of Restaurant')
plt.ylabel('count')
plt.xticks(rotation=45)
plt.show()

# **Average order amount spending by two people**
average_order_amount=df['approx_cost(for two people)']
sns.countplot(x=average_order_amount)

# **Plot online order vs offline order**
sns.boxplot(x='online_order',y='rate',data=df)
