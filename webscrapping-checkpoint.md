```python
import selenium
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
SLEEP_EACH_SCROLL = 3
count, limit      = 0, 30 # if we want to stop
import regex as re
import time
gecko = 'C:\seleniumWebDrivers'
browser = webdriver.Firefox(gecko)
browser.get('https://beds24.com/control2.php')
username = browser.find_element_by_name('username')
username.send_keys('')

password = browser.find_element_by_name('loginpass')
password.send_keys('')
browser.find_element_by_name('dosubmit').click()
browser.find_element_by_name('submittoday').click()
browser.get('https://beds24.com/control2.php?pagetype=calendar')
browser.find_element_by_name('showfor').click()
browser.find_element_by_xpath("//option[@value='0']").click()




```


```python
appart = browser.find_elements_by_xpath('//div[@class="dashgrid_rowroomname"]')
appart
```




    [<selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="3384584f-2556-4fe8-be2f-e8a4bc28bc17")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="7c50fafd-7c58-4731-ad58-d8f52bc47125")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="8248ddf3-1dd2-4326-9d0b-5c5b7e5776bc")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="f3a21d1c-14f1-474c-9e0e-9d8dfda4b578")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="35d8591d-a770-4c84-a727-6e3633a5fa2a")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="07303c83-6208-491d-9a64-0f4c213fec01")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="7291e0da-1863-4f38-8ffe-5b84f0e233f3")>]




```python
n = len(appart)
n
```




    7




```python
a = [appart[i].text for i in range(n)]
a
```




    ['Au Vert et Bleu de Créteil',
     "L'hypercentre de Suresnes",
     "Le Confort d'Antony",
     'Le Cosy Montreuil',
     'Un Coin de Tournage',
     'Villiers sur Marne 1',
     'Villiers sur Marne 2']




```python
jour = browser.find_elements_by_xpath('//span[@class="smalldatetext"]')
jour
now = time.strftime("%x")
```


```python
j = [jour[i].text + " " + now for i in range(n) ]
j
```




    [' Tue 02/09/21',
     ' Tue 02/09/21',
     ' Tue 02/09/21',
     ' Tue 02/09/21',
     ' Tue 02/09/21',
     ' Tue 02/09/21',
     ' Tue 02/09/21']




```python
inventory = browser.find_elements_by_xpath('//div[@class="dashgrid_inventory pointer" or @class="dashgrid_inventory_na pointer"]')
inventory

```




    [<selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="57669644-d7c3-43d6-bc72-5d37fe4848f9")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="882a2c16-5e30-4fca-8e31-7b13acbf38ac")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="0389d23e-f294-4e68-962f-2788cc8fa20d")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="80ab0146-d9e1-4716-8714-1fe27fec9999")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="3a66b840-c9ad-402d-aad7-5630b87727ac")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="1987640b-0193-4568-bd3c-518dda958a31")>,
     <selenium.webdriver.firefox.webelement.FirefoxWebElement (session="71952461-ebb6-4099-ba2d-1bd0d58413f1", element="3337d376-a23c-432a-80e0-fb30357d7a2b")>]




```python
i = [inventory[i].text for i in range(n)]
i
```




    ['0', '1', '0', '0', '1', '1', '1']




```python
import pandas as pd
```


```python
df = pd.DataFrame()
df['appart'] = a
df
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
      <th>appart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Au Vert et Bleu de Créteil</td>
    </tr>
    <tr>
      <th>1</th>
      <td>L'hypercentre de Suresnes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Le Confort d'Antony</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Le Cosy Montreuil</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Un Coin de Tournage</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Villiers sur Marne 1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Villiers sur Marne 2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["jours"] =j
df["disponibilite"] = i
df
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
      <th>appart</th>
      <th>jours</th>
      <th>disponibilite</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Au Vert et Bleu de Créteil</td>
      <td>Tue 02/09/21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>L'hypercentre de Suresnes</td>
      <td>Tue 02/09/21</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Le Confort d'Antony</td>
      <td>Tue 02/09/21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Le Cosy Montreuil</td>
      <td>Tue 02/09/21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Un Coin de Tournage</td>
      <td>Tue 02/09/21</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Villiers sur Marne 1</td>
      <td>Tue 02/09/21</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Villiers sur Marne 2</td>
      <td>Tue 02/09/21</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
import os
cwd = os.getcwd()
```


```python
cwd
```




    'D:\\ESILV\\semestre1\\python for data analysis\\.ipynb_checkpoints\\.ipynb_checkpoints'




```python
df.to_csv(r'bulletin_du_jour.csv',index=False)
```


```python

```
