# [Nov 2022] Python for Time Series Data Analysis


<p align="right"> <a 
href="https://stackoverflow.com/users/18680621/sam-taylor" target="_blank"><img alt="StackOverflow" 
src="https://stackoverflow-badge.vercel.app/?userID=18680621" /></a> <a 
href="https://github.com/SamTaylor92" target="_blank"><img alt="Github" 
src="https://img.shields.io/badge/GitHub-181717.svg?style=for-the-badge&logo=GitHub&logoColor=white" /></a> <a 
href="https://www.linkedin.com/in/samjamest" target="_blank"><img alt="LinkedIn" 
src="https://img.shields.io/badge/LinkedIn-0A66C2.svg?style=for-the-badge&logo=LinkedIn&logoColor=white" /></a> <a 
href="https://signal.group/#CjQKIO50NLkjJmSisbgDD4OhRj5lHG7X-SJTOl-Dn8Fkc4FpEhCYdnCVL1ok4DlVNntY3mGe" target="_blank"><img alt="Signal" src="https://img.shields.io/badge/Signal-3A76F0.svg?style=for-the-badge&logo=Signal&logoColor=white"/></a> <a 
href="mailto:samtaylor92@live.co.uk" target="_blank"><img alt="Email" src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" /></a>
</p>
<p align="right">

## Description
This is a repository to highlight certain parts of the [Python for Time Series Data Analysis](https://www.udemy.com/course/python-for-time-series-data-analysis) course, and record some of the key skills and concepts covered.<br><br>

<p align="center">
  <img src="https://user-images.githubusercontent.com/105542266/198875156-7e28b2ca-a0b8-43d2-8bea-57e9433104b3.png">
</p>

<h2> Tools</h2>
<p>
<a target="_blank"><img alt="Jupyter Notebook" src="https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white"/></a> 
<a target="_blank"><img alt="Python" src="https://img.shields.io/badge/Python-3776AB.svg?style=for-the-badge&logo=Python&logoColor=white"/></a> 
<a target="_blank"><img alt="Pandas" src="https://img.shields.io/badge/pandas-150458.svg?style=for-the-badge&logo=pandas&logoColor=white"/></a>
<a target="_blank"><img alt="matplotlib" src="https://img.shields.io/badge/matplotlib-13324B.svg?style=for-the-badge&logo=ChartMogul&logoColor=white"/></a>
<a target="_blank"><img alt="statsmodels" src="https://img.shields.io/badge/Statsmodels-8CAAE6.svg?style=for-the-badge&logo=SciPy&logoColor=white"/></a>
</p>

<details open>
<summary> <h2>Table of contents</h2></summary>	

- [Repository description](#description)
- [Exponential smoothing](#exponential-smoothing)
  - [Task](#-task-)
  - [Solution](#solution)
- [Evaluating forecasting models](#evaluating-forecasting-models)
  - [Code](#-code-)
- [Stationarity test: adfuller](#stationarity-test-adfuller)
  - [Code](#-code--1)
- [Causality test: granger](#causality-test-granger)
  - [Code](#-code--2)
- [Forecasting: SARIMAX](#forecasting-sarimax)
  - [Code](#-code--3)
- [Reference material](#reference-material)

</details>

<details open>
<summary> <h2>📈Exponential smoothing</h2> </summary>
  
This part of the course asked me to apply concepts for exponential smoothing, using statsmodels.tsa.  

<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🎯Task </h3> </summary>

> For this set of exercises we're using data from the Federal Reserve Economic Database (FRED) concerning the Industrial Production Index for Electricity and Gas Utilities from January 1970 to December 1989.<br><br>
> Data source: https://fred.stlouisfed.org/series/IPG2211A2N
>
> `To do:`
> - Import the data
> - Set a date index and assign a frequency to the DatetimeIndex.
> - Add a 12-month Simple Moving Average (SMA)
> - Add a 12-month Exponentially Weighted Moving Average (EWMA)
> - Use a Holt-Winters fitted model & Triple Exponential Smoothing (TES)
> - Plot the above
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	  
  
</details>  
  
<details open>
<summary> <h3>💡Solution</h3> </summary>

`Repository:` [(Link)](https://github.com/SamTaylor92/Python_for_time_series_data_analysis/blob/main/Exponential-smoothing.ipynb)<br> 
`Notes:` Repository contains the Jupyter notebook and CSV datasets

![Screenshot 2022-10-30 at 11 37 13](https://user-images.githubusercontent.com/105542266/198874278-4b50495f-7732-4ed4-86ad-fbe1805bed70.png)
<p align="right"> [Simple & triple exponential smoothing]</p>

</details>  
</details>
</details>
</details>

<details open>
<summary> <h2>🤔Evaluating forecasting models</h2> </summary>

<br> There are three common ways to evaluate a forecasting model: <br> 
- `Mean Squared Error (MSE)`
- `Root Mean Squared Error (RMSE)`
  - Minimizing the RMSE will lead to forecasts of the mean.
- `Mean Absolute Error (MAE)`
  - A forecast method that minimizes the MAE will lead to forecasts of the median.

Most people use RMSE for the main metric for evaluating predictions. <br>
It punishes larger values and stays in the same units as the original data
<br>
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🐍Code </h3> </summary>

```python    
#Create a dataset
  
import numpy as np
import pandas as pd

np.random.seed(42)
df = pd.DataFrame(np.random.randint(20,30,(50,2)),
                  columns=['test','predictions'])
df.plot(figsize=(12,4));
``` 

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/105542266/200584412-0b68546b-57ce-43fe-bd73-e7c6f7d5962f.png" alt="Example dataset plot">
</p>         

```python
#Evaluate the predictions
  
from statsmodels.tools.eval_measures import mse, rmse, meanabs

MSE = mse(df['test'],df['predictions']) 
RMSE = rmse(df['test'],df['predictions'])
MAE = meanabs(df['test'],df['predictions'])

print(f'Model Mean Squared Error (MSE): {MSE:.3f}')
print(f'Model Root Mean Squared Error (RMSE): {RMSE:.3f}')
print(f'Model Mean Absolute Error (MAE): {MAE:.3f}')
```                        
<br>
  
<p align="center">
  <img src="https://user-images.githubusercontent.com/105542266/200585575-52aea2cd-4d79-4b30-be7e-cb7e641e0d19.png" alt="Example dataset plot">
</p>           
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	    
  
</details>  
</details>
</details>
</details>

<details open>
<summary> <h2>👨🏼‍💻Stationarity test: adfuller</h2> </summary>
  
The Adfuller method allows us to look for stationarity within a dataset.<br>
- Essentially, does a timeseries dataset remain stationary (similar mean and variance) across time, regardless of trends and potential noise?<br>

This is a function for printing a more user friendly adfuller report in python. 
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🐍Code </h3> </summary>

```python    
from statsmodels.tsa.stattools import adfuller
    
def adf_test(series,title=''):
    """
    Pass in a time series and an optional title, returns an ADF report
    """
print(f'Augmented Dickey-Fuller Test: {title}')
result = adfuller(series.dropna(),autolag='AIC') # .dropna() handles differenced data
    
labels = ['ADF test statistic','p-value','# lags used','# observations']
out = pd.Series(result[0:4],index=labels)

for key,val in result[4].items():
    out[f'critical value ({key})']=val
        
print(out.to_string())          # .to_string() removes the line "dtype: float64"
    
if result[1] <= 0.05:
    print("Strong evidence against the null hypothesis")
    print("Reject the null hypothesis")
    print("Data has no unit root and is stationary")
else:
    print("Weak evidence against the null hypothesis")
    print("Fail to reject the null hypothesis")
    print("Data has a unit root and is non-stationary")

# To use, type: 
# adf_test(dataframe['column_name'])
```                        
<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/105542266/200164346-8912b8e2-696e-4646-9da6-30281e59d176.png" img width="494" alt="Example adfuller test"            >
</p>         
                    
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	    
  
</details>  
</details>
</details>
</details>

<details open>
<summary> <h2>👨🏼‍💻Causality test: granger</h2> </summary>
  
The Granger causality test is a a hypothesis test to determine if one time series is useful in forecasting another. <br>It observes changes in one series and sees if these changes are correlated to changes in another after a consistent amount of time. 
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🐍Code </h3> </summary>

`Dataset:` [[samples.csv]](https://github.com/SamTaylor92/Python_for_time_series_data_analysis/blob/main/samples.csv)

```python
#Import a dataset & set index to datetime and assign a datetime frequency

df3 = pd.read_csv('../Data/samples.csv',
                  index_col=0,
                  parse_dates=True)
    
df3.index.freq = 'MS'
    
df3[['a','d']].plot(figsize=(16,5));
```
    
![Screenshot 2022-11-08 at 13 56 53](https://user-images.githubusercontent.com/105542266/200572391-0201b062-8eb8-4685-909b-5d090f336565.png)

```python
# Import the statistical package needed
# Add a semicolon at the end to avoid duplicate output
    
from statsmodels.tsa.stattools import grangercausalitytests
    
grangercausalitytests(df3[['a','d']],
                      maxlag=3);
```

![Screenshot 2022-11-08 at 13 57 10](https://user-images.githubusercontent.com/105542266/200572424-3a0a9fb0-7e30-4ba5-a9da-1066968d3f09.png)

```python
# A visual representation of the correlation found
# Two days after something happens with column a, the data in column d reacts.

df3['a'].iloc[2:].plot(figsize=(16,5),
                       legend=True);
    
df3['d'].shift(2).plot(legend=True);   
```

![Screenshot 2022-11-08 at 13 57 19](https://user-images.githubusercontent.com/105542266/200572592-915dc35e-dbed-4440-8e67-79eb40f11645.png)
                      

<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	    

<details open>
<summary> <h2>📈Forecasting: SARIMAX</h2> </summary>
  
A piece of code to be used as a template for seasonal forecasting with an exogenous variable using SARIMAX.
  
![Screenshot 2022-12-21 at 11 32 54](https://user-images.githubusercontent.com/105542266/208884677-f2dae7d4-2d9a-4313-ac8e-5138af5b6aea.png)
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🐍Code </h3> </summary>

`Code:` [[Code Snippet]](https://gist.github.com/SamTaylor92/2b0d6b018074fdd58388a429582c5410#file-sarimax_template-py)
  
![Screenshot 2022-12-21 at 11 35 09](https://user-images.githubusercontent.com/105542266/208884884-dec0485b-abd9-4957-b0a2-1c1f07ef0be8.png)
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
</details>  
</details>
</details>
</details>

<details open>
<summary> <h3>📚Reference material</h3> </summary>
  
- [x] [Python for Time Series Data Analysis](https://www.udemy.com/course/python-for-time-series-data-analysis/)
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	

</details>
</details>

</p>

</br></br>
© 2022 GitHub, Inc.
Terms
Privacy
