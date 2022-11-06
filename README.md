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
This is a repository to highlight certain parts of the [Python for Time Series Data Analysis](https://www.udemy.com/course/python-for-time-series-data-analysis) course, to highlights some of the key skills and concepts covered.<br><br>

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
- [ADFULLER function: test for seasonaily](#adfuller-function-test-for-seasonaily)
  - [Code](#-code-)
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
<summary> <h2>👨🏼‍💻ADFULLER function: test for seasonaily</h2> </summary>
  
This is a function for printing a more user friendly adfuller report in python. 

<img width="494" alt="Screenshot 2022-11-06 at 10 53 01" src="https://user-images.githubusercontent.com/105542266/200164346-8912b8e2-696e-4646-9da6-30281e59d176.png">  
  
<p align='right'><a href="#-tools" target="_blank">⬆</a></p>	
  
<details open>  
  
<summary> <h3> 🐍Code </h3> </summary>

    
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
