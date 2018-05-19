
# District Summary


```python
# import dependencies 
import pandas as pd
import numpy as np
```


```python
# import csv files
schools_complete_csv = 'resources/schools_complete.csv'
students_complete_csv = 'resources/students_complete.csv'
```


```python
# convert to data frame with pandas
schools_df = pd.read_csv(schools_complete_csv)
students_df = pd.read_csv(students_complete_csv)
```


```python
# taking a look at the data
schools_df.head()
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
# making sure there are no NaN values
schools_df.count()
```




    School ID    15
    name         15
    type         15
    size         15
    budget       15
    dtype: int64




```python
# taking a look at the data
students_df.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# making sure there are no NaN values
students_df.count()
```




    Student ID       39170
    name             39170
    gender           39170
    grade            39170
    school           39170
    reading_score    39170
    math_score       39170
    dtype: int64




```python
# calculating total schools
tot_schools = schools_df['name'].count()
tot_schools
```




    15




```python
# calculating total students
tot_students = students_df['name'].count()
tot_students
```




    39170




```python
# calculating total budget
tot_budget = schools_df['budget'].sum()
tot_budget
```




    24649428




```python
# calculating average math scores
avg_math_score = (students_df['math_score'].sum()) / tot_students
avg_math_score
```




    78.98537145774827




```python
# calculating average reading scores
avg_reading_scores = (students_df['reading_score'].sum())/ tot_students
avg_reading_scores
```




    81.87784018381414




```python
# calulating percent passing math
students_df['passing_math'] = np.where(students_df['math_score'] >= 70, 'passing' , 'failing')
print(students_df.head())

list_passing_math = students_df['passing_math'].value_counts().values.tolist()

print(list_passing_math)

perc_passing_math = (list_passing_math[0] / tot_students)*100
print(perc_passing_math)

```

       Student ID               name gender grade             school  \
    0           0       Paul Bradley      M   9th  Huang High School   
    1           1       Victor Smith      M  12th  Huang High School   
    2           2    Kevin Rodriguez      M  12th  Huang High School   
    3           3  Dr. Richard Scott      M  12th  Huang High School   
    4           4         Bonnie Ray      F   9th  Huang High School   
    
       reading_score  math_score passing_math  
    0             66          79      passing  
    1             94          61      failing  
    2             90          60      failing  
    3             67          58      failing  
    4             97          84      passing  
    [29370, 9800]
    74.9808526933878
    


```python
# calulating percent passing reading
students_df['passing_reading'] = np.where(students_df['reading_score'] >= 70, 'passing' , 'failing')
print(students_df.head())

list_passing_reading = students_df['passing_reading'].value_counts().values.tolist()

print(list_passing_reading)

perc_passing_reading = (list_passing_reading[0] / tot_students)*100

print(perc_passing_reading)

```

       Student ID               name gender grade             school  \
    0           0       Paul Bradley      M   9th  Huang High School   
    1           1       Victor Smith      M  12th  Huang High School   
    2           2    Kevin Rodriguez      M  12th  Huang High School   
    3           3  Dr. Richard Scott      M  12th  Huang High School   
    4           4         Bonnie Ray      F   9th  Huang High School   
    
       reading_score  math_score passing_math passing_reading  
    0             66          79      passing         failing  
    1             94          61      failing         passing  
    2             90          60      failing         passing  
    3             67          58      failing         failing  
    4             97          84      passing         passing  
    [33610, 5560]
    85.80546336482001
    


```python
# calculating overall passing rate
overall_passing_rate = ((perc_passing_math + perc_passing_reading)/2)
overall_passing_rate
```




    80.39315802910392




```python
# create summary table
district_summary_df = pd.DataFrame({
    'Total Schools': [tot_schools],
    'Total Students': [tot_students],
    'Total Budget': [tot_budget],
    'Average Math Score': [avg_math_score],
    'Average Reading Score': [avg_reading_scores],
    'Percent Passing Math': [perc_passing_math],
    'Percent Passing Reading': [perc_passing_reading],
    'Overall Passing Rate': [overall_passing_rate]
})

organized_summary_df = district_summary_df[['Total Schools', 'Total Students', 'Total Budget', 'Average Math Score', 'Average Reading Score', \
             'Percent Passing Math', 'Percent Passing Reading', 'Overall Passing Rate']]
# organized_summary_df

organized_summary_df['Total Budget'] = organized_summary_df['Total Budget'].map('${:,}'.format)
organized_summary_df['Total Students'] = organized_summary_df['Total Students'].map('{:,}'.format)
organized_summary_df['Percent Passing Math'] = organized_summary_df['Percent Passing Math'].map('{:.2f}%'.format)
organized_summary_df['Percent Passing Reading'] = organized_summary_df['Percent Passing Reading'].map('{:.2f}%'.format)
organized_summary_df['Overall Passing Rate'] = organized_summary_df['Overall Passing Rate'].map('{:.2f}%'.format)
organized_summary_df['Average Math Score'] = organized_summary_df['Average Math Score'].map('{:,.2f}'.format)
organized_summary_df['Average Reading Score'] = organized_summary_df['Average Reading Score'].map('{:,.2f}'.format)

organized_summary_df
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
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428</td>
      <td>78.99</td>
      <td>81.88</td>
      <td>74.98%</td>
      <td>85.81%</td>
      <td>80.39%</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary


```python
# import dependencies
import pandas as pd
import numpy as np
```


```python
# import csv files
schools_complete_csv = 'resources/schools_complete.csv'
students_complete_csv = 'resources/students_complete.csv'
```


```python
# convert to data frame with pandas
schools_df = pd.read_csv(schools_complete_csv)
students_df = pd.read_csv(students_complete_csv)
```


```python
# taking a look at the data
schools_df.head()
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
# select all rows for columns 'name', 'type', 'size', 'budget'
school_summary_df = schools_df.loc[:, ['name', 'type', 'size', 'budget']].head(15)
school_summary_df.head(15)
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
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
  </tbody>
</table>
</div>




```python
# find per student budget
school_summary_df['Per Student Budget'] = schools_df['budget'] / schools_df['size']
school_summary_df.head()
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
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# rename 'name' to 'school'
organized_school_df = school_summary_df.rename(columns={'name':'school'})
organized_school_df
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# taking a look at the data
students_df.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# group by schools
students_grouped_df = students_df.groupby(['school'])
print(students_grouped_df)
students_grouped_df.count().head(15)

```

    <pandas.core.groupby.DataFrameGroupBy object at 0x000001E8F7E6B198>
    




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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>school</th>
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
      <th>Bailey High School</th>
      <td>4976</td>
      <td>4976</td>
      <td>4976</td>
      <td>4976</td>
      <td>4976</td>
      <td>4976</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
      <td>1858</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>2949</td>
      <td>2949</td>
      <td>2949</td>
      <td>2949</td>
      <td>2949</td>
      <td>2949</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>2739</td>
      <td>2739</td>
      <td>2739</td>
      <td>2739</td>
      <td>2739</td>
      <td>2739</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
      <td>1468</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>4635</td>
      <td>4635</td>
      <td>4635</td>
      <td>4635</td>
      <td>4635</td>
      <td>4635</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
      <td>427</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>2917</td>
      <td>2917</td>
      <td>2917</td>
      <td>2917</td>
      <td>2917</td>
      <td>2917</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>4761</td>
      <td>4761</td>
      <td>4761</td>
      <td>4761</td>
      <td>4761</td>
      <td>4761</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>962</td>
      <td>962</td>
      <td>962</td>
      <td>962</td>
      <td>962</td>
      <td>962</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>3999</td>
      <td>3999</td>
      <td>3999</td>
      <td>3999</td>
      <td>3999</td>
      <td>3999</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
      <td>1761</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
      <td>1635</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
      <td>2283</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
      <td>1800</td>
    </tr>
  </tbody>
</table>
</div>




```python
# sum reading and math scores per school
students_reading_math_df = students_grouped_df['reading_score', 'math_score'].sum()
students_reading_math_df = students_reading_math_df.reset_index()
```


```python
# Merge two dataframes using an outer join
merge_table_df = pd.merge(students_reading_math_df, organized_school_df, on='school', how='outer')
merge_table_df
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
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>403225</td>
      <td>383393</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>156027</td>
      <td>154329</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>239335</td>
      <td>226223</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>221164</td>
      <td>211184</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>123043</td>
      <td>122360</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>375131</td>
      <td>358238</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>35789</td>
      <td>35784</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>236810</td>
      <td>223528</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>385481</td>
      <td>366942</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>80851</td>
      <td>80654</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>322898</td>
      <td>307294</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>147441</td>
      <td>146796</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>137093</td>
      <td>136389</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>191748</td>
      <td>190115</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>151119</td>
      <td>150628</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# find average reading and math score
merge_table_df['Average Reading Score'] = merge_table_df['reading_score']/ merge_table_df['size']
merge_table_df['Average Math Score'] = merge_table_df['math_score']/ merge_table_df['size']
merge_table_df
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
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>403225</td>
      <td>383393</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>156027</td>
      <td>154329</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>239335</td>
      <td>226223</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>221164</td>
      <td>211184</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>123043</td>
      <td>122360</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>375131</td>
      <td>358238</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>35789</td>
      <td>35784</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>236810</td>
      <td>223528</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>385481</td>
      <td>366942</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>80851</td>
      <td>80654</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>322898</td>
      <td>307294</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>147441</td>
      <td>146796</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>137093</td>
      <td>136389</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>191748</td>
      <td>190115</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>151119</td>
      <td>150628</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
# delete total reading score
del merge_table_df['reading_score']
```


```python
# delete total math score
del merge_table_df['math_score']
```


```python
# look at new merged data
merge_table_df
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
# calulating percent passing math
passing_math = students_df.loc[students_df["math_score"] >= 70,:]
passing_math
passing_math_score = passing_math[["school", "math_score"]].groupby("school").count()
passing_math_score = passing_math_score.reset_index()
merge_table_df['Percent Passing Math'] = (passing_math_score['math_score']/ merge_table_df['size']) * 100
merge_table_df
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>66.680064</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>66.752967</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>92.505855</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>93.867121</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>93.333333</td>
    </tr>
  </tbody>
</table>
</div>




```python
# calculating passing reading score
passing_read = students_df.loc[students_df["reading_score"] >= 70,:]
passing_read
passing_read_score = passing_read[["school", "reading_score"]].groupby("school").count()
passing_read_score = passing_read_score.reset_index()
merge_table_df['Percent Passing Reading'] = (passing_read_score['reading_score']/ merge_table_df['size']) * 100
merge_table_df
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>66.680064</td>
      <td>81.933280</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
      <td>97.039828</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
      <td>80.739234</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
      <td>79.299014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
      <td>97.138965</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>66.752967</td>
      <td>80.862999</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>92.505855</td>
      <td>96.252927</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
      <td>81.316421</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
      <td>81.222432</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
      <td>95.945946</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
      <td>80.220055</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>93.867121</td>
      <td>95.854628</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
      <td>97.308869</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
      <td>96.539641</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>93.333333</td>
      <td>96.611111</td>
    </tr>
  </tbody>
</table>
</div>




```python
# overall passing
merge_table_df['Overall Passing Rate'] = (merge_table_df['Percent Passing Reading'] + merge_table_df['Percent Passing Math'])/2
merge_table_df

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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>628.0</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>652.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>581.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>600.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>583.0</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
    </tr>
  </tbody>
</table>
</div>



## Top Performing Schools (By Passing Rate)


```python
merge_table_df.sort_values('Overall Passing Rate').head(5)
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>637.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>639.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>655.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>650.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>644.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
    </tr>
  </tbody>
</table>
</div>



## Bottom Performing Schools


```python
merge_table_df.sort_values('Overall Passing Rate', ascending=False).head(5)
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
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Per Student Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Math</th>
      <th>Percent Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>582.0</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>638.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>609.0</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>625.0</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>578.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
    </tr>
  </tbody>
</table>
</div>



## Math Scores by Grade


```python
students_df[['school', 'grade','math_score']].groupby(['school', 'grade']).mean()
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
      <th></th>
      <th>math_score</th>
    </tr>
    <tr>
      <th>school</th>
      <th>grade</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">Bailey High School</th>
      <th>10th</th>
      <td>76.996772</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>77.515588</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.083676</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Cabrera High School</th>
      <th>10th</th>
      <td>83.154506</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>82.765560</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.094697</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Figueroa High School</th>
      <th>10th</th>
      <td>76.539974</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>76.884344</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>76.403037</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Ford High School</th>
      <th>10th</th>
      <td>77.672316</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>76.918058</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.361345</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Griffin High School</th>
      <th>10th</th>
      <td>84.229064</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>83.842105</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>82.044010</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Hernandez High School</th>
      <th>10th</th>
      <td>77.337408</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>77.136029</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.438495</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Holden High School</th>
      <th>10th</th>
      <td>83.429825</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.787402</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Huang High School</th>
      <th>10th</th>
      <td>75.908735</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>76.446602</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.027251</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Johnson High School</th>
      <th>10th</th>
      <td>76.691117</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>77.491653</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>77.187857</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Pena High School</th>
      <th>10th</th>
      <td>83.372000</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>84.328125</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.625455</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Rodriguez High School</th>
      <th>10th</th>
      <td>76.612500</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>76.395626</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>76.859966</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Shelton High School</th>
      <th>10th</th>
      <td>82.917411</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>83.383495</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.420755</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Thomas High School</th>
      <th>10th</th>
      <td>83.087886</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>83.498795</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.590022</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Wilson High School</th>
      <th>10th</th>
      <td>83.724422</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>83.195326</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.085578</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Wright High School</th>
      <th>10th</th>
      <td>84.010288</td>
    </tr>
    <tr>
      <th>11th</th>
      <td>83.836782</td>
    </tr>
    <tr>
      <th>12th</th>
      <td>83.644986</td>
    </tr>
    <tr>
      <th>9th</th>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>



## Scores By School Spending


```python
bins = [0, 585, 615, 645, 675]
group_names = [">585", '585-615', '615-645', '645-675']
merge_table_df["Spending Ranges"] = pd.cut(merge_table_df["Per Student Budget"], bins, labels=group_names)

# Create a GroupBy object based upon "View Group"
spending_ranges = merge_table_df.groupby('Spending Ranges')

# Find how many rows fall into each bin
# print(spending_ranges['Spending Ranges'].count())

# Get the average of each column within the GroupBy object
spending_ranges = spending_ranges[['Average Reading Score', 'Average Math Score', 'Percent Passing Reading', \
                                   'Percent Passing Math', 'Overall Passing Rate']].mean()

spending_ranges.head()
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
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&gt;585</th>
      <td>83.933814</td>
      <td>83.455399</td>
      <td>96.610877</td>
      <td>93.460096</td>
      <td>95.035486</td>
    </tr>
    <tr>
      <th>585-615</th>
      <td>83.885211</td>
      <td>83.599686</td>
      <td>95.900287</td>
      <td>94.230858</td>
      <td>95.065572</td>
    </tr>
    <tr>
      <th>615-645</th>
      <td>81.891436</td>
      <td>79.079225</td>
      <td>86.106569</td>
      <td>75.668212</td>
      <td>80.887391</td>
    </tr>
    <tr>
      <th>645-675</th>
      <td>81.027843</td>
      <td>76.997210</td>
      <td>81.133951</td>
      <td>66.164813</td>
      <td>73.649382</td>
    </tr>
  </tbody>
</table>
</div>



## Scores By School Size


```python
bins = [0, 1000, 2000, 5000]
group_names = [">1000", "1000-2000", "2000-5000"]
merge_table_df["School Size"] = pd.cut(merge_table_df["size"], bins, labels=group_names)

# Create a GroupBy object based upon "View Group"
school_size = merge_table_df.groupby('School Size')

# Find how many rows fall into each bin
print(school_size['School Size'].count())

# Get the average of each column within the GroupBy object
school_size = school_size[['Average Reading Score', 'Average Math Score', 'Percent Passing Reading', 'Percent Passing Math', 'Overall Passing Rate']].mean()

school_size.head()
```

    School Size
    >1000        2
    1000-2000    5
    2000-5000    8
    Name: School Size, dtype: int64
    




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
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&gt;1000</th>
      <td>83.929843</td>
      <td>83.821598</td>
      <td>96.099437</td>
      <td>93.550225</td>
      <td>94.824831</td>
    </tr>
    <tr>
      <th>1000-2000</th>
      <td>83.864438</td>
      <td>83.374684</td>
      <td>96.790680</td>
      <td>93.599695</td>
      <td>95.195187</td>
    </tr>
    <tr>
      <th>2000-5000</th>
      <td>81.344493</td>
      <td>77.746417</td>
      <td>82.766634</td>
      <td>69.963361</td>
      <td>76.364998</td>
    </tr>
  </tbody>
</table>
</div>



## Scores By School Type


```python

# Create a GroupBy object based upon "View Group"
school_type = merge_table_df.groupby('type')

# Find how many rows fall into each bin
print(school_type['type'].count())

# Get the average of each column within the GroupBy object
school_type = school_type[['Average Reading Score', 'Average Math Score', 'Percent Passing Reading', \
                           'Percent Passing Math', 'Overall Passing Rate']].mean()

school_type.head()
```

    type
    Charter     8
    District    7
    Name: type, dtype: int64
    




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
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>Percent Passing Reading</th>
      <th>Percent Passing Math</th>
      <th>Overall Passing Rate</th>
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
      <th>Charter</th>
      <td>83.896421</td>
      <td>83.473852</td>
      <td>96.586489</td>
      <td>93.620830</td>
      <td>95.103660</td>
    </tr>
    <tr>
      <th>District</th>
      <td>80.966636</td>
      <td>76.956733</td>
      <td>80.799062</td>
      <td>66.548453</td>
      <td>73.673757</td>
    </tr>
  </tbody>
</table>
</div>


