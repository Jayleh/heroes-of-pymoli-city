
# Observable Trends

###### 1. Most players who play Heroes of Pymoli are male (81.15%).
###### 2. Close to half the players (45.2%) from the game's database range from ages 20 to 24. This age group has also contributed approximately 45% of the total amount of purchases.
###### 3. The most popular and also the most profitable item purchased is the Final Critic, with 14 purchased for a total of $38.60.


```python
# Dependencies
import pandas as pd
```


```python
# Set json path
json_path = 'raw_data/purchase_data.json'
```


```python
# Read json file
heroes_df = pd.read_json(json_path)
heroes_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Look at column names
heroes_df.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
# Reorginizing columns
heroes_df = heroes_df[['SN', 'Gender', 'Age', 'Item ID', 'Item Name', 'Price']]
heroes_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aelalis34</td>
      <td>Male</td>
      <td>38</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Eolo46</td>
      <td>Male</td>
      <td>21</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Assastnya25</td>
      <td>Male</td>
      <td>34</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pheusrical25</td>
      <td>Male</td>
      <td>21</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>Male</td>
      <td>23</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Checking out the data
heroes_df.count()
```




    SN           780
    Gender       780
    Age          780
    Item ID      780
    Item Name    780
    Price        780
    dtype: int64



# Total Unique Players


```python
# Find number of unique players
total_players = len(heroes_df['SN'].unique())
total_players
```




    573



# Purchasing Analysis (Total)


```python
# Number of unique items
number_unique_items = len(heroes_df['Item ID'].unique())
print(number_unique_items)

# Average purchase price of unique items
avg_price = heroes_df['Price'].mean()
print(avg_price)

# Number of purchases
purchases = len(heroes_df['Price'])
print(purchases)

# Total revenue
revenue = heroes_df['Price'].sum()
print(revenue)
```

    183
    2.931192307692303
    780
    2286.3299999999963
    


```python
# Create purchasing analysis dataframe
purchase_analysis = {'Number of Unique Items': [number_unique_items], 
                     'Average Price': [f'${avg_price:.2f}'], 
                     'Number of Purchases': [purchases], 
                     'Total Revenue': [f'${revenue:,.2f}']}

purchase_analysis_df = pd.DataFrame(purchase_analysis)

# Reorder columns
purchase_analysis_df = purchase_analysis_df[['Number of Unique Items', 'Average Price', 'Number of Purchases', 'Total Revenue']]

# Purchasing Analysis (Total)
purchase_analysis_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2,286.33</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics


```python
# Only grab unique players by dropping duplicates
unique_heroes_df = heroes_df.drop_duplicates(subset='SN', keep='first')
unique_heroes_df.count()
```




    SN           573
    Gender       573
    Age          573
    Item ID      573
    Item Name    573
    Price        573
    dtype: int64




```python
# Group by gender to see count
unique_grouped_gender = unique_heroes_df.groupby('Gender').count()
unique_grouped_gender
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>465</td>
      <td>465</td>
      <td>465</td>
      <td>465</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Convert the counts of each gender into a dataframe 
unique_grouped_gender_df = pd.DataFrame(unique_grouped_gender)

# Add percentage of players
unique_grouped_gender_df['Percentage of Players'] = round(unique_grouped_gender['SN']/total_players*100, 2)
unique_grouped_gender_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>17.45</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>465</td>
      <td>465</td>
      <td>465</td>
      <td>465</td>
      <td>465</td>
      <td>81.15</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>1.40</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Rename SN column
unique_grouped_gender_df = unique_grouped_gender_df.rename(columns={'SN': 'Total Count'})

# Reorganize columns
gender_demo = unique_grouped_gender_df[['Percentage of Players', 'Total Count']]

# Gender Demographics
gender_demo
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)


```python
# Group by gender for Purchasing Analysis (Gender)
grouped_gender = heroes_df.groupby(['Gender'])
grouped_gender
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x0000017669706828>




```python
# Grab purchase count for each gender
purchase_count = grouped_gender['Price'].count()
purchase_count

# Grab average price for each gender
avg_purchase_price = grouped_gender['Price'].mean()
avg_purchase_price

# Grab sum for each gender
total_purchase_value = grouped_gender['Price'].sum()
total_purchase_value
```




    Gender
    Female                    382.91
    Male                     1867.68
    Other / Non-Disclosed      35.74
    Name: Price, dtype: float64




```python
# Create Purchasing Analysis (Gender)
gender_purchasing_analysis = pd.DataFrame({'Purchase Count': purchase_count, 
                                           'Average Purchase Price': avg_purchase_price, 
                                           'Total Purchase Value': total_purchase_value})
# Reorder columns
gender_purchasing_analysis = gender_purchasing_analysis[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]

# Find mean and standard deviation of average purchase price of the population
mean_norm = heroes_df['Price'].mean()
stdev_norm = heroes_df['Price'].std()

# Calculate the z value, standard score of a raw score 
z_value = (gender_purchasing_analysis['Average Purchase Price']-mean_norm)/stdev_norm

# Calculate normalized totals and add to analysis
gender_purchasing_analysis['Normalized Totals'] = gender_purchasing_analysis['Average Purchase Price']+z_value

# Format values
gender_purchasing_analysis['Average Purchase Price'] = gender_purchasing_analysis['Average Purchase Price'].map("${:.2f}".format)
gender_purchasing_analysis['Total Purchase Value'] = gender_purchasing_analysis['Total Purchase Value'].map("${:,.2f}".format)
gender_purchasing_analysis['Normalized Totals'] = gender_purchasing_analysis['Normalized Totals'].map("${:.2f}".format)

# Purchase Analysis (Gender)
gender_purchasing_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$2.71</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>$2.97</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$3.53</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
# Create bins for Age Demographics Analysis
bins = [2, 9, 14, 19, 24, 29, 34, 39, 99]
labels = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

# Add bins column to dataframe
unique_heroes_df['Age Range'] = pd.cut(unique_heroes_df['Age'], bins=bins, labels=labels)
unique_heroes_df.head()
```

    C:\Users\Justin\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age Range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aelalis34</td>
      <td>Male</td>
      <td>38</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Eolo46</td>
      <td>Male</td>
      <td>21</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Assastnya25</td>
      <td>Male</td>
      <td>34</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pheusrical25</td>
      <td>Male</td>
      <td>21</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>Male</td>
      <td>23</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by age range
grouped_age_range = unique_heroes_df.groupby(['Age Range']).count()
grouped_age_range
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>259</td>
      <td>259</td>
      <td>259</td>
      <td>259</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>47</td>
      <td>47</td>
      <td>47</td>
      <td>47</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
      <td>27</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Convert the counts of each age range into a dataframe
age_demo_df = pd.DataFrame(grouped_age_range)

# Add percentage of players
age_demo_df['Percentage of Players'] = round(age_demo_df['Age']/total_players*100, 2)

# Rename Age column
age_demo_df = age_demo_df.rename(columns={'Age': 'Total Count'})

# Reduce dataframe and reorganize columns
age_demo_df = age_demo_df[['Percentage of Players', 'Total Count']]

# Age Demographics
age_demo_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>3.32</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.01</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.20</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>15.18</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.20</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>4.71</td>
      <td>27</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.92</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Age)


```python
# Group by Age Range
grouped_age_range = unique_heroes_df.groupby(['Age Range'])

# Grab purchase count for each age range
purchase_count = grouped_age_range['Price'].count()
purchase_count

# Grab average price for each age range
avg_purchase_price = round(grouped_age_range['Price'].mean(), 2)
avg_purchase_price

# Grab sum for each age range
total_purchase_value = grouped_age_range['Price'].sum()
total_purchase_value
```




    Age Range
    <10       59.45
    10-14     62.04
    15-19    289.88
    20-24    765.69
    25-29    263.53
    30-34    152.60
    35-39     78.65
    40+       34.25
    Name: Price, dtype: float64




```python
# Create Purchasing Analysis (Age)
age_purchasing_analysis = pd.DataFrame({'Purchase Count': purchase_count, 
                                           'Average Purchase Price': avg_purchase_price, 
                                           'Total Purchase Value': total_purchase_value})
# Reorder columns
age_purchasing_analysis = age_purchasing_analysis[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]

# Find mean and standard deviation of average purchase price of the population
mean_norm = heroes_df['Price'].mean()
stdev_norm = heroes_df['Price'].std()

# Calculate the z value, standard score of a raw score 
z_value = (age_purchasing_analysis['Average Purchase Price']-mean_norm)/stdev_norm

# Calculate normalized totals and add to analysis
age_purchasing_analysis['Normalized Totals'] = age_purchasing_analysis['Average Purchase Price']+z_value

# Format values
age_purchasing_analysis['Average Purchase Price'] = age_purchasing_analysis['Average Purchase Price'].map("${:.2f}".format)
age_purchasing_analysis['Total Purchase Value'] = age_purchasing_analysis['Total Purchase Value'].map("${:,.2f}".format)
age_purchasing_analysis['Normalized Totals'] = age_purchasing_analysis['Normalized Totals'].map("${:.2f}".format)

# Purchasing Analysis (Age)
age_purchasing_analysis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>19</td>
      <td>$3.13</td>
      <td>$59.45</td>
      <td>$3.31</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>23</td>
      <td>$2.70</td>
      <td>$62.04</td>
      <td>$2.49</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>$2.90</td>
      <td>$289.88</td>
      <td>$2.87</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>$2.96</td>
      <td>$765.69</td>
      <td>$2.99</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>$3.03</td>
      <td>$263.53</td>
      <td>$3.12</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>$3.25</td>
      <td>$152.60</td>
      <td>$3.54</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>$2.91</td>
      <td>$78.65</td>
      <td>$2.89</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>11</td>
      <td>$3.11</td>
      <td>$34.25</td>
      <td>$3.27</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
# Groupy by SN
grouped_players = heroes_df.groupby('SN')

# Grab purchase count for each age range
purchase_count = grouped_players['Price'].count()
purchase_count.head()

# Grab average price for each age range
avg_purchase_price = round(grouped_players['Price'].mean(), 2)
avg_purchase_price.head()

# Grab sum for each age range
total_purchase_value = grouped_players['Price'].sum()
total_purchase_value.head()
```




    SN
    Adairialis76    2.46
    Aduephos78      6.70
    Aeduera68       5.80
    Aela49          2.46
    Aela59          1.27
    Name: Price, dtype: float64




```python
# Create Top Spenders Analysis
top_spenders_analysis = pd.DataFrame({'Purchase Count': purchase_count, 
                                        'Average Purchase Price': avg_purchase_price, 
                                        'Total Purchase Value': total_purchase_value})

# Reorder columns
top_spenders_analysis = top_spenders_analysis[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value']]

# Sort values by total purchase value
top_spenders_analysis = top_spenders_analysis.sort_values(by='Total Purchase Value', ascending=False)

# Format values
top_spenders_analysis['Average Purchase Price'] = top_spenders_analysis['Average Purchase Price'].map('${:.2f}'.format)
top_spenders_analysis['Total Purchase Value'] = top_spenders_analysis['Total Purchase Value'].map('${:.2f}'.format)

# Top 5 Spenders
top_spenders_analysis.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
# Group by Item Name
grouped_items = heroes_df.groupby(['Item ID'])
grouped_items
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x00000176696B10F0>




```python
# Grab purchase count for each item
purchase_count = grouped_items['Price'].count()
purchase_count

# Grab sum for each item
total_purchase_value = grouped_items['Price'].sum()
total_purchase_value.head()
```




    Item ID
    0    1.82
    1    9.12
    2    3.40
    3    1.79
    4    2.28
    Name: Price, dtype: float64




```python
# Create Most Popular Items Analysis
most_popular_count_total = pd.DataFrame({'Purchase Count': purchase_count, 
                                         'Total Purchase Value': total_purchase_value})

most_popular_count_total.reset_index(inplace=True)
most_popular_count_total.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>4</td>
      <td>9.12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reduce heroes df to merge
most_popular_id_price = heroes_df[['Item Name', 'Item ID', 'Price']]

# Drop duplicate Item Names
most_popular_id_price = most_popular_id_price.drop_duplicates(subset='Item ID', keep='first')

most_popular_id_price.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bone Crushing Silver Skewer</td>
      <td>165</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>119</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Primitive Blade</td>
      <td>174</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Final Critic</td>
      <td>92</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Stormfury Mace</td>
      <td>63</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge dataframes on Item Name
combined_most_popular = pd.merge(most_popular_count_total, most_popular_id_price, on='Item ID', how='inner')
combined_most_popular.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>1.82</td>
      <td>Splinter</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>4</td>
      <td>9.12</td>
      <td>Crucifer</td>
      <td>2.28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>3.40</td>
      <td>Verdict</td>
      <td>3.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
      <td>1.79</td>
      <td>Phantomlight</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>1</td>
      <td>2.28</td>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Rename Price column
most_popular_analysis = combined_most_popular.rename(columns={'Price': 'Item Price'})

# Reorganize columns
most_popular_analysis = most_popular_analysis[['Item ID', 'Item Name', 'Purchase Count', 'Item Price', 'Total Purchase Value']]

# Group by to create Most Popular Analysis
most_popular_analysis = most_popular_analysis.set_index(['Item ID', 'Item Name'])

# Sort by greatest purchase count
most_popular_analysis = most_popular_analysis.sort_values(by=['Purchase Count'], ascending=False)

# Format values
most_popular_analysis['Item Price'] = most_popular_analysis['Item Price'].map('${:.2f}'.format)
most_popular_analysis['Total Purchase Value'] = most_popular_analysis['Total Purchase Value'].map('${:.2f}'.format)

# Most Popular Items Analysis
most_popular_analysis.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
# Format values back to numeric
most_popular_analysis['Item Price'] = pd.to_numeric(most_popular_analysis['Item Price'].str.replace('$', ''))
most_popular_analysis['Total Purchase Value'] = pd.to_numeric(most_popular_analysis['Total Purchase Value'].str.replace('$', ''))

# Sort by total purchase value
most_profit_analysis = most_popular_analysis.sort_values(by=['Total Purchase Value'], ascending=False)

# Format values
most_profit_analysis['Item Price'] = most_profit_analysis['Item Price'].map('${:.2f}'.format)
most_profit_analysis['Total Purchase Value'] = most_profit_analysis['Total Purchase Value'].map('${:.2f}'.format)

# Most Profitable Items Analysis
most_profit_analysis.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


