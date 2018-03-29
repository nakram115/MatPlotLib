

```python
# Dependencies
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sb
```


```python
# Load in csv
city_data_df = pd.read_csv("raw_data/city_data.csv")
city_data_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_data_clean_df = pd.DataFrame({'type': city_data_df.groupby('city').first()['type'],
                                'driver_count': city_data_df.groupby('city').sum()['driver_count']}).reset_index()
city_data_clean_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Load in csv
ride_df = pd.read_csv("raw_data/ride_data.csv")
ride_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_data_clean_df.columns
```




    Index(['city', 'driver_count', 'type'], dtype='object')




```python
ride_df.columns
```




    Index(['city', 'date', 'fare', 'ride_id'], dtype='object')




```python
total_fares=ride_df['fare'].sum()
total_fares
```




    63651.31




```python
#Merged Tabled
merge_table_df = pd.merge(ride_df, city_data_clean_df, how="left", on="city")
merge_table_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_city_counts = merge_table_df["city"].value_counts()
ride_city_counts.head()
```




    Port Johnstad    34
    Swansonbury      34
    Port James       32
    South Louis      32
    West Peter       31
    Name: city, dtype: int64




```python
# Group By City
# Using GroupBy in order to separate the data
grouped_city_df = merge_table_df.groupby(['city'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(grouped_city_df)

# In order to be visualized, a data function must be used...
grouped_city_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB553E8A90>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Arnoldview</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Campbellport</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>Carrollbury</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Carrollfort</th>
      <td>29</td>
      <td>29</td>
      <td>29</td>
      <td>29</td>
      <td>29</td>
    </tr>
    <tr>
      <th>Clarkstad</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_city_fare_df=grouped_city_df["fare"].mean()
avg_city_fare_df.head()
```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Name: fare, dtype: float64




```python
fare_summary_table = pd.DataFrame({"City Fare Average":avg_city_fare_df})
fare_summary_table.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City Fare Average</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Rides Per City
# Using GroupBy in order to separate the data 
city_ri_df = merge_table_df.groupby(['city','ride_id'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(city_ri_df)

# In order to be visualized, a data function must be used...
city_ri_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB553E8F98>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>date</th>
      <th>fare</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th>ride_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">Alvarezhaven</th>
      <th>306054352684</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>357421158941</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>858631473935</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1108172306544</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1197329964911</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1806812593131</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2233026076010</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2747592323442</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3565582370530</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3829336915201</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total Number of Rides Per City
total_rides_city= city_ri_df["ride_id"].count()
total_rides_city.head()
```




    city          ride_id      
    Alvarezhaven  306054352684     1
                  357421158941     1
                  858631473935     1
                  1108172306544    1
                  1197329964911    1
    Name: ride_id, dtype: int64




```python
# rides per city is equal to city_counts
total_rides_table = pd.DataFrame({"Total Rides Per City": ride_city_counts })
total_rides_table.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Rides Per City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Port Johnstad</th>
      <td>34</td>
    </tr>
    <tr>
      <th>Swansonbury</th>
      <td>34</td>
    </tr>
    <tr>
      <th>Port James</th>
      <td>32</td>
    </tr>
    <tr>
      <th>South Louis</th>
      <td>32</td>
    </tr>
    <tr>
      <th>West Peter</th>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total Number of Drivers Per City
# Using GroupBy in order to separate the data 
city_driver_df = merge_table_df.groupby(['city','driver_count'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(city_driver_df)

# In order to be visualized, a data function must be used...
city_driver_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB55A906D8>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th>driver_count</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <th>21</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <th>67</th>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <th>16</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <th>21</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <th>49</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Arnoldview</th>
      <th>41</th>
      <td>31</td>
      <td>31</td>
      <td>31</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Campbellport</th>
      <th>26</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>Carrollbury</th>
      <th>4</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Carrollfort</th>
      <th>55</th>
      <td>29</td>
      <td>29</td>
      <td>29</td>
      <td>29</td>
    </tr>
    <tr>
      <th>Clarkstad</th>
      <th>21</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
driver_count = city_driver_df["driver_count"].count()
driver_count.head()
```




    city          driver_count
    Alvarezhaven  21              31
    Alyssaberg    67              26
    Anitamouth    16               9
    Antoniomouth  21              22
    Aprilchester  49              19
    Name: driver_count, dtype: int64




```python
 #City Type (Urban, Suburban, Rural)
# Using GroupBy in order to separate the data 

type_df = city_data_df.groupby(['type'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(type_df)

# In order to be visualized, a data function must be used...count().head(10)
type_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB55A907F0>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>42</td>
      <td>42</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>66</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>




```python
type_count = type_df["type","city"].count()
type_count.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type</th>
      <th>city</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>42</td>
      <td>42</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>66</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>




```python
# % of Total Fares by City Type
# Using GroupBy in order to separate the data 
group_type_city_fare_df = merge_table_df.groupby(['type'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(group_type_city_fare_df)

# In order to be visualized, a data function must be used...count().head(10)
group_type_city_fare_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB55A99908>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_type_city_df= group_type_city_fare_df["fare"].sum()
group_type_city_df.head()
```




    type
    Rural        4255.09
    Suburban    19317.88
    Urban       40078.34
    Name: fare, dtype: float64




```python
#% fare/type
pct_rural= (4255.09/63651.31)*100
pct_rural
```




    6.684999884527122




```python
pct_suburban=(19317.88/63651.31)*100
pct_suburban
```




    30.34954033153442




```python
pct_urban=(40078.34/63651.31)*100
pct_urban
```




    62.965459783938456




```python
#% of Total Rides by City Type
# Using GroupBy in order to separate the data 
rides_type_df = merge_table_df.groupby(['type'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(rides_type_df)

# In order to be visualized, a data function must be used...count().head(10)
rides_type_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB55A99E80>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
      <td>125</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
      <td>625</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
      <td>1625</td>
    </tr>
  </tbody>
</table>
</div>




```python
type_rides_pct_df= rides_type_df['ride_id'].count()
type_rides_pct_df.head()
```




    type
    Rural        125
    Suburban     625
    Urban       1625
    Name: ride_id, dtype: int64




```python
rural_rides=(125/2375)*100
rural_rides
```




    5.263157894736842




```python
suburban_rides=(625/2375)*100
suburban_rides
```




    26.31578947368421




```python
urban_rides=(1625/2375)*100
urban_rides
```




    68.42105263157895




```python
#% of Total Drivers by City Type
# Using GroupBy in order to separate the data 
type1_df = city_data_clean_df.groupby(['type'])

# The object returned is a "GroupBy" object and cannot be viewed normally...
print(type1_df)

# In order to be visualized, a data function must be used...count().head(10)
type1_df.count().head(10)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001EB55AA7470>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>41</td>
      <td>41</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>66</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>




```python
type_drivers_pct_df= type1_df['driver_count'].sum()
type_drivers_pct_df.head()
```




    type
    Rural        104
    Suburban     638
    Urban       2607
    Name: driver_count, dtype: int64




```python
total_drivers_counts_df = city_data_clean_df['driver_count'].sum()
total_drivers_counts_df
```




    3349




```python
# % Drivers Per City Type
rural_drivers=(104/3349)*100
rural_drivers
```




    3.1054045983875787




```python
suburban_drivers=(638/3349)*100
suburban_drivers
```




    19.050462824723798




```python
urban_drivers=(2607/3349)*100
urban_drivers
```




    77.84413257688863




```python
total_rides_city_df = pd.DataFrame(total_rides_city)
```


```python
plt.ylim(20,50)
plt.xlim(0,40)

plt.scatter(total_rides_city_df,avg_city_fare_df,s=total_drivers_counts_df, marker="o", facecolors="red", edgecolors="black", 
            alpha=0.75)

# Create labels for the X and Y axis
plt.title("Pyber Ride Sharing Data 2016")
plt.xlabel("Total # of Rides Per City")
plt.ylabel("Average Fare $")
# Set our legend to where the chart thinks is best
#plt.legend(handles=[averagefare,totalridescity], loc="best")
plt.show
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-37-d72396b27499> in <module>()
          3 
          4 plt.scatter(total_rides_city_df,avg_city_fare_df,s=total_drivers_counts_df, marker="o", facecolors="red", edgecolors="black", 
    ----> 5             alpha=0.75)
          6 
          7 # Create labels for the X and Y axis
    

    ~\Anaconda3\lib\site-packages\matplotlib\pyplot.py in scatter(x, y, s, c, marker, cmap, norm, vmin, vmax, alpha, linewidths, verts, edgecolors, hold, data, **kwargs)
       3376                          vmin=vmin, vmax=vmax, alpha=alpha,
       3377                          linewidths=linewidths, verts=verts,
    -> 3378                          edgecolors=edgecolors, data=data, **kwargs)
       3379     finally:
       3380         ax._hold = washold
    

    ~\Anaconda3\lib\site-packages\matplotlib\__init__.py in inner(ax, *args, **kwargs)
       1715                     warnings.warn(msg % (label_namer, func.__name__),
       1716                                   RuntimeWarning, stacklevel=2)
    -> 1717             return func(ax, *args, **kwargs)
       1718         pre_doc = inner.__doc__
       1719         if pre_doc is None:
    

    ~\Anaconda3\lib\site-packages\matplotlib\axes\_axes.py in scatter(self, x, y, s, c, marker, cmap, norm, vmin, vmax, alpha, linewidths, verts, edgecolors, **kwargs)
       3953         y = np.ma.ravel(y)
       3954         if x.size != y.size:
    -> 3955             raise ValueError("x and y must be the same size")
       3956 
       3957         if s is None:
    

    ValueError: x and y must be the same size



![png](output_36_1.png)



```python
# Labels for the sections of our pie chart
labels = ["Urban", "Rural", "Suburban"]

# The values of each section of the pie chart
sizes = [pct_urban,pct_rural,pct_suburban]

# The colors of each section of the pie chart
colors = ["Gold", "lightskyblue", "lightcoral"]

# Tells matplotlib to seperate the section from the others
explode = (0.1, 0, 0)
```


```python
# Creates the pie chart based upon the values above
# Automatically finds the percentages of each part of the pie chart
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)

# Tells matplotlib that we want a pie chart with equal axes EGG!!
plt.axis("equal")

# Give our chart some labels and a tile
plt.title("% Total Fares by City Type")

plt.show
```


```python
# Labels for the sections of our pie chart
labels = ["Urban", "Rural", "Suburban"]

# The values of each section of the pie chart
sizes = [urban_rides,rural_rides,suburban_rides]

# The colors of each section of the pie chart
colors = ["Gold", "lightskyblue", "lightcoral"]

# Tells matplotlib to seperate the section from the others
explode = (0.1, 0, 0)
```


```python
# Creates the pie chart based upon the values above
# Automatically finds the percentages of each part of the pie chart
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)

# Tells matplotlib that we want a pie chart with equal axes EGG!!
plt.axis("equal")

# Give our chart some labels and a tile
plt.title("% Total Rides by City Type")

plt.show
```


```python
# Labels for the sections of our pie chart
labels = ["Urban", "Rural", "Suburban"]

# The values of each section of the pie chart
sizes = [urban_drivers,rural_drivers,suburban_drivers]

# The colors of each section of the pie chart
colors = ["Gold", "lightskyblue", "lightcoral"]

# Tells matplotlib to seperate the section from the others
explode = (0.1, 0, 0)
```


```python
# Creates the pie chart based upon the values above
# Automatically finds the percentages of each part of the pie chart
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=75)

# Tells matplotlib that we want a pie chart with equal axes EGG!!
plt.axis("equal")

# Give our chart some labels and a tile
plt.title("% Total Drivers by City Type")

plt.show
```


```python
#1) Urban has the highest percentage for all three categories: % of fares by city type, % total rides by city type, 
#    % Total drivers by city type.
#2) Suburban is the second highest in percentage for fares by city type and total rides by city type but rural is higher 
#    for % total drivers by city type.
#3) The less driver count per city type, higher the average fare. With less drivers, you pay more.
```
