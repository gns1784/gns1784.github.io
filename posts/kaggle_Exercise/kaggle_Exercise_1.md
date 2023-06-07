---
layout: posts
title: "Kaggle Exercise 1"
author: "Sin dong hun"
date: "2023-06-01"
---

```python
# 패키지 설치
!pip install geopandas
```

    Looking in indexes: https://pypi.org/simple, https://us-python.pkg.dev/colab-wheels/public/simple/
    Collecting geopandas
      Downloading geopandas-0.13.0-py3-none-any.whl (1.1 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m1.1/1.1 MB[0m [31m14.6 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting fiona>=1.8.19 (from geopandas)
      Downloading Fiona-1.9.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.5 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m16.5/16.5 MB[0m [31m57.9 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: packaging in /usr/local/lib/python3.10/dist-packages (from geopandas) (23.1)
    Requirement already satisfied: pandas>=1.1.0 in /usr/local/lib/python3.10/dist-packages (from geopandas) (1.5.3)
    Collecting pyproj>=3.0.1 (from geopandas)
      Downloading pyproj-3.5.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (7.7 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m7.7/7.7 MB[0m [31m55.9 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: shapely>=1.7.1 in /usr/local/lib/python3.10/dist-packages (from geopandas) (2.0.1)
    Requirement already satisfied: attrs>=19.2.0 in /usr/local/lib/python3.10/dist-packages (from fiona>=1.8.19->geopandas) (23.1.0)
    Requirement already satisfied: certifi in /usr/local/lib/python3.10/dist-packages (from fiona>=1.8.19->geopandas) (2022.12.7)
    Requirement already satisfied: click~=8.0 in /usr/local/lib/python3.10/dist-packages (from fiona>=1.8.19->geopandas) (8.1.3)
    Collecting click-plugins>=1.0 (from fiona>=1.8.19->geopandas)
      Downloading click_plugins-1.1.1-py2.py3-none-any.whl (7.5 kB)
    Collecting cligj>=0.5 (from fiona>=1.8.19->geopandas)
      Downloading cligj-0.7.2-py3-none-any.whl (7.1 kB)
    Requirement already satisfied: six in /usr/local/lib/python3.10/dist-packages (from fiona>=1.8.19->geopandas) (1.16.0)
    Requirement already satisfied: python-dateutil>=2.8.1 in /usr/local/lib/python3.10/dist-packages (from pandas>=1.1.0->geopandas) (2.8.2)
    Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.10/dist-packages (from pandas>=1.1.0->geopandas) (2022.7.1)
    Requirement already satisfied: numpy>=1.21.0 in /usr/local/lib/python3.10/dist-packages (from pandas>=1.1.0->geopandas) (1.22.4)
    Installing collected packages: pyproj, cligj, click-plugins, fiona, geopandas
    Successfully installed click-plugins-1.1.1 cligj-0.7.2 fiona-1.9.4 geopandas-0.13.0 pyproj-3.5.0
    


```python
import geopandas as gpd
```


```python
from google.colab import drive
drive.mount('/content/drive')
```

    Mounted at /content/drive
    


```python
# Read in the data
full_data = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/DEC_lands/DEC_lands")

# View the first five rows of the data
full_data.head()
```





  <div id="df-4df60d81-3f7c-4795-ac97-c34189c6535d">
    <div class="colab-df-container">
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
      <th>OBJECTID</th>
      <th>CATEGORY</th>
      <th>UNIT</th>
      <th>FACILITY</th>
      <th>CLASS</th>
      <th>UMP</th>
      <th>DESCRIPTIO</th>
      <th>REGION</th>
      <th>COUNTY</th>
      <th>URL</th>
      <th>SOURCE</th>
      <th>UPDATE_</th>
      <th>OFFICE</th>
      <th>ACRES</th>
      <th>LANDS_UID</th>
      <th>GREENCERT</th>
      <th>SHAPE_AREA</th>
      <th>SHAPE_LEN</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>FOR PRES DET PAR</td>
      <td>CFP</td>
      <td>HANCOCK FP DETACHED PARCEL</td>
      <td>WILD FOREST</td>
      <td>NaN</td>
      <td>DELAWARE COUNTY DETACHED PARCEL</td>
      <td>4</td>
      <td>DELAWARE</td>
      <td>http://www.dec.ny.gov/</td>
      <td>DELAWARE RPP</td>
      <td>5/12</td>
      <td>STAMFORD</td>
      <td>738.620192</td>
      <td>103</td>
      <td>N</td>
      <td>2.990365e+06</td>
      <td>7927.662385</td>
      <td>POLYGON ((486093.245 4635308.586, 486787.235 4...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>FOR PRES DET PAR</td>
      <td>CFP</td>
      <td>HANCOCK FP DETACHED PARCEL</td>
      <td>WILD FOREST</td>
      <td>NaN</td>
      <td>DELAWARE COUNTY DETACHED PARCEL</td>
      <td>4</td>
      <td>DELAWARE</td>
      <td>http://www.dec.ny.gov/</td>
      <td>DELAWARE RPP</td>
      <td>5/12</td>
      <td>STAMFORD</td>
      <td>282.553140</td>
      <td>1218</td>
      <td>N</td>
      <td>1.143940e+06</td>
      <td>4776.375600</td>
      <td>POLYGON ((491931.514 4637416.256, 491305.424 4...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>FOR PRES DET PAR</td>
      <td>CFP</td>
      <td>HANCOCK FP DETACHED PARCEL</td>
      <td>WILD FOREST</td>
      <td>NaN</td>
      <td>DELAWARE COUNTY DETACHED PARCEL</td>
      <td>4</td>
      <td>DELAWARE</td>
      <td>http://www.dec.ny.gov/</td>
      <td>DELAWARE RPP</td>
      <td>5/12</td>
      <td>STAMFORD</td>
      <td>234.291262</td>
      <td>1780</td>
      <td>N</td>
      <td>9.485476e+05</td>
      <td>5783.070364</td>
      <td>POLYGON ((486000.287 4635834.453, 485007.550 4...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>FOR PRES DET PAR</td>
      <td>CFP</td>
      <td>GREENE COUNTY FP DETACHED PARCEL</td>
      <td>WILD FOREST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>GREENE</td>
      <td>http://www.dec.ny.gov/</td>
      <td>GREENE RPP</td>
      <td>5/12</td>
      <td>STAMFORD</td>
      <td>450.106464</td>
      <td>2060</td>
      <td>N</td>
      <td>1.822293e+06</td>
      <td>7021.644833</td>
      <td>POLYGON ((541716.775 4675243.268, 541217.579 4...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>FOREST PRESERVE</td>
      <td>AFP</td>
      <td>SARANAC LAKES WILD FOREST</td>
      <td>WILD FOREST</td>
      <td>SARANAC LAKES</td>
      <td>NaN</td>
      <td>5</td>
      <td>ESSEX</td>
      <td>http://www.dec.ny.gov/lands/22593.html</td>
      <td>DECRP, ESSEX RPP</td>
      <td>12/96</td>
      <td>RAY BROOK</td>
      <td>69.702387</td>
      <td>1517</td>
      <td>N</td>
      <td>2.821959e+05</td>
      <td>2663.909932</td>
      <td>POLYGON ((583896.043 4909643.187, 583891.200 4...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-4df60d81-3f7c-4795-ac97-c34189c6535d')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-4df60d81-3f7c-4795-ac97-c34189c6535d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4df60d81-3f7c-4795-ac97-c34189c6535d');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
type(full_data)
```




    geopandas.geodataframe.GeoDataFrame




```python
data = full_data.loc[:, ["CLASS", "COUNTY", "geometry"]].copy()
```


```python
# How many lands of each type are there?
data.CLASS.value_counts()
```




    WILD FOREST                   965
    INTENSIVE USE                 108
    PRIMITIVE                      60
    WILDERNESS                     52
    ADMINISTRATIVE                 17
    UNCLASSIFIED                    7
    HISTORIC                        5
    PRIMITIVE BICYCLE CORRIDOR      4
    CANOE AREA                      1
    Name: CLASS, dtype: int64




```python
# Select lands that fall under the "WILD FOREST" or "WILDERNESS" category
wild_lands = data.loc[data.CLASS.isin(['WILD FOREST', 'WILDERNESS'])].copy()
wild_lands.head()
```





  <div id="df-e5d51f9f-14d8-4f90-8fdd-ae6320e1f0ec">
    <div class="colab-df-container">
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
      <th>CLASS</th>
      <th>COUNTY</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>WILD FOREST</td>
      <td>DELAWARE</td>
      <td>POLYGON ((486093.245 4635308.586, 486787.235 4...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WILD FOREST</td>
      <td>DELAWARE</td>
      <td>POLYGON ((491931.514 4637416.256, 491305.424 4...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>WILD FOREST</td>
      <td>DELAWARE</td>
      <td>POLYGON ((486000.287 4635834.453, 485007.550 4...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>WILD FOREST</td>
      <td>GREENE</td>
      <td>POLYGON ((541716.775 4675243.268, 541217.579 4...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>WILD FOREST</td>
      <td>ESSEX</td>
      <td>POLYGON ((583896.043 4909643.187, 583891.200 4...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e5d51f9f-14d8-4f90-8fdd-ae6320e1f0ec')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-e5d51f9f-14d8-4f90-8fdd-ae6320e1f0ec button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e5d51f9f-14d8-4f90-8fdd-ae6320e1f0ec');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
wild_lands.plot()
```




    <Axes: >




    
![png](output_8_1.png)
    



```python
# View the first five entries in the "geometry" column
wild_lands.geometry.head()
```




    0    POLYGON ((486093.245 4635308.586, 486787.235 4...
    1    POLYGON ((491931.514 4637416.256, 491305.424 4...
    2    POLYGON ((486000.287 4635834.453, 485007.550 4...
    3    POLYGON ((541716.775 4675243.268, 541217.579 4...
    4    POLYGON ((583896.043 4909643.187, 583891.200 4...
    Name: geometry, dtype: geometry




```python
# Campsites in New York state (Point) 
POI_data = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/DEC_pointsinterest/DEC_pointsinterest")
campsites = POI_data.loc[POI_data.ASSET=='PRIMITIVE CAMPSITE'].copy()

# Foot trails in New York state (LineString)
roads_trails = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/DEC_roadstrails/DEC_roadstrails")
trails = roads_trails.loc[roads_trails.ASSET=='FOOT TRAIL'].copy()

# County boundaries in New York state (Polygon)
counties = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/NY_county_boundaries/NY_county_boundaries")
```


```python
# Define a base map with county boundaries
ax = counties.plot(figsize=(10,10), color='none', edgecolor='gainsboro', zorder=3)

# Add wild lands, campsites, and foot trails to the base map
wild_lands.plot(color='lightgreen', ax=ax)
campsites.plot(color='maroon', markersize=2, ax=ax)
trails.plot(color='black', markersize=1, ax=ax)
```




    <Axes: >




    
![png](output_11_1.png)
    


# 비영리 단체가 사업을 확장할 수 있는 필리핀의 외딴 지역을 직접 찾아보세요.

1) 데이터를 가져옵니다.
다음 셀을 사용하여 loans_filepath에 있는 모양 파일을 로드하여 GeoDataFrame world_loans를 만듭니다.


```python
loans_filepath = "/content/drive/MyDrive/2023 데이터마이닝/archive/kiva_loans/kiva_loans/kiva_loans.shp"


# Your code here: Load the data
world_loans = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/kiva_loans/kiva_loans/kiva_loans.shp")
# Check your answer
world_loans.head()

# ("/content/drive/MyDrive/2023 데이터마이닝/archive/kiva_loans/kiva_loans")
```





  <div id="df-a23db36f-dd5e-46df-b794-60d9e3084083">
    <div class="colab-df-container">
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
      <th>Partner ID</th>
      <th>Field Part</th>
      <th>sector</th>
      <th>Loan Theme</th>
      <th>country</th>
      <th>amount</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9</td>
      <td>KREDIT Microfinance Institution</td>
      <td>General Financial Inclusion</td>
      <td>Higher Education</td>
      <td>Cambodia</td>
      <td>450</td>
      <td>POINT (102.89751 13.66726)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>KREDIT Microfinance Institution</td>
      <td>General Financial Inclusion</td>
      <td>Vulnerable Populations</td>
      <td>Cambodia</td>
      <td>20275</td>
      <td>POINT (102.98962 13.02870)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>KREDIT Microfinance Institution</td>
      <td>General Financial Inclusion</td>
      <td>Higher Education</td>
      <td>Cambodia</td>
      <td>9150</td>
      <td>POINT (102.98962 13.02870)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>KREDIT Microfinance Institution</td>
      <td>General Financial Inclusion</td>
      <td>Vulnerable Populations</td>
      <td>Cambodia</td>
      <td>604950</td>
      <td>POINT (105.31312 12.09829)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>KREDIT Microfinance Institution</td>
      <td>General Financial Inclusion</td>
      <td>Sanitation</td>
      <td>Cambodia</td>
      <td>275</td>
      <td>POINT (105.31312 12.09829)</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a23db36f-dd5e-46df-b794-60d9e3084083')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a23db36f-dd5e-46df-b794-60d9e3084083 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a23db36f-dd5e-46df-b794-60d9e3084083');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




2) 데이터를 플롯합니다.
다음 코드 셀을 변경하지 않고 실행하여 국가 경계가 포함된 지오데이터프레임 월드를 로드합니다.


```python
# This dataset is provided in GeoPandas
world_filepath = gpd.datasets.get_path('naturalearth_lowres')
world = gpd.read_file(world_filepath)
world.head()
```

    <ipython-input-16-8d5431ffd4fc>:2: FutureWarning: The geopandas.dataset module is deprecated and will be removed in GeoPandas 1.0. You can get the original 'naturalearth_lowres' data from https://www.naturalearthdata.com/downloads/110m-cultural-vectors/.
      world_filepath = gpd.datasets.get_path('naturalearth_lowres')
    





  <div id="df-5f44c007-a6a1-4173-944c-5cfecb02aa76">
    <div class="colab-df-container">
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
      <th>pop_est</th>
      <th>continent</th>
      <th>name</th>
      <th>iso_a3</th>
      <th>gdp_md_est</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>889953.0</td>
      <td>Oceania</td>
      <td>Fiji</td>
      <td>FJI</td>
      <td>5496</td>
      <td>MULTIPOLYGON (((180.00000 -16.06713, 180.00000...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>58005463.0</td>
      <td>Africa</td>
      <td>Tanzania</td>
      <td>TZA</td>
      <td>63177</td>
      <td>POLYGON ((33.90371 -0.95000, 34.07262 -1.05982...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>603253.0</td>
      <td>Africa</td>
      <td>W. Sahara</td>
      <td>ESH</td>
      <td>907</td>
      <td>POLYGON ((-8.66559 27.65643, -8.66512 27.58948...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>37589262.0</td>
      <td>North America</td>
      <td>Canada</td>
      <td>CAN</td>
      <td>1736425</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -122.9742...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>328239523.0</td>
      <td>North America</td>
      <td>United States of America</td>
      <td>USA</td>
      <td>21433226</td>
      <td>MULTIPOLYGON (((-122.84000 49.00000, -120.0000...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5f44c007-a6a1-4173-944c-5cfecb02aa76')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-5f44c007-a6a1-4173-944c-5cfecb02aa76 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5f44c007-a6a1-4173-944c-5cfecb02aa76');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




3) 필리핀에 기반을 둔 대출을 선택합니다.
다음으로 필리핀에 소재한 대출에 집중하겠습니다. 다음 코드 셀을 사용하여 필리핀을 기반으로 하는 대출이 있는 world_loans의 모든 행을 포함하는 GeoDataFrame PHL_loans를 만듭니다.


```python
world.plot()
```




    <Axes: >




    
![png](output_18_1.png)
    



```python
### Your code here
world_data = world.plot()
world_loans.plot(ax=world_data, color='red', markersize=0.1)
```




    <Axes: >




    
![png](output_19_1.png)
    



```python
# Your code here
PHL_loans = world_loans.loc[world_loans['country'] =='Philippines']
PHL_loans.head()
```





  <div id="df-44149490-c2dd-4812-8be6-bb92c35b502e">
    <div class="colab-df-container">
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
      <th>Partner ID</th>
      <th>Field Part</th>
      <th>sector</th>
      <th>Loan Theme</th>
      <th>country</th>
      <th>amount</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2859</th>
      <td>123</td>
      <td>Alalay sa Kaunlaran (ASKI)</td>
      <td>General Financial Inclusion</td>
      <td>General</td>
      <td>Philippines</td>
      <td>400</td>
      <td>POINT (121.73961 17.64228)</td>
    </tr>
    <tr>
      <th>2860</th>
      <td>123</td>
      <td>Alalay sa Kaunlaran (ASKI)</td>
      <td>General Financial Inclusion</td>
      <td>General</td>
      <td>Philippines</td>
      <td>400</td>
      <td>POINT (121.74169 17.63235)</td>
    </tr>
    <tr>
      <th>2861</th>
      <td>123</td>
      <td>Alalay sa Kaunlaran (ASKI)</td>
      <td>General Financial Inclusion</td>
      <td>General</td>
      <td>Philippines</td>
      <td>400</td>
      <td>POINT (121.46667 16.60000)</td>
    </tr>
    <tr>
      <th>2862</th>
      <td>123</td>
      <td>Alalay sa Kaunlaran (ASKI)</td>
      <td>General Financial Inclusion</td>
      <td>General</td>
      <td>Philippines</td>
      <td>6050</td>
      <td>POINT (121.73333 17.83333)</td>
    </tr>
    <tr>
      <th>2863</th>
      <td>123</td>
      <td>Alalay sa Kaunlaran (ASKI)</td>
      <td>General Financial Inclusion</td>
      <td>General</td>
      <td>Philippines</td>
      <td>625</td>
      <td>POINT (121.51800 16.72368)</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-44149490-c2dd-4812-8be6-bb92c35b502e')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-44149490-c2dd-4812-8be6-bb92c35b502e button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-44149490-c2dd-4812-8be6-bb92c35b502e');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# Load a KML file containing island boundaries
gpd.io.file.fiona.drvsupport.supported_drivers['KML'] = 'rw'
PHL = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/Philippines_AL258.kml")
PHL.head()
```





  <div id="df-08f695f9-90a5-44c3-bac5-d9e174a898c9">
    <div class="colab-df-container">
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
      <th>Name</th>
      <th>Description</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Autonomous Region in Muslim Mindanao</td>
      <td></td>
      <td>MULTIPOLYGON (((119.46690 4.58718, 119.46653 4...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bicol Region</td>
      <td></td>
      <td>MULTIPOLYGON (((124.04577 11.57862, 124.04594 ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Cagayan Valley</td>
      <td></td>
      <td>MULTIPOLYGON (((122.51581 17.04436, 122.51568 ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Calabarzon</td>
      <td></td>
      <td>MULTIPOLYGON (((120.49202 14.05403, 120.49201 ...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Caraga</td>
      <td></td>
      <td>MULTIPOLYGON (((126.45401 8.24400, 126.45407 8...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-08f695f9-90a5-44c3-bac5-d9e174a898c9')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-08f695f9-90a5-44c3-bac5-d9e174a898c9 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-08f695f9-90a5-44c3-bac5-d9e174a898c9');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
# Your code here
PHL = PHL.plot()
PHL_loans.plot(ax=PHL, color='red', markersize=0.2)
```




    <Axes: >




    
![png](output_22_1.png)
    



```python

```
