
<a><img src="https://ibm.box.com/shared/static/ugcqz6ohbvff804xp84y4kqnvvk3bq1g.png" width="200" align="center"></a>

<h1>Analyzing US Economic Data and  Building a Dashboard  </h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some essential economic indicators from some data, you will then display these economic indicators in a Dashboard. You can then share the dashboard via an URL.
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
        <li><a href="#Section_6"><b>(Optional not marked)</b> Save the dashboard on IBM cloud and display it</a></li>
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
df_gdp = pd.read_csv(links['GDP'])
```

Use the method <code>head()</code> to display the first five rows of the GDP data, then take a screen-shot.


```python
# Type your code here
df_gdp.head()
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



<h3 id="Section_2"> Question 2: Create a dataframe that contains the unemployment data. Display the first five rows of the dataframe. </h3>

Use the dictionary <code>links</code> and the function <code>pd.read_csv</code> to create a Pandas dataframes that contains the unemployment data.


```python
# Type your code here
df_unemp = pd.read_csv(links['unemployment'])
```

Use the method <code>head()</code> to display the first five rows of the GDP data, then take a screen-shot.


```python
# Type your code here
df_unemp.head()
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



<h3 id="Section_3">Question 3: Display a dataframe where unemployment was greater than 8.5%. Take a screen-shot.</h3>


```python
# Type your code here
df_unemp_percent = df_unemp[df_unemp['unemployment'] > 8.5]
df_unemp_percent
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
x = df_gdp['date']
```

Create a new dataframe with the column <code>'change-current' </code> called <code>gdp_change</code>  from the dataframe that contains the GDP data.


```python
gdp_change = df_gdp['change-current']
```

Create a new dataframe with the column <code>'unemployment' </code> called <code>unemployment</code>  from the dataframe that contains the  unemployment data.


```python
unemployment = df_unemp['unemployment']
```

Give your dashboard a string title, and assign it to the variable <code>title</code>


```python
title = 'US Economic Data'
```

Finally, the function <code>make_dashboard</code> will output an <code>.html</code> in your direictory, just like a <code>csv</code> file. The name of the file is <code>"index.html"</code> and it will be stored in the varable  <code>file_name</code>.


```python
file_name = "index.html"
```

Call the function <code>make_dashboard</code> , to produce a dashboard.  Assign the parameter values accordingly take a the <b>, take a screen shot of the dashboard and submit it</b>.


```python
# Fill up the parameters in the following function:
make_dashboard(x=x, gdp_change=gdp_change, unemployment=unemployment, title=title, file_name=file_name)
```








  <div class="bk-root" id="4d832ec5-bd30-4d11-b26a-758985ec8dc0" data-root-id="1003"></div>





<h3 id="Section_5"> <b>(Optional not marked)</b>Save the dashboard on IBM cloud and display it  </h3>

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
# @hidden_cell
credentials = {
  "apikey": "OraKWr4Hqx_U5nrf4ZEc7maCYhIWgCl2CWdQVNzlWQHd",
  "cos_hmac_keys": {
    "access_key_id": "c308429fdb9d42d7ac1e2b003271c371",
    "secret_access_key": "899b8a86f459114e61ffb57f5ea77ac01edcef82360c9859"
  },
  "endpoints": "https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints",
  "iam_apikey_description": "Auto-generated for key c308429f-db9d-42d7-ac1e-2b003271c371",
  "iam_apikey_name": "WDP-Project-Management-f1526e6f-10ae-486d-b00b-3ea1ba25cd0d",
  "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",
  "iam_serviceid_crn": "crn:v1:bluemix:public:iam-identity::a/b98c0e2de37145e783293266f592227f::serviceid:ServiceId-5556a4a4-53b4-4cc3-9c6b-acc7e6add46f",
  "resource_instance_id": "crn:v1:bluemix:public:cloud-object-storage:global:a/b98c0e2de37145e783293266f592227f:f1526e6f-10ae-486d-b00b-3ea1ba25cd0d::"
}
```

You will need the endpoint make sure the setting are the same as <i> PROVISIONING AN OBJECT STORAGE INSTANCE ON IBM CLOUD </i> assign the name of your bucket to the variable  <code>bucket_name </code> 


```python
endpoint = 'https://s3.eu.cloud-object-storage.appdomain.cloud'
```

From the tutorial <i> PROVISIONING AN OBJECT STORAGE INSTANCE ON IBM CLOUD </i> assign the name of your bucket to the variable  <code>bucket_name </code> 


```python
bucket_name = 'dataanalysisused-donotdelete-pr-fv7o3xoyg9n8uu'
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
html_path = directory + "/" + file_name
```

Now you must read the html file, use the function <code>f = open(html_path, mode)</code> to create a file object and assign it to the variable <code>f</code>. The parameter <code>file</code> should be the variable <code>html_path</code>, the mode should be <code>"r"</code> for read. 


```python
f = open(html_path, "r")
```

To load your dataset into the bucket we will use the method <code>put_object</code>, you must set the parameter name to the name of the bucket, the parameter <code>Key</code> should be the name of the HTML file and the value for the parameter Body  should be set to <code>f.read()</code>.


```python
# Fill up the parameters in the following function:
resource.Bucket(name=bucket_name).put_object(Key=file_name, Body=f.read())
```




    s3.Object(bucket_name='dataanalysisused-donotdelete-pr-fv7o3xoyg9n8uu', key='index.html')



In the dictionary <code>Params</code> provide the bucket name  as the value for the key <i>'Bucket'</i>. Also for the value of the key <i>'Key'</i> add the name of the <code>html</code> file, both values should be strings.


```python
# Fill in the value for each key
Params = {'Bucket': bucket_name ,'Key': file_name}
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

    https://s3.eu.cloud-object-storage.appdomain.cloud/dataanalysisused-donotdelete-pr-fv7o3xoyg9n8uu/index.html?AWSAccessKeyId=c308429fdb9d42d7ac1e2b003271c371&Signature=WiaA1J0VbMgH7gXUIpg241SMN8w%3D&Expires=1587294248

