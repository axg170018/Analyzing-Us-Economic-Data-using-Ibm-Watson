
<h1>Analyzing US Economic Data and  Building a Simple Dashboard (Akash Gupta) </h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this tutorial, you will extract some essential economic indicators from some data, you will then display these economic indicators in a Dashboard. You can then share the dashboard via an URL.
<p>
<a href="https://en.wikipedia.org/wiki/Gross_domestic_product"> Gross domestic product (GDP)</a> is a measure of the market value of all the final goods and services produced in a period. GDP is an indicator of how well the economy is doing. A drop in GDP indicates the economy is producing less; similarly an increase in GDP suggests the economy is performing better. In this lab, you will examine how changes in GDP impact the unemployment rate. You will take screen shots of every step, you will share the notebook and the URL pointing to the dashboard.</p>

<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
        <li><a href="#Section_1"> Define a Function that Makes a Dashboard </a></li>
    <li><a href="#Section_2">Question 1: Create a dataframe that contains the GDP data and display it</a> </li>
    <li><a href="#Section_3">Question 2: Create a dataframe that contains the unemployment data and display it</a></li>
    <li><a href="#Section_4">Question 3: Display a dataframe where unemployment was greater than 8.5%</a></li>
    <li><a href="#Section_5">Question 4: Use the function make_dashboard to make a dashboard</a></li>
     <li><a href="#Section_6">Question 5: Save the dashboard on IBM cloud and display it</a></li>
    </ul>
<p>
    Estimated Time Needed: <strong>180 min</strong></p>
</div>

<hr>

<h2 id="Section_1"> Define Function that Makes a Dashboard  </h2>

We will import the following libraries.


```python
import pandas as pd
from bokeh.plotting import figure, output_file, show,output_notebook
output_notebook()
```



    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1001">Loading BokehJS ...</span>
    </div>




In this section, we define the function <code>make_dashboard</code>. 
You don't have to know how the function works, you should only care about the inputs. The function will produce a dashboard as well as an html file. You can then use this html file to share your dashboard. If you do not know what an html file is don't worry everything you need to know will be provided in the lab. 


```python
def make_dashboard(x, gdp_change, unemployment, title, file_name):
    output_file(file_name)
    p = figure(title=title, x_axis_label='year', y_axis_label='%')
    p.line(x.squeeze(), gdp_change.squeeze(), color="firebrick", line_width=4, legend="% GDP change")
    p.line(x.squeeze(), unemployment.squeeze(), line_width=4, legend="% unemployed")
    show(p)
```

The dictionary  <code>links</code> contain the CSV files with all the data. The value for the key <code>GDP</code> is the file that contains the GDP data. The value for the key <code>unemployment</code> contains the unemployment data.


```python
links={'GDP':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_gdp.csv',\
       'unemployment':'https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/coursera_project/clean_unemployment.csv'}
```

<h3 id="Section_2"> Question 1: Create a dataframe that contains the GDP data and display the first five rows of the dataframe.</h3>

Use the dictionary <code>links</code> and the function <code>pd.read_csv</code> to create a Pandas dataframes that contains the GDP data.

<b>Hint: <code>links["GDP"]</code> contains the path or name of the file.</b>


```python
# Type your code here
gdp=pd.read_csv(links["GDP"])
```

Use the method <code>head()</code> to display the first five rows of the GDP data, then take a screen-shot.


```python
# Type your code here
gdp.head(5)
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
      <th>date</th>
      <th>level-current</th>
      <th>level-chained</th>
      <th>change-current</th>
      <th>change-chained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>274.8</td>
      <td>2020.0</td>
      <td>-0.7</td>
      <td>-0.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>272.8</td>
      <td>2008.9</td>
      <td>10.0</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>300.2</td>
      <td>2184.0</td>
      <td>15.7</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>347.3</td>
      <td>2360.0</td>
      <td>5.9</td>
      <td>4.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>367.7</td>
      <td>2456.1</td>
      <td>6.0</td>
      <td>4.7</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

<h3 id="Section_2"> Question 2: Create a dataframe that contains the unemployment data. Display the first five rows of the dataframe. </h3>

Use the dictionary <code>links</code> and the function <code>pd.read_csv</code> to create a Pandas dataframes that contains the unemployment data.


```python
# Type your code here
unemp=pd.read_csv(links["unemployment"])
```

Use the method <code>head()</code> to display the first five rows of the GDP data, then take a screen-shot.


```python
# Type your code here
unemp.head(5)
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
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>3.025000</td>
    </tr>
  </tbody>
</table>
</div>




```python
unemp.describe()
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
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>69.000000</td>
      <td>69.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1982.000000</td>
      <td>5.810628</td>
    </tr>
    <tr>
      <th>std</th>
      <td>20.062403</td>
      <td>1.608657</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1948.000000</td>
      <td>2.925000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1965.000000</td>
      <td>4.741667</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1982.000000</td>
      <td>5.591667</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1999.000000</td>
      <td>6.850000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2016.000000</td>
      <td>9.708333</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_3">Question 3: Display a dataframe where unemployment was greater than 8.5%.</h3>


```python
# Type your code here
unemp1=unemp[(unemp['unemployment']>8.5)]
unemp1
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
      <th>date</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <td>1982</td>
      <td>9.708333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1983</td>
      <td>9.600000</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2009</td>
      <td>9.283333</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2010</td>
      <td>9.608333</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2011</td>
      <td>8.933333</td>
    </tr>
  </tbody>
</table>
</div>



<h3 id="Section_4">Question 4: Use the function make_dashboard to make a dashboard</h3>

In this section, you will call the function  <code>make_dashboard</code> , to produce a dashboard. We will use the convention of giving each variable the same name as the function parameter.

Create a new dataframe with the column <code>'date'</code> called <code>x</code> from the dataframe that contains the GDP data.


```python
x1 =unemp
x1.columns=['x','unemployment']
x1# Create your dataframe with column date
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
      <th>x</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>3.025000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1953</td>
      <td>2.925000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1954</td>
      <td>5.591667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1955</td>
      <td>4.366667</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1956</td>
      <td>4.125000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1957</td>
      <td>4.300000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1958</td>
      <td>6.841667</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1959</td>
      <td>5.450000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1960</td>
      <td>5.541667</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1961</td>
      <td>6.691667</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1962</td>
      <td>5.566667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1963</td>
      <td>5.641667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1964</td>
      <td>5.158333</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1965</td>
      <td>4.508333</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1966</td>
      <td>3.791667</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1967</td>
      <td>3.841667</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1968</td>
      <td>3.558333</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1969</td>
      <td>3.491667</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1970</td>
      <td>4.983333</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1971</td>
      <td>5.950000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1972</td>
      <td>5.600000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1973</td>
      <td>4.858333</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1974</td>
      <td>5.641667</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1975</td>
      <td>8.475000</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1976</td>
      <td>7.700000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1977</td>
      <td>7.050000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39</th>
      <td>1987</td>
      <td>6.175000</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1988</td>
      <td>5.491667</td>
    </tr>
    <tr>
      <th>41</th>
      <td>1989</td>
      <td>5.258333</td>
    </tr>
    <tr>
      <th>42</th>
      <td>1990</td>
      <td>5.616667</td>
    </tr>
    <tr>
      <th>43</th>
      <td>1991</td>
      <td>6.850000</td>
    </tr>
    <tr>
      <th>44</th>
      <td>1992</td>
      <td>7.491667</td>
    </tr>
    <tr>
      <th>45</th>
      <td>1993</td>
      <td>6.908333</td>
    </tr>
    <tr>
      <th>46</th>
      <td>1994</td>
      <td>6.100000</td>
    </tr>
    <tr>
      <th>47</th>
      <td>1995</td>
      <td>5.591667</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1996</td>
      <td>5.408333</td>
    </tr>
    <tr>
      <th>49</th>
      <td>1997</td>
      <td>4.941667</td>
    </tr>
    <tr>
      <th>50</th>
      <td>1998</td>
      <td>4.500000</td>
    </tr>
    <tr>
      <th>51</th>
      <td>1999</td>
      <td>4.216667</td>
    </tr>
    <tr>
      <th>52</th>
      <td>2000</td>
      <td>3.966667</td>
    </tr>
    <tr>
      <th>53</th>
      <td>2001</td>
      <td>4.741667</td>
    </tr>
    <tr>
      <th>54</th>
      <td>2002</td>
      <td>5.783333</td>
    </tr>
    <tr>
      <th>55</th>
      <td>2003</td>
      <td>5.991667</td>
    </tr>
    <tr>
      <th>56</th>
      <td>2004</td>
      <td>5.541667</td>
    </tr>
    <tr>
      <th>57</th>
      <td>2005</td>
      <td>5.083333</td>
    </tr>
    <tr>
      <th>58</th>
      <td>2006</td>
      <td>4.608333</td>
    </tr>
    <tr>
      <th>59</th>
      <td>2007</td>
      <td>4.616667</td>
    </tr>
    <tr>
      <th>60</th>
      <td>2008</td>
      <td>5.800000</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2009</td>
      <td>9.283333</td>
    </tr>
    <tr>
      <th>62</th>
      <td>2010</td>
      <td>9.608333</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2011</td>
      <td>8.933333</td>
    </tr>
    <tr>
      <th>64</th>
      <td>2012</td>
      <td>8.075000</td>
    </tr>
    <tr>
      <th>65</th>
      <td>2013</td>
      <td>7.358333</td>
    </tr>
    <tr>
      <th>66</th>
      <td>2014</td>
      <td>6.158333</td>
    </tr>
    <tr>
      <th>67</th>
      <td>2015</td>
      <td>5.275000</td>
    </tr>
    <tr>
      <th>68</th>
      <td>2016</td>
      <td>4.875000</td>
    </tr>
  </tbody>
</table>
<p>69 rows × 2 columns</p>
</div>



Create a new dataframe with the column <code>'change-current' </code> called <code>gdp_change</code>  from the dataframe that contains the GDP data.


```python
gdp_change1 =gdp
gdp_change1.rename(columns={'change-current':'gdp_change'},inplace=True)
gdp_change1.head(5)# Create your dataframe with column change-current
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
      <th>date</th>
      <th>level-current</th>
      <th>level-chained</th>
      <th>gdp_change</th>
      <th>change-chained</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>274.8</td>
      <td>2020.0</td>
      <td>-0.7</td>
      <td>-0.6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>272.8</td>
      <td>2008.9</td>
      <td>10.0</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>300.2</td>
      <td>2184.0</td>
      <td>15.7</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>347.3</td>
      <td>2360.0</td>
      <td>5.9</td>
      <td>4.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>367.7</td>
      <td>2456.1</td>
      <td>6.0</td>
      <td>4.7</td>
    </tr>
  </tbody>
</table>
</div>



Create a new dataframe with the column <code>'unemployment' </code> called <code>unemployment</code>  from the dataframe that contains the  unemployment data.


```python
unemployment1 =unemp
unemployment1.rename(columns={'unemployment':'unemployment'})
unemployment1.head(5)# Create your dataframe with column unemployment
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
      <th>x</th>
      <th>unemployment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1948</td>
      <td>3.750000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1949</td>
      <td>6.050000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1950</td>
      <td>5.208333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1951</td>
      <td>3.283333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1952</td>
      <td>3.025000</td>
    </tr>
  </tbody>
</table>
</div>



Give your dashboard a string title, and assign it to the variable <code>title</code>


```python
title = str("Us Economy Evaluation")# Give your dashboard a string title
```

Finally, the function <code>make_dashboard</code> will output an <code>.html</code> in your direictory, just like a <code>csv</code> file. The name of the file is <code>"index.html"</code> and it will be stored in the varable  <code>file_name</code>.


```python
file_name = "index.html"
```


```python
make_dashboard(x1['x'], gdp_change1['gdp_change'], unemployment1['unemployment'], title, file_name="index.html")
```








  <div class="bk-root" id="6e53e978-1a0b-4a4c-b50e-dc7899de4633" data-root-id="1003"></div>





Call the function <code>make_dashboard</code> , to produce a dashboard.  Assign the parameter values accordingly take a the <b>, take a screen shot of the dashboard and submit it</b>.


```python
# Fill up the parameters in the following function:
# make_dashboard(x=, gdp_change=, unemployment=, title=, file_name=)
```

<h3 id="Section_5">Question 5: Save the dashboard on IBM cloud and display it</h3>

From the tutorial <i>PROVISIONING AN OBJECT STORAGE INSTANCE ON IBM CLOUD</i> copy the JSON object containing the credentials you created. You’ll want to store everything you see in a credentials variable like the one below (obviously, replace the placeholder values with your own). Take special note of your <code>access_key_id</code> and <code>secret_access_key</code>. <b>Do not delete <code># @hidden_cell </code> as this will not allow people to see your credentials when you share your notebook. </b>

<code>
credentials = {<br>
 &nbsp; "apikey": "your-api-key",<br>
 &nbsp; "cos_hmac_keys": {<br>
 &nbsp;  "access_key_id": "your-access-key-here", <br>
 &nbsp;   "secret_access_key": "your-secret-access-key-here"<br>
 &nbsp; },<br>
</code>
<code>
   &nbsp;"endpoints": "your-endpoints",<br>
 &nbsp; "iam_apikey_description": "your-iam_apikey_description",<br>
 &nbsp; "iam_apikey_name": "your-iam_apikey_name",<br>
 &nbsp; "iam_role_crn": "your-iam_apikey_name",<br>
 &nbsp;  "iam_serviceid_crn": "your-iam_serviceid_crn",<br>
 &nbsp;"resource_instance_id": "your-resource_instance_id"<br>
}
</code>


```python
#The message you see below has been set up by Watson itself as I added ""@hidden_cell"
#in the beginning of the code to ensure that my keys are not shared just follow the 
#above code and insert your data as instructed.
```


```python
# The code was removed by Watson Studio for sharing.
```

You will need the endpoint make sure the setting are the same as <i> PROVISIONING AN OBJECT STORAGE INSTANCE ON IBM CLOUD </i> assign the name of your bucket to the variable  <code>bucket_name </code> 


```python
endpoint = 'https://s3-api.us-geo.objectstorage.softlayer.net'
```

From the tutorial <i> PROVISIONING AN OBJECT STORAGE INSTANCE ON IBM CLOUD </i> assign the name of your bucket to the variable  <code>bucket_name </code> 


```python
bucket_name ='useconomicdata-donotdelete-pr-pq7a4a7mcfl3gi' # Type your bucket name on IBM Cloud
```

We can access IBM Cloud Object Storage with Python useing the <code>boto3</code> library, which we’ll import below:


```python
import boto3
```

We can interact with IBM Cloud Object Storage through a <code>boto3</code> resource object.


```python
resource = boto3.resource(
    's3',
    aws_access_key_id = credentials["cos_hmac_keys"]['access_key_id'],
    aws_secret_access_key = credentials["cos_hmac_keys"]["secret_access_key"],
    endpoint_url = endpoint,
)
```

We are going to use  <code>open</code> to create a file object. To get the path of the file, you are going to concatenate the name of the file stored in the variable <code>file_name</code>. The directory stored in the variable directory using the <code>+</code> operator and assign it to the variable 
<code>html_path</code>. We will use the function <code>getcwd()</code> to find current the working directory.


```python
import os

directory = os.getcwd()
html_path = directory + "/" + "index.html"
```

Now you must read the html file, use the function <code>f = open(html_path, mode)</code> to create a file object and assign it to the variable <code>f</code>. The parameter <code>file</code> should be the variable <code>html_path</code>, the mode should be <code>"r"</code> for read. 


```python
# Type your code here
f = open(html_path, "r")
```

To load your dataset into the bucket we will use the method <code>put_object</code>, you must set the parameter name to the name of the bucket, the parameter <code>Key</code> should be the name of the HTML file and the value for the parameter Body  should be set to <code>f.read()</code>.


```python
# Fill up the parameters in the following function:
resource.Bucket(name='useconomicdata-donotdelete-pr-pq7a4a7mcfl3gi').put_object(Key="index.html", Body=f.read())
```




    s3.Object(bucket_name='useconomicdata-donotdelete-pr-pq7a4a7mcfl3gi', key='index.html')



In the dictionary <code>Params</code> provide the bucket name  as the value for the key <i>'Bucket'</i>. Also for the value of the key <i>'Key'</i> add the name of the <code>html</code> file, both values should be strings.


```python
# Fill in the value for each key
Params = {'Bucket':'useconomicdata-donotdelete-pr-pq7a4a7mcfl3gi' ,'Key': "index.html"}
```

The following lines of code will generate a URL to share your dashboard. The URL only last seven days, but don't worry you will get full marks if the URL is visible in your notebook.  


```python
import sys
time = 7*24*60**2
client = boto3.client(
    's3',
    aws_access_key_id = credentials["cos_hmac_keys"]['access_key_id'],
    aws_secret_access_key = credentials["cos_hmac_keys"]["secret_access_key"],
    endpoint_url=endpoint,

)
url = client.generate_presigned_url('get_object',Params=Params,ExpiresIn=time)
print(url)
```

    https://s3-api.us-geo.objectstorage.softlayer.net/useconomicdata-donotdelete-pr-pq7a4a7mcfl3gi/index.html?AWSAccessKeyId=8b64349d277341c6803494f4e507d4e5&Signature=oLBsa9hxo3rk5%2BtVJbULngxUvbY%3D&Expires=1563218486


<h2 id="Section_5">  How to submit </h2>

<p>Once you complete your notebook you will have to share it to be marked. Select the icon on the top right a marked in red in the image below, a dialogue box should open, select the option all&nbsp;content excluding sensitive code cells.</p>

<p><img height="440" width="700" src="https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/EdX/ReadMe%20files/share_noteook1.png" alt="share notebook" /></p>
<p></p>

<p>You can then share the notebook&nbsp; via a&nbsp; URL by scrolling down as shown in the following image:</p>
<p style="text-align: center;"> <img height="308" width="350" src="https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/PY0101EN/projects/EdX/ReadMe%20files/link2.png"  alt="share notebook" /> </p>

<h2>References :</h2> 

<ul>
 <il>
     1) <a href="https://research.stlouisfed.org/">Economic Research at the St. Louis Fed </a>:<a href="https://fred.stlouisfed.org/series/UNRATE/"> Civilian Unemployment Rate</a>
   </il>   
    <p>
     <il>
    2) <a href="https://github.com/datasets">Data Packaged Core Datasets
       </a>
   </il> 
    </p>
    
</ul>
</div>
