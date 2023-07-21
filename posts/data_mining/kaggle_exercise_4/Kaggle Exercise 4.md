---
layout: posts
title: "Kaggle Exercise 4"
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
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m1.1/1.1 MB[0m [31m20.3 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting fiona>=1.8.19 (from geopandas)
      Downloading Fiona-1.9.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.5 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m16.5/16.5 MB[0m [31m53.1 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: packaging in /usr/local/lib/python3.10/dist-packages (from geopandas) (23.1)
    Requirement already satisfied: pandas>=1.1.0 in /usr/local/lib/python3.10/dist-packages (from geopandas) (1.5.3)
    Collecting pyproj>=3.0.1 (from geopandas)
      Downloading pyproj-3.5.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (7.7 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m7.7/7.7 MB[0m [31m64.9 MB/s[0m eta [36m0:00:00[0m
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
from geopy.geocoders import Nominatim
import pandas as pd
import numpy as np
import folium
from folium import Marker
import warnings 
warnings.filterwarnings('ignore')
from geopy.geocoders import Nominatim
```


```python
geolocator = Nominatim(user_agent="kaggle_learn")
location = geolocator.geocode("Pyramid of Khufu")

print(location.point)
print(location.address)
```

    29 58m 44.976s N, 31 8m 3.17625s E
    هرم خوفو, شارع ابو الهول السياحي, نزلة البطران, الجيزة, 12125, مصر
    


```python
point = location.point
print("Latitude:", point.latitude)
print("Longitude:", point.longitude)

```

    Latitude: 29.97916
    Longitude: 31.134215625236113
    


```python
universities = pd.read_csv("/content/drive/MyDrive/2023 데이터마이닝/archive/top_universities.csv")
universities.head()
```





  <div id="df-e7ab6bb6-e3c9-4bdc-a613-3742399d935b">
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>University of Oxford</td>
    </tr>
    <tr>
      <th>1</th>
      <td>University of Cambridge</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Imperial College London</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ETH Zurich</td>
    </tr>
    <tr>
      <th>4</th>
      <td>UCL</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-e7ab6bb6-e3c9-4bdc-a613-3742399d935b')"
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
          document.querySelector('#df-e7ab6bb6-e3c9-4bdc-a613-3742399d935b button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-e7ab6bb6-e3c9-4bdc-a613-3742399d935b');
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
def my_geocoder(row):
    try:
        point = geolocator.geocode(row).point
        return pd.Series({'Latitude': point.latitude, 'Longitude': point.longitude})
    except:
        return None
# try - except : 실패 시에 대비하여서 값 설정

universities[['Latitude', 'Longitude']] = universities.apply(lambda x: my_geocoder(x['Name']), axis=1)

print("{}% of addresses were geocoded!".format(
    (1 - sum(np.isnan(universities["Latitude"])) / len(universities)) * 100))

# Drop universities that were not successfully geocoded
universities = universities.loc[~np.isnan(universities["Latitude"])]
universities = gpd.GeoDataFrame(
    universities, geometry=gpd.points_from_xy(universities.Longitude, universities.Latitude))
universities.crs = {'init': 'epsg:4326'}
universities.head()
```

    91.0% of addresses were geocoded!
    





  <div id="df-830ecbbd-f364-4e0a-a7a9-0202ab53d574">
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
      <th>Latitude</th>
      <th>Longitude</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>University of Oxford</td>
      <td>51.759037</td>
      <td>-1.252430</td>
      <td>POINT (-1.25243 51.75904)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>University of Cambridge</td>
      <td>52.200623</td>
      <td>0.110474</td>
      <td>POINT (0.11047 52.20062)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Imperial College London</td>
      <td>51.498959</td>
      <td>-0.175641</td>
      <td>POINT (-0.17564 51.49896)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ETH Zurich</td>
      <td>47.408327</td>
      <td>8.507564</td>
      <td>POINT (8.50756 47.40833)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>UCL</td>
      <td>51.521785</td>
      <td>-0.135151</td>
      <td>POINT (-0.13515 51.52179)</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-830ecbbd-f364-4e0a-a7a9-0202ab53d574')"
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
          document.querySelector('#df-830ecbbd-f364-4e0a-a7a9-0202ab53d574 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-830ecbbd-f364-4e0a-a7a9-0202ab53d574');
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
# Create a map
m = folium.Map(location=[54, 15], tiles='openstreetmap', zoom_start=2)

# Add points to the map
for idx, row in universities.iterrows():
    Marker([row['Latitude'], row['Longitude']], popup=row['Name']).add_to(m)

# Display the map
m
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe srcdoc="&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;

    &lt;meta http-equiv=&quot;content-type&quot; content=&quot;text/html; charset=UTF-8&quot; /&gt;

        &lt;script&gt;
            L_NO_TOUCH = false;
            L_DISABLE_3D = false;
        &lt;/script&gt;

    &lt;style&gt;html, body {width: 100%;height: 100%;margin: 0;padding: 0;}&lt;/style&gt;
    &lt;style&gt;#map {position:absolute;top:0;bottom:0;right:0;left:0;}&lt;/style&gt;
    &lt;script src=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://code.jquery.com/jquery-1.12.4.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.js&quot;&gt;&lt;/script&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/npm/leaflet@1.9.3/dist/leaflet.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.2.0/css/all.min.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdnjs.cloudflare.com/ajax/libs/Leaflet.awesome-markers/2.0.2/leaflet.awesome-markers.css&quot;/&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;https://cdn.jsdelivr.net/gh/python-visualization/folium/folium/templates/leaflet.awesome.rotate.min.css&quot;/&gt;

            &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width,
                initial-scale=1.0, maximum-scale=1.0, user-scalable=no&quot; /&gt;
            &lt;style&gt;
                #map_4dcffdb3531d39924ea28668635b9ad5 {
                    position: relative;
                    width: 100.0%;
                    height: 100.0%;
                    left: 0.0%;
                    top: 0.0%;
                }
                .leaflet-container { font-size: 1rem; }
            &lt;/style&gt;

&lt;/head&gt;
&lt;body&gt;


            &lt;div class=&quot;folium-map&quot; id=&quot;map_4dcffdb3531d39924ea28668635b9ad5&quot; &gt;&lt;/div&gt;

&lt;/body&gt;
&lt;script&gt;


            var map_4dcffdb3531d39924ea28668635b9ad5 = L.map(
                &quot;map_4dcffdb3531d39924ea28668635b9ad5&quot;,
                {
                    center: [54.0, 15.0],
                    crs: L.CRS.EPSG3857,
                    zoom: 2,
                    zoomControl: true,
                    preferCanvas: false,
                }
            );





            var tile_layer_115d53a0a7b65311f64e67bcb9413670 = L.tileLayer(
                &quot;https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png&quot;,
                {&quot;attribution&quot;: &quot;Data by \u0026copy; \u003ca target=\&quot;_blank\&quot; href=\&quot;http://openstreetmap.org\&quot;\u003eOpenStreetMap\u003c/a\u003e, under \u003ca target=\&quot;_blank\&quot; href=\&quot;http://www.openstreetmap.org/copyright\&quot;\u003eODbL\u003c/a\u003e.&quot;, &quot;detectRetina&quot;: false, &quot;maxNativeZoom&quot;: 18, &quot;maxZoom&quot;: 18, &quot;minZoom&quot;: 0, &quot;noWrap&quot;: false, &quot;opacity&quot;: 1, &quot;subdomains&quot;: &quot;abc&quot;, &quot;tms&quot;: false}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


            var marker_d0ffcb8a7f5a9ce4713c641b6619393b = L.marker(
                [51.7590373, -1.2524298],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_302ad1d7474ef04ac35f77acd68f64bc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e524046103764c369dbd8c96dae23055 = $(`&lt;div id=&quot;html_e524046103764c369dbd8c96dae23055&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Oxford&lt;/div&gt;`)[0];
                popup_302ad1d7474ef04ac35f77acd68f64bc.setContent(html_e524046103764c369dbd8c96dae23055);



        marker_d0ffcb8a7f5a9ce4713c641b6619393b.bindPopup(popup_302ad1d7474ef04ac35f77acd68f64bc)
        ;




            var marker_d6adda3a76ce8cc551aec5ab2f65b8a0 = L.marker(
                [52.2006233, 0.1104744],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_bc30c892a9b3f0c203cf77a056ab2846 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f058f9f799ebb58d932e96eb57ce7fae = $(`&lt;div id=&quot;html_f058f9f799ebb58d932e96eb57ce7fae&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Cambridge&lt;/div&gt;`)[0];
                popup_bc30c892a9b3f0c203cf77a056ab2846.setContent(html_f058f9f799ebb58d932e96eb57ce7fae);



        marker_d6adda3a76ce8cc551aec5ab2f65b8a0.bindPopup(popup_bc30c892a9b3f0c203cf77a056ab2846)
        ;




            var marker_2b66522670a83b96f7aa4d4bcc72e443 = L.marker(
                [51.4989595, -0.17564069276310426],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_0792994757a2b72eedf3abc520515cda = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_6fc02932b93bed3dc8f176605f3e5f68 = $(`&lt;div id=&quot;html_6fc02932b93bed3dc8f176605f3e5f68&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Imperial College London&lt;/div&gt;`)[0];
                popup_0792994757a2b72eedf3abc520515cda.setContent(html_6fc02932b93bed3dc8f176605f3e5f68);



        marker_2b66522670a83b96f7aa4d4bcc72e443.bindPopup(popup_0792994757a2b72eedf3abc520515cda)
        ;




            var marker_f32c1eec40dc48b224b34e631385d38b = L.marker(
                [47.40832745, 8.507563966360525],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_c65afa88820fea60997a14a25772205a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_3f94fcae37e573fbf1bafd57952c0b1b = $(`&lt;div id=&quot;html_3f94fcae37e573fbf1bafd57952c0b1b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;ETH Zurich&lt;/div&gt;`)[0];
                popup_c65afa88820fea60997a14a25772205a.setContent(html_3f94fcae37e573fbf1bafd57952c0b1b);



        marker_f32c1eec40dc48b224b34e631385d38b.bindPopup(popup_c65afa88820fea60997a14a25772205a)
        ;




            var marker_0eba939744642887e66f45249d78b820 = L.marker(
                [51.5217852, -0.13515149671251314],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e23e8c50acd9992c31ed79d18a256072 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_b5a6becd648c0ee2df6114221e1c4b6c = $(`&lt;div id=&quot;html_b5a6becd648c0ee2df6114221e1c4b6c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;UCL&lt;/div&gt;`)[0];
                popup_e23e8c50acd9992c31ed79d18a256072.setContent(html_b5a6becd648c0ee2df6114221e1c4b6c);



        marker_0eba939744642887e66f45249d78b820.bindPopup(popup_e23e8c50acd9992c31ed79d18a256072)
        ;




            var marker_6dce7b3d8b6fdd34cb7c52cfff32924a = L.marker(
                [51.5143114, -0.11678105481073275],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_387d80af5eb2ceb883ef9552a0daaf41 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_502dbea34ace6a36075a8f14d2ebbcec = $(`&lt;div id=&quot;html_502dbea34ace6a36075a8f14d2ebbcec&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;London School of Economics and Political Science&lt;/div&gt;`)[0];
                popup_387d80af5eb2ceb883ef9552a0daaf41.setContent(html_502dbea34ace6a36075a8f14d2ebbcec);



        marker_6dce7b3d8b6fdd34cb7c52cfff32924a.bindPopup(popup_387d80af5eb2ceb883ef9552a0daaf41)
        ;




            var marker_fff3c79ca3825f90efe4d49121846258 = L.marker(
                [55.94407645, -3.1883735563964555],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_07893126b1a0f2d304972aefd6e423ca = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f85bd32664ce0d486e748b942257afdb = $(`&lt;div id=&quot;html_f85bd32664ce0d486e748b942257afdb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Edinburgh&lt;/div&gt;`)[0];
                popup_07893126b1a0f2d304972aefd6e423ca.setContent(html_f85bd32664ce0d486e748b942257afdb);



        marker_fff3c79ca3825f90efe4d49121846258.bindPopup(popup_07893126b1a0f2d304972aefd6e423ca)
        ;




            var marker_8ed84eca0b1d274e61a20fb9ce669623 = L.marker(
                [48.2469873, 11.544935443359439],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e652012e2f463b4e209fe76cf9618ad1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_43afe39d8d76b47c85b56adf67fbdf2e = $(`&lt;div id=&quot;html_43afe39d8d76b47c85b56adf67fbdf2e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;LMU Munich&lt;/div&gt;`)[0];
                popup_e652012e2f463b4e209fe76cf9618ad1.setContent(html_43afe39d8d76b47c85b56adf67fbdf2e);



        marker_8ed84eca0b1d274e61a20fb9ce669623.bindPopup(popup_e652012e2f463b4e209fe76cf9618ad1)
        ;




            var marker_54b3fecaf032174b75655e7d19e24cf4 = L.marker(
                [46.518659400000004, 6.566561505148001],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_64897c8b19570bf8b22004e1edc28185 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_53f31036d34c35e48c77ca1a03540403 = $(`&lt;div id=&quot;html_53f31036d34c35e48c77ca1a03540403&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;École Polytechnique Fédérale de Lausanne&lt;/div&gt;`)[0];
                popup_64897c8b19570bf8b22004e1edc28185.setContent(html_53f31036d34c35e48c77ca1a03540403);



        marker_54b3fecaf032174b75655e7d19e24cf4.bindPopup(popup_64897c8b19570bf8b22004e1edc28185)
        ;




            var marker_007468496a7833c79b5226b6cffcfe7b = L.marker(
                [51.5060001, -0.1121582948025203],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_a1732a54efa6c45b76a8ed3c77509b42 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_29af97991741690241e86365688cb53e = $(`&lt;div id=&quot;html_29af97991741690241e86365688cb53e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;King’s College London&lt;/div&gt;`)[0];
                popup_a1732a54efa6c45b76a8ed3c77509b42.setContent(html_29af97991741690241e86365688cb53e);



        marker_007468496a7833c79b5226b6cffcfe7b.bindPopup(popup_a1732a54efa6c45b76a8ed3c77509b42)
        ;




            var marker_f5cd995f5a729e969f9c89e167c1d4d7 = L.marker(
                [59.219549549999996, 17.94005487275674],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_b344863068f18e21fa0f6cf74fe581ec = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e4cffdb6cff9123574f6676105ec5903 = $(`&lt;div id=&quot;html_e4cffdb6cff9123574f6676105ec5903&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Karolinska Institute&lt;/div&gt;`)[0];
                popup_b344863068f18e21fa0f6cf74fe581ec.setContent(html_e4cffdb6cff9123574f6676105ec5903);



        marker_f5cd995f5a729e969f9c89e167c1d4d7.bindPopup(popup_b344863068f18e21fa0f6cf74fe581ec)
        ;




            var marker_aa3bd1f606d5401ef432c9023a692652 = L.marker(
                [1.3078539, 103.7776795],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_50703b2fcafa6a530d349268b472721c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4182a6bce1793076c405d380bd45a8ea = $(`&lt;div id=&quot;html_4182a6bce1793076c405d380bd45a8ea&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Technical University of Munich&lt;/div&gt;`)[0];
                popup_50703b2fcafa6a530d349268b472721c.setContent(html_4182a6bce1793076c405d380bd45a8ea);



        marker_aa3bd1f606d5401ef432c9023a692652.bindPopup(popup_50703b2fcafa6a530d349268b472721c)
        ;




            var marker_31df42370cd5a9823d0146d01df7796b = L.marker(
                [41.11442525, -83.16686666639325],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_127a06de8b36f7039fbb65847a456d90 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_1c5a9ffa9a6e96cf1d535c0ad84a8748 = $(`&lt;div id=&quot;html_1c5a9ffa9a6e96cf1d535c0ad84a8748&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Heidelberg University&lt;/div&gt;`)[0];
                popup_127a06de8b36f7039fbb65847a456d90.setContent(html_1c5a9ffa9a6e96cf1d535c0ad84a8748);



        marker_31df42370cd5a9823d0146d01df7796b.bindPopup(popup_127a06de8b36f7039fbb65847a456d90)
        ;




            var marker_17dd5a357dfb79975d1e85d47f4724c7 = L.marker(
                [50.80571285, 3.2915374489139757],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_48d3a1c97e4363c6c38a39391452959c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_d2625e631434b8b6a8a82d203af2dfac = $(`&lt;div id=&quot;html_d2625e631434b8b6a8a82d203af2dfac&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;KU Leuven&lt;/div&gt;`)[0];
                popup_48d3a1c97e4363c6c38a39391452959c.setContent(html_d2625e631434b8b6a8a82d203af2dfac);



        marker_17dd5a357dfb79975d1e85d47f4724c7.bindPopup(popup_48d3a1c97e4363c6c38a39391452959c)
        ;




            var marker_1ee930a5e7b58450753fa1ef0892f46c = L.marker(
                [53.4657087, -2.232734319907597],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8b57b19d79235799a8833090250911bd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_cc3cbb3df6b88b175baa3bc6302bfe04 = $(`&lt;div id=&quot;html_cc3cbb3df6b88b175baa3bc6302bfe04&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Manchester&lt;/div&gt;`)[0];
                popup_8b57b19d79235799a8833090250911bd.setContent(html_cc3cbb3df6b88b175baa3bc6302bfe04);



        marker_1ee930a5e7b58450753fa1ef0892f46c.bindPopup(popup_8b57b19d79235799a8833090250911bd)
        ;




            var marker_fa66a0622aa7c63c3d73e3d005249b5c = L.marker(
                [51.99882735, 4.373960368154041],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_dde664c9378bcc419c6d4ce77a1be349 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_b8699d3ca070554b80b07458e8139b93 = $(`&lt;div id=&quot;html_b8699d3ca070554b80b07458e8139b93&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Delft University of Technology&lt;/div&gt;`)[0];
                popup_dde664c9378bcc419c6d4ce77a1be349.setContent(html_b8699d3ca070554b80b07458e8139b93);



        marker_fa66a0622aa7c63c3d73e3d005249b5c.bindPopup(popup_dde664c9378bcc419c6d4ce77a1be349)
        ;




            var marker_b9f64e05b4a30c2b3fc81415f4481c14 = L.marker(
                [51.98544495, 5.663212001137484],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6f80dd778293423a82460e57626e8d49 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_6cb5fb1fd106ed9f74a300660f77a60a = $(`&lt;div id=&quot;html_6cb5fb1fd106ed9f74a300660f77a60a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Wageningen University &amp; Research&lt;/div&gt;`)[0];
                popup_6f80dd778293423a82460e57626e8d49.setContent(html_6cb5fb1fd106ed9f74a300660f77a60a);



        marker_b9f64e05b4a30c2b3fc81415f4481c14.bindPopup(popup_6f80dd778293423a82460e57626e8d49)
        ;




            var marker_bc6e1b782ae95755c97a690aa855aef2 = L.marker(
                [52.36813335, 4.889804155733945],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_a459e4c4b55a236636cfd0c818c8876f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_1a80497ba867fdd3b16fee03ea208c50 = $(`&lt;div id=&quot;html_1a80497ba867fdd3b16fee03ea208c50&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Amsterdam&lt;/div&gt;`)[0];
                popup_a459e4c4b55a236636cfd0c818c8876f.setContent(html_1a80497ba867fdd3b16fee03ea208c50);



        marker_bc6e1b782ae95755c97a690aa855aef2.bindPopup(popup_a459e4c4b55a236636cfd0c818c8876f)
        ;




            var marker_aac39b2d9447436884e2e83305849020 = L.marker(
                [52.5183402, 13.392920232320172],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_7f7c9338f460648f858267d786794e21 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_339e347a6b3ab6a45542951a92f7081c = $(`&lt;div id=&quot;html_339e347a6b3ab6a45542951a92f7081c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Humboldt University of Berlin&lt;/div&gt;`)[0];
                popup_7f7c9338f460648f858267d786794e21.setContent(html_339e347a6b3ab6a45542951a92f7081c);



        marker_aac39b2d9447436884e2e83305849020.bindPopup(popup_7f7c9338f460648f858267d786794e21)
        ;




            var marker_e12086641466bd6a7fbc056bb675121b = L.marker(
                [52.168633850000006, 4.45966305742133],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_706f03532ca96360d961150dc87b23a5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e3cc9b65fc9912b82d296b8e8839c298 = $(`&lt;div id=&quot;html_e3cc9b65fc9912b82d296b8e8839c298&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Leiden University&lt;/div&gt;`)[0];
                popup_706f03532ca96360d961150dc87b23a5.setContent(html_e3cc9b65fc9912b82d296b8e8839c298);



        marker_e12086641466bd6a7fbc056bb675121b.bindPopup(popup_706f03532ca96360d961150dc87b23a5)
        ;




            var marker_a346e29282f8739b0a8247bbad0e2fb6 = L.marker(
                [51.9229171, 4.487612362865811],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_073b7d56ea3237fa46cb427b01d5a6d5 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_671d97a8b42addb0575cf301f0beef32 = $(`&lt;div id=&quot;html_671d97a8b42addb0575cf301f0beef32&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Erasmus University Rotterdam&lt;/div&gt;`)[0];
                popup_073b7d56ea3237fa46cb427b01d5a6d5.setContent(html_671d97a8b42addb0575cf301f0beef32);



        marker_a346e29282f8739b0a8247bbad0e2fb6.bindPopup(popup_073b7d56ea3237fa46cb427b01d5a6d5)
        ;




            var marker_1341e4af89ff3b2fa3ad16d25230d2a8 = L.marker(
                [48.846899699999994, 2.357448653115875],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_d6383c54519d657253f04e73c0d7b41e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e3d219e2d41cd28341cd5e2452c7bd72 = $(`&lt;div id=&quot;html_e3d219e2d41cd28341cd5e2452c7bd72&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Sorbonne University&lt;/div&gt;`)[0];
                popup_d6383c54519d657253f04e73c0d7b41e.setContent(html_e3d219e2d41cd28341cd5e2452c7bd72);



        marker_1341e4af89ff3b2fa3ad16d25230d2a8.bindPopup(popup_d6383c54519d657253f04e73c0d7b41e)
        ;




            var marker_561d265557329d123d869a82a495ec2e = L.marker(
                [52.08340265, 5.148315067762755],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_74e7b714acb970d7a18d2e9fd8445710 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_13af81bfdbd8080e12b8ffe3afa9e1d6 = $(`&lt;div id=&quot;html_13af81bfdbd8080e12b8ffe3afa9e1d6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Utrecht University&lt;/div&gt;`)[0];
                popup_74e7b714acb970d7a18d2e9fd8445710.setContent(html_13af81bfdbd8080e12b8ffe3afa9e1d6);



        marker_561d265557329d123d869a82a495ec2e.bindPopup(popup_74e7b714acb970d7a18d2e9fd8445710)
        ;




            var marker_cee9eed16f583487613cb394fb5e480e = L.marker(
                [46.793058, 7.157106],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_1437eb0e9b36a13ac91b247ea8f251fc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_0bde101f4466490d647c9f62b2cd0ecb = $(`&lt;div id=&quot;html_0bde101f4466490d647c9f62b2cd0ecb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Freiburg&lt;/div&gt;`)[0];
                popup_1437eb0e9b36a13ac91b247ea8f251fc.setContent(html_0bde101f4466490d647c9f62b2cd0ecb);



        marker_cee9eed16f583487613cb394fb5e480e.bindPopup(popup_1437eb0e9b36a13ac91b247ea8f251fc)
        ;




            var marker_246996bf110ab269bbb17e9f36791ed8 = L.marker(
                [51.457609649999995, -2.6016348983421755],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_f82aa555853c634e638958b8035a76ce = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_457371e2fe0ad18de6c301f264d6f99d = $(`&lt;div id=&quot;html_457371e2fe0ad18de6c301f264d6f99d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Bristol&lt;/div&gt;`)[0];
                popup_f82aa555853c634e638958b8035a76ce.setContent(html_457371e2fe0ad18de6c301f264d6f99d);



        marker_246996bf110ab269bbb17e9f36791ed8.bindPopup(popup_f82aa555853c634e638958b8035a76ce)
        ;




            var marker_c5bbda3413b180aec66cfcad43474695 = L.marker(
                [53.21967825, 6.562514810379012],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_3cf8edaf9fb9975d890dd24c622ba263 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_3251e3d2cf437380d47651161c2b94cc = $(`&lt;div id=&quot;html_3251e3d2cf437380d47651161c2b94cc&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Groningen&lt;/div&gt;`)[0];
                popup_3cf8edaf9fb9975d890dd24c622ba263.setContent(html_3251e3d2cf437380d47651161c2b94cc);



        marker_c5bbda3413b180aec66cfcad43474695.bindPopup(popup_3cf8edaf9fb9975d890dd24c622ba263)
        ;




            var marker_b670287b58d73041fc6cd8c74330b0ab = L.marker(
                [52.3813073, -1.5639569481637439],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_48b0c845f01d1bf7305edb9b5c77cc9c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e780bc0ba37b722fc5ef99754eb64222 = $(`&lt;div id=&quot;html_e780bc0ba37b722fc5ef99754eb64222&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Warwick&lt;/div&gt;`)[0];
                popup_48b0c845f01d1bf7305edb9b5c77cc9c.setContent(html_e780bc0ba37b722fc5ef99754eb64222);



        marker_b670287b58d73041fc6cd8c74330b0ab.bindPopup(popup_48b0c845f01d1bf7305edb9b5c77cc9c)
        ;




            var marker_f16cd2b20c56b6e9e76523d71b610ed5 = L.marker(
                [50.7791645, 6.068920971222876],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_ebdf995e44e7dabab2b1daba447df336 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_0703dfc6bf869db9821bb58150c150e1 = $(`&lt;div id=&quot;html_0703dfc6bf869db9821bb58150c150e1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;RWTH Aachen University&lt;/div&gt;`)[0];
                popup_ebdf995e44e7dabab2b1daba447df336.setContent(html_0703dfc6bf869db9821bb58150c150e1);



        marker_f16cd2b20c56b6e9e76523d71b610ed5.bindPopup(popup_ebdf995e44e7dabab2b1daba447df336)
        ;




            var marker_29fdef448722dc3d99891fe98362e430 = L.marker(
                [59.8617859, 17.6376705],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_7c1200058ff712f193911915d363cef1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_0b540de29cb8b2589089417380ca6101 = $(`&lt;div id=&quot;html_0b540de29cb8b2589089417380ca6101&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Uppsala University&lt;/div&gt;`)[0];
                popup_7c1200058ff712f193911915d363cef1.setContent(html_0b540de29cb8b2589089417380ca6101);



        marker_29fdef448722dc3d99891fe98362e430.bindPopup(popup_7c1200058ff712f193911915d363cef1)
        ;




            var marker_a15504f80382b7cf72c54cfbec040e0e = L.marker(
                [48.53405945, 9.071244429234808],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_f7c490fd1ef671389a27f3b019b2fecc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4059d1af7e094308057ef0425a6e2904 = $(`&lt;div id=&quot;html_4059d1af7e094308057ef0425a6e2904&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Tübingen&lt;/div&gt;`)[0];
                popup_f7c490fd1ef671389a27f3b019b2fecc.setContent(html_4059d1af7e094308057ef0425a6e2904);



        marker_a15504f80382b7cf72c54cfbec040e0e.bindPopup(popup_f7c490fd1ef671389a27f3b019b2fecc)
        ;




            var marker_3a08e35d69e0da614739728e5a7d630d = L.marker(
                [52.5299885, 13.34866394036122],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_43608d71a6239653fea9b765343d825d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_6ba263e965fb9c1b7800c61326b10dfa = $(`&lt;div id=&quot;html_6ba263e965fb9c1b7800c61326b10dfa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Charité - Universitätsmedizin Berlin&lt;/div&gt;`)[0];
                popup_43608d71a6239653fea9b765343d825d.setContent(html_6ba263e965fb9c1b7800c61326b10dfa);



        marker_3a08e35d69e0da614739728e5a7d630d.bindPopup(popup_43608d71a6239653fea9b765343d825d)
        ;




            var marker_7e46ad46b67e4840fc7df0225a504df3 = L.marker(
                [47.49684345, 8.72980716809498],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_fcbd9e635faf38c7e26776ce678d2c85 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4cc720ab58f7ceed5a698c92b0430754 = $(`&lt;div id=&quot;html_4cc720ab58f7ceed5a698c92b0430754&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Zurich&lt;/div&gt;`)[0];
                popup_fcbd9e635faf38c7e26776ce678d2c85.setContent(html_4cc720ab58f7ceed5a698c92b0430754);



        marker_7e46ad46b67e4840fc7df0225a504df3.bindPopup(popup_fcbd9e635faf38c7e26776ce678d2c85)
        ;




            var marker_c074f16d43eb8b61a569fa5aa98b03ae = L.marker(
                [55.872315349999994, -4.289219112981823],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_7f10ccf9f543e82e5858c23b6e28bd00 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_ad79977c26c7a6378d708aca78be3688 = $(`&lt;div id=&quot;html_ad79977c26c7a6378d708aca78be3688&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Glasgow&lt;/div&gt;`)[0];
                popup_7f10ccf9f543e82e5858c23b6e28bd00.setContent(html_ad79977c26c7a6378d708aca78be3688);



        marker_c074f16d43eb8b61a569fa5aa98b03ae.bindPopup(popup_7f10ccf9f543e82e5858c23b6e28bd00)
        ;




            var marker_77f334fee002713812b7414ee13468e9 = L.marker(
                [55.7126504, 13.210758659399971],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_cea2b6fcb508fc0b3fdc7c219c996dfc = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_5e376e5d21abbca1e9c54d7b0d0f652e = $(`&lt;div id=&quot;html_5e376e5d21abbca1e9c54d7b0d0f652e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Lund University&lt;/div&gt;`)[0];
                popup_cea2b6fcb508fc0b3fdc7c219c996dfc.setContent(html_5e376e5d21abbca1e9c54d7b0d0f652e);



        marker_77f334fee002713812b7414ee13468e9.bindPopup(popup_cea2b6fcb508fc0b3fdc7c219c996dfc)
        ;




            var marker_9d7c7e66994eebb468898aa2f0147efb = L.marker(
                [60.175648300000006, 24.953550020522073],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8846d79f56a3ceb1907a48a9d23a0069 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_1d6f3c3522728a3e3c288fc7dcce34c1 = $(`&lt;div id=&quot;html_1d6f3c3522728a3e3c288fc7dcce34c1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Helsinki&lt;/div&gt;`)[0];
                popup_8846d79f56a3ceb1907a48a9d23a0069.setContent(html_1d6f3c3522728a3e3c288fc7dcce34c1);



        marker_9d7c7e66994eebb468898aa2f0147efb.bindPopup(popup_8846d79f56a3ceb1907a48a9d23a0069)
        ;




            var marker_5a5a29c299b081e5f6acc93cfb8ed392 = L.marker(
                [47.56174235, 7.58285513707386],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_3b92ea9556c5a092a548b106bb2b6c0b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_739daf9a3935ce9cce98014ecad71ddd = $(`&lt;div id=&quot;html_739daf9a3935ce9cce98014ecad71ddd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Basel&lt;/div&gt;`)[0];
                popup_3b92ea9556c5a092a548b106bb2b6c0b.setContent(html_739daf9a3935ce9cce98014ecad71ddd);



        marker_5a5a29c299b081e5f6acc93cfb8ed392.bindPopup(popup_3b92ea9556c5a092a548b106bb2b6c0b)
        ;




            var marker_b57a5f94216c20238fb78651946d2ef7 = L.marker(
                [53.3815327, -1.4806602],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_1c697d7defe3471426cb425bc91b9fdb = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4e2d46824cc455ba930ce5e068ed550c = $(`&lt;div id=&quot;html_4e2d46824cc455ba930ce5e068ed550c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Sheffield&lt;/div&gt;`)[0];
                popup_1c697d7defe3471426cb425bc91b9fdb.setContent(html_4e2d46824cc455ba930ce5e068ed550c);



        marker_b57a5f94216c20238fb78651946d2ef7.bindPopup(popup_1c697d7defe3471426cb425bc91b9fdb)
        ;




            var marker_a6b313232b79bac471dee85d24461122 = L.marker(
                [48.7127874, 2.2107453],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_46df9a53b2d938326c7b411ce89a7c5e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_5e1d7c82b1d05908636ba583d057ee84 = $(`&lt;div id=&quot;html_5e1d7c82b1d05908636ba583d057ee84&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;École Polytechnique&lt;/div&gt;`)[0];
                popup_46df9a53b2d938326c7b411ce89a7c5e.setContent(html_5e1d7c82b1d05908636ba583d057ee84);



        marker_a6b313232b79bac471dee85d24461122.bindPopup(popup_46df9a53b2d938326c7b411ce89a7c5e)
        ;




            var marker_cf9f013da2be07645e4c16e0b99efff0 = L.marker(
                [46.95097255, 7.438684130809055],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_ade53bfe61cca49fcb2c1176c3a09a4f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_2fc40066f3e0ad16f29b39d0de2fd844 = $(`&lt;div id=&quot;html_2fc40066f3e0ad16f29b39d0de2fd844&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Bern&lt;/div&gt;`)[0];
                popup_ade53bfe61cca49fcb2c1176c3a09a4f.setContent(html_2fc40066f3e0ad16f29b39d0de2fd844);



        marker_cf9f013da2be07645e4c16e0b99efff0.bindPopup(popup_ade53bfe61cca49fcb2c1176c3a09a4f)
        ;




            var marker_9156678df80e8e6535358dc87c1492f5 = L.marker(
                [50.7338124, 7.1022465],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_c507d9c60d268800e5f1a130f3533fac = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_238495f9a0b88e2c9a669c510ebdae3b = $(`&lt;div id=&quot;html_238495f9a0b88e2c9a669c510ebdae3b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Bonn&lt;/div&gt;`)[0];
                popup_c507d9c60d268800e5f1a130f3533fac.setContent(html_238495f9a0b88e2c9a669c510ebdae3b);



        marker_9156678df80e8e6535358dc87c1492f5.bindPopup(popup_c507d9c60d268800e5f1a130f3533fac)
        ;




            var marker_72b88982c61cae266d1afc56838c0485 = L.marker(
                [54.9027916, -1.392096],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6fa69f01f60c73dae3a84e222ac9268b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_c94380a96d157161b016192fecb3fe79 = $(`&lt;div id=&quot;html_c94380a96d157161b016192fecb3fe79&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Durham University&lt;/div&gt;`)[0];
                popup_6fa69f01f60c73dae3a84e222ac9268b.setContent(html_c94380a96d157161b016192fecb3fe79);



        marker_72b88982c61cae266d1afc56838c0485.bindPopup(popup_6fa69f01f60c73dae3a84e222ac9268b)
        ;




            var marker_b1a23fd33c3131faa7f0f0076bacfab3 = L.marker(
                [52.4522956, -1.9312856726008194],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_5d8427b50535447c1174e0bf182b4181 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_d793f14b8029bd256a474df89fad5bb1 = $(`&lt;div id=&quot;html_d793f14b8029bd256a474df89fad5bb1&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Birmingham&lt;/div&gt;`)[0];
                popup_5d8427b50535447c1174e0bf182b4181.setContent(html_d793f14b8029bd256a474df89fad5bb1);



        marker_b1a23fd33c3131faa7f0f0076bacfab3.bindPopup(popup_5d8427b50535447c1174e0bf182b4181)
        ;




            var marker_7a2de94561dce8d9a90e37857ee931e5 = L.marker(
                [55.6801502, 12.57232700140625],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_0fefdf9aa37aa74c57be0698313d961f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f151ece50fe7b0d17f16e3bb2beff41f = $(`&lt;div id=&quot;html_f151ece50fe7b0d17f16e3bb2beff41f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Copenhagen&lt;/div&gt;`)[0];
                popup_0fefdf9aa37aa74c57be0698313d961f.setContent(html_f151ece50fe7b0d17f16e3bb2beff41f);



        marker_7a2de94561dce8d9a90e37857ee931e5.bindPopup(popup_0fefdf9aa37aa74c57be0698313d961f)
        ;




            var marker_47fad0c54bef56ec48bb697af56a5021 = L.marker(
                [50.9354752, -1.3962847494297244],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_d57419e5364681c494f94666bd839566 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_82c25c0fba1c7250354a885d3cf64fc0 = $(`&lt;div id=&quot;html_82c25c0fba1c7250354a885d3cf64fc0&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Southampton&lt;/div&gt;`)[0];
                popup_d57419e5364681c494f94666bd839566.setContent(html_82c25c0fba1c7250354a885d3cf64fc0);



        marker_47fad0c54bef56ec48bb697af56a5021.bindPopup(popup_d57419e5364681c494f94666bd839566)
        ;




            var marker_1f98338487085f5980cf91ad8d94ad2a = L.marker(
                [53.9453903, -1.0314592943104675],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6680a7ea5e44a2b90be5ffbf7e900bd2 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f25432b93a45953ed438d0de69e0a3d6 = $(`&lt;div id=&quot;html_f25432b93a45953ed438d0de69e0a3d6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of York&lt;/div&gt;`)[0];
                popup_6680a7ea5e44a2b90be5ffbf7e900bd2.setContent(html_f25432b93a45953ed438d0de69e0a3d6);



        marker_1f98338487085f5980cf91ad8d94ad2a.bindPopup(popup_6680a7ea5e44a2b90be5ffbf7e900bd2)
        ;




            var marker_80bdef47deb2ec033a2a9e6c00ec6e9f = L.marker(
                [53.34366745, -6.254444724511822],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e4973241cd111d13afc258abf80d5d46 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_ed82288dc6ba825e1c5077c28fa8914e = $(`&lt;div id=&quot;html_ed82288dc6ba825e1c5077c28fa8914e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Trinity College Dublin&lt;/div&gt;`)[0];
                popup_e4973241cd111d13afc258abf80d5d46.setContent(html_ed82288dc6ba825e1c5077c28fa8914e);



        marker_80bdef47deb2ec033a2a9e6c00ec6e9f.bindPopup(popup_e4973241cd111d13afc258abf80d5d46)
        ;




            var marker_29552ccc9eddf8c50bfd5d316df31c57 = L.marker(
                [59.9414173, 10.722768340750914],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_b0cc48f7e0c8d32dd2ca2786a8be9d15 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_9deab27297bf5dcce4746c406ccfbbf2 = $(`&lt;div id=&quot;html_9deab27297bf5dcce4746c406ccfbbf2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Oslo&lt;/div&gt;`)[0];
                popup_b0cc48f7e0c8d32dd2ca2786a8be9d15.setContent(html_9deab27297bf5dcce4746c406ccfbbf2);



        marker_29552ccc9eddf8c50bfd5d316df31c57.bindPopup(popup_b0cc48f7e0c8d32dd2ca2786a8be9d15)
        ;




            var marker_153d7bb4f52e983bc20fbae873332bfa = L.marker(
                [56.1670905, 10.202617693592895],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_c3fb2a5ccb6cf9cc86095a5c8c90a30b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_41c59c845b552546f282471ca009ae60 = $(`&lt;div id=&quot;html_41c59c845b552546f282471ca009ae60&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Aarhus University&lt;/div&gt;`)[0];
                popup_c3fb2a5ccb6cf9cc86095a5c8c90a30b.setContent(html_41c59c845b552546f282471ca009ae60);



        marker_153d7bb4f52e983bc20fbae873332bfa.bindPopup(popup_c3fb2a5ccb6cf9cc86095a5c8c90a30b)
        ;




            var marker_d1ddd485aedb8fd307b2c800e1f60ea4 = L.marker(
                [51.5411003, 9.948200846079496],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_5d52a61da809119e05dd15590bd8089e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f8a3cc4978c00e205c5615b1a6abb78b = $(`&lt;div id=&quot;html_f8a3cc4978c00e205c5615b1a6abb78b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Göttingen&lt;/div&gt;`)[0];
                popup_5d52a61da809119e05dd15590bd8089e.setContent(html_f8a3cc4978c00e205c5615b1a6abb78b);



        marker_d1ddd485aedb8fd307b2c800e1f60ea4.bindPopup(popup_5d52a61da809119e05dd15590bd8089e)
        ;




            var marker_de6df90c4ade1f784bd715d75d1d4a8d = L.marker(
                [49.4699765, 8.4819024],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_1c82e1755f6434f6c64acea6cb8ee028 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_0aa506289f1a9c95f7349418f6117156 = $(`&lt;div id=&quot;html_0aa506289f1a9c95f7349418f6117156&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Mannheim&lt;/div&gt;`)[0];
                popup_1c82e1755f6434f6c64acea6cb8ee028.setContent(html_0aa506289f1a9c95f7349418f6117156);



        marker_de6df90c4ade1f784bd715d75d1d4a8d.bindPopup(popup_1c82e1755f6434f6c64acea6cb8ee028)
        ;




            var marker_7b7d034fedae27c25f92bfe3688e5e04 = L.marker(
                [51.82151725, 5.863403442541042],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_9037b845fee2bec8945f904f7679b493 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_bc3a3fe27d9d60ac9229ca1445430b38 = $(`&lt;div id=&quot;html_bc3a3fe27d9d60ac9229ca1445430b38&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Radboud University Nijmegen&lt;/div&gt;`)[0];
                popup_9037b845fee2bec8945f904f7679b493.setContent(html_bc3a3fe27d9d60ac9229ca1445430b38);



        marker_7b7d034fedae27c25f92bfe3688e5e04.bindPopup(popup_9037b845fee2bec8945f904f7679b493)
        ;




            var marker_1149f9d75af91304a8efa7d2726dc54c = L.marker(
                [50.821212700000004, 4.34955336942806],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_4f6b04fb3bdcfded00231ac2d0544054 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_9e34fa79408ebfeacff0e7257710cdd3 = $(`&lt;div id=&quot;html_9e34fa79408ebfeacff0e7257710cdd3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Université Catholique de Louvain&lt;/div&gt;`)[0];
                popup_4f6b04fb3bdcfded00231ac2d0544054.setContent(html_9e34fa79408ebfeacff0e7257710cdd3);



        marker_1149f9d75af91304a8efa7d2726dc54c.bindPopup(popup_4f6b04fb3bdcfded00231ac2d0544054)
        ;




            var marker_9425d507c7d36721bbc3710b2950f07a = L.marker(
                [50.8499111, 5.6856029],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6aa48a95823c964f3269eb1b086a5bbd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_cdf29c8e794ba231239c190da715cc54 = $(`&lt;div id=&quot;html_cdf29c8e794ba231239c190da715cc54&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Maastricht University&lt;/div&gt;`)[0];
                popup_6aa48a95823c964f3269eb1b086a5bbd.setContent(html_cdf29c8e794ba231239c190da715cc54);



        marker_9425d507c7d36721bbc3710b2950f07a.bindPopup(popup_6aa48a95823c964f3269eb1b086a5bbd)
        ;




            var marker_46c86c58a98938829bd59774a8feee5d = L.marker(
                [51.5247272, -0.03931034663016243],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8b0f60984d989b1d851048fe02f7543f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_94481e00e6e5e7bdd2cb4268e191109c = $(`&lt;div id=&quot;html_94481e00e6e5e7bdd2cb4268e191109c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Queen Mary University of London&lt;/div&gt;`)[0];
                popup_8b0f60984d989b1d851048fe02f7543f.setContent(html_94481e00e6e5e7bdd2cb4268e191109c);



        marker_46c86c58a98938829bd59774a8feee5d.bindPopup(popup_8b0f60984d989b1d851048fe02f7543f)
        ;




            var marker_de5af46bf694620b4ce02f8de76d2c80 = L.marker(
                [42.6126851, -88.4805318],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6b82a588c4086563536eec8d3fa3c531 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_206c0cd14e03e83199ea50d0c4204a7c = $(`&lt;div id=&quot;html_206c0cd14e03e83199ea50d0c4204a7c&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Geneva&lt;/div&gt;`)[0];
                popup_6b82a588c4086563536eec8d3fa3c531.setContent(html_206c0cd14e03e83199ea50d0c4204a7c);



        marker_de5af46bf694620b4ce02f8de76d2c80.bindPopup(popup_6b82a588c4086563536eec8d3fa3c531)
        ;




            var marker_5f63cf3bc16961f1144cf955a271b96c = L.marker(
                [53.5641091, 9.994978875267606],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_73b72d20cad43f56f6a17681d11b2239 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_cfc9434658fc851f97bab41be3e1e035 = $(`&lt;div id=&quot;html_cfc9434658fc851f97bab41be3e1e035&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Hamburg&lt;/div&gt;`)[0];
                popup_73b72d20cad43f56f6a17681d11b2239.setContent(html_cfc9434658fc851f97bab41be3e1e035);



        marker_5f63cf3bc16961f1144cf955a271b96c.bindPopup(popup_73b72d20cad43f56f6a17681d11b2239)
        ;




            var marker_a941bd6876c25dd572e0a4863cca6773 = L.marker(
                [49.101853399999996, 8.433120159201868],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_aad5836a858940401f59dbdad9477502 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f92bba23c8c58235d7704ec7facaf12e = $(`&lt;div id=&quot;html_f92bba23c8c58235d7704ec7facaf12e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Karlsruhe Institute of Technology&lt;/div&gt;`)[0];
                popup_aad5836a858940401f59dbdad9477502.setContent(html_f92bba23c8c58235d7704ec7facaf12e);



        marker_a941bd6876c25dd572e0a4863cca6773.bindPopup(popup_aad5836a858940401f59dbdad9477502)
        ;




            var marker_08e48f2503b711aa22ca03aa0527063c = L.marker(
                [50.73693715, -3.534734858662963],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_15746c106acf5ad7d18a87ed2d996738 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_be8a7c5fe5f9b39701b8fb86a822ba0d = $(`&lt;div id=&quot;html_be8a7c5fe5f9b39701b8fb86a822ba0d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Exeter&lt;/div&gt;`)[0];
                popup_15746c106acf5ad7d18a87ed2d996738.setContent(html_be8a7c5fe5f9b39701b8fb86a822ba0d);



        marker_08e48f2503b711aa22ca03aa0527063c.bindPopup(popup_15746c106acf5ad7d18a87ed2d996738)
        ;




            var marker_aebde388f63da236acf5247eef4f26e2 = L.marker(
                [51.00784845, 3.710883068491984],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_9d9ee1867cb1d18d3be2e630e0b37e17 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_1e04ae332b8b5a8dab4243410459f588 = $(`&lt;div id=&quot;html_1e04ae332b8b5a8dab4243410459f588&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Ghent University&lt;/div&gt;`)[0];
                popup_9d9ee1867cb1d18d3be2e630e0b37e17.setContent(html_1e04ae332b8b5a8dab4243410459f588);



        marker_aebde388f63da236acf5247eef4f26e2.bindPopup(popup_9d9ee1867cb1d18d3be2e630e0b37e17)
        ;




            var marker_80fa35f953e8987c80ac59a791789e2b = L.marker(
                [48.2131284, 16.360685994114505],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_0a4eef7a4a6c04cd6ab82d28d01a80df = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f655335cea3bb46427f06558f64f5b46 = $(`&lt;div id=&quot;html_f655335cea3bb46427f06558f64f5b46&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Vienna&lt;/div&gt;`)[0];
                popup_0a4eef7a4a6c04cd6ab82d28d01a80df.setContent(html_f655335cea3bb46427f06558f64f5b46);



        marker_80fa35f953e8987c80ac59a791789e2b.bindPopup(popup_0a4eef7a4a6c04cd6ab82d28d01a80df)
        ;




            var marker_0f7250ad9eb93a1a3fc1e26dbf5db679 = L.marker(
                [50.928044549999996, 6.928130514523661],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_cc3a7cc6776fa4fa99da8b0716a2be44 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_9d53b1c753314931bbf3a6afba54c7f7 = $(`&lt;div id=&quot;html_9d53b1c753314931bbf3a6afba54c7f7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Cologne&lt;/div&gt;`)[0];
                popup_cc3a7cc6776fa4fa99da8b0716a2be44.setContent(html_9d53b1c753314931bbf3a6afba54c7f7);



        marker_0f7250ad9eb93a1a3fc1e26dbf5db679.bindPopup(popup_cc3a7cc6776fa4fa99da8b0716a2be44)
        ;




            var marker_612fee57f38410c49099f7c7bd49d8fe = L.marker(
                [54.00975365, -2.7875727317728654],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_2fbecf33c5caf9db5281ed171caeeac9 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_20d2bc908cbf4ae284c59519d6068b98 = $(`&lt;div id=&quot;html_20d2bc908cbf4ae284c59519d6068b98&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Lancaster University&lt;/div&gt;`)[0];
                popup_2fbecf33c5caf9db5281ed171caeeac9.setContent(html_20d2bc908cbf4ae284c59519d6068b98);



        marker_612fee57f38410c49099f7c7bd49d8fe.bindPopup(popup_2fbecf33c5caf9db5281ed171caeeac9)
        ;




            var marker_850499226fad1da2220785087ce46cf9 = L.marker(
                [52.9387428, -1.2002956927457427],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_f68db12542e17bfb45541292b7792d8c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_3aaada9f00c5ff770f8ae4e6298d8f42 = $(`&lt;div id=&quot;html_3aaada9f00c5ff770f8ae4e6298d8f42&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Nottingham&lt;/div&gt;`)[0];
                popup_f68db12542e17bfb45541292b7792d8c.setContent(html_3aaada9f00c5ff770f8ae4e6298d8f42);



        marker_850499226fad1da2220785087ce46cf9.bindPopup(popup_f68db12542e17bfb45541292b7792d8c)
        ;




            var marker_d72c0ee28247dcaff219ccd23ff6cb67 = L.marker(
                [48.38044334999999, 10.010101151636224],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8272fb645293e2de29653ba340eea609 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_fbdffeb4ed9152934e9d2c1385224565 = $(`&lt;div id=&quot;html_fbdffeb4ed9152934e9d2c1385224565&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Ulm University&lt;/div&gt;`)[0];
                popup_8272fb645293e2de29653ba340eea609.setContent(html_fbdffeb4ed9152934e9d2c1385224565);



        marker_d72c0ee28247dcaff219ccd23ff6cb67.bindPopup(popup_8272fb645293e2de29653ba340eea609)
        ;




            var marker_333fc096d229bdc4dfb603040a23d6cb = L.marker(
                [51.028276500000004, 13.735982754935176],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e86ef602cd1457b03d6c66ae71233a50 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_ba998888c3fc9850a3e55a111292c2c2 = $(`&lt;div id=&quot;html_ba998888c3fc9850a3e55a111292c2c2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;TU Dresden&lt;/div&gt;`)[0];
                popup_e86ef602cd1457b03d6c66ae71233a50.setContent(html_ba998888c3fc9850a3e55a111292c2c2);



        marker_333fc096d229bdc4dfb603040a23d6cb.bindPopup(popup_e86ef602cd1457b03d6c66ae71233a50)
        ;




            var marker_aeeaa092b37348a7bd942266eaf5588f = L.marker(
                [53.80677435, -1.5562877504739676],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_ac3c65abe4860b6029e61c33b87d02f4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_f09f5f32cd21f4cdc1624e545f41e3eb = $(`&lt;div id=&quot;html_f09f5f32cd21f4cdc1624e545f41e3eb&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Leeds&lt;/div&gt;`)[0];
                popup_ac3c65abe4860b6029e61c33b87d02f4.setContent(html_f09f5f32cd21f4cdc1624e545f41e3eb);



        marker_aeeaa092b37348a7bd942266eaf5588f.bindPopup(popup_ac3c65abe4860b6029e61c33b87d02f4)
        ;




            var marker_99aa22f25884b7f343b5b68858782b15 = L.marker(
                [43.7206078, 10.4026444],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_ad8b6d1a250dc5761f6739d2d285750e = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_e9e77825cbfa2e999a01e687a0de895a = $(`&lt;div id=&quot;html_e9e77825cbfa2e999a01e687a0de895a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Scuola Superiore Sant’Anna&lt;/div&gt;`)[0];
                popup_ad8b6d1a250dc5761f6739d2d285750e.setContent(html_e9e77825cbfa2e999a01e687a0de895a);



        marker_99aa22f25884b7f343b5b68858782b15.bindPopup(popup_ad8b6d1a250dc5761f6739d2d285750e)
        ;




            var marker_9a616b850fa0bec71f104033c738ab11 = L.marker(
                [59.363333600000004, 18.05879425982729],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e2f46600d3890abd9c10a1188fdaa69f = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_3d413c2c9ff37f81dc653cb523f18927 = $(`&lt;div id=&quot;html_3d413c2c9ff37f81dc653cb523f18927&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Stockholm University&lt;/div&gt;`)[0];
                popup_e2f46600d3890abd9c10a1188fdaa69f.setContent(html_3d413c2c9ff37f81dc653cb523f18927);



        marker_9a616b850fa0bec71f104033c738ab11.bindPopup(popup_e2f46600d3890abd9c10a1188fdaa69f)
        ;




            var marker_6d3e872212cf5ce24278d67da5385de5 = L.marker(
                [57.16452475, -2.1018363546621197],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_3d1c5ed3beee47a99e453c218a001d7a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_6bc4eb0a8497cf4a786e325dc1f7710a = $(`&lt;div id=&quot;html_6bc4eb0a8497cf4a786e325dc1f7710a&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Aberdeen&lt;/div&gt;`)[0];
                popup_3d1c5ed3beee47a99e453c218a001d7a.setContent(html_6bc4eb0a8497cf4a786e325dc1f7710a);



        marker_6d3e872212cf5ce24278d67da5385de5.bindPopup(popup_3d1c5ed3beee47a99e453c218a001d7a)
        ;




            var marker_21bf47bba0742ccbc15ecaab1fb6228c = L.marker(
                [43.7196687, 10.400432749413179],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_54bd5b300094751f485cd162697b5d4c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_581cba0e46c9f1214c32b3629cb572b8 = $(`&lt;div id=&quot;html_581cba0e46c9f1214c32b3629cb572b8&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Scuola Normale Superiore di Pisa&lt;/div&gt;`)[0];
                popup_54bd5b300094751f485cd162697b5d4c.setContent(html_581cba0e46c9f1214c32b3629cb572b8);



        marker_21bf47bba0742ccbc15ecaab1fb6228c.bindPopup(popup_54bd5b300094751f485cd162697b5d4c)
        ;




            var marker_29beb91034de8da25c774f70a7f6483b = L.marker(
                [50.86796665, -0.08778899363132905],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_7f806cb61ad9a0a1825bec65553b5279 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_6f466ef2cafba3eb0323987b7f60f4f2 = $(`&lt;div id=&quot;html_6f466ef2cafba3eb0323987b7f60f4f2&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Sussex&lt;/div&gt;`)[0];
                popup_7f806cb61ad9a0a1825bec65553b5279.setContent(html_6f466ef2cafba3eb0323987b7f60f4f2);



        marker_29beb91034de8da25c774f70a7f6483b.bindPopup(popup_7f806cb61ad9a0a1825bec65553b5279)
        ;




            var marker_42ae360f04812d997457936c2b7b7b4c = L.marker(
                [55.785414450000005, 12.520215144442094],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_ba36491ec3a56d722e8788163d0f58d4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_fd34c1ca4b025165a8454ea802648f51 = $(`&lt;div id=&quot;html_fd34c1ca4b025165a8454ea802648f51&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Technical University of Denmark&lt;/div&gt;`)[0];
                popup_ba36491ec3a56d722e8788163d0f58d4.setContent(html_fd34c1ca4b025165a8454ea802648f51);



        marker_42ae360f04812d997457936c2b7b7b4c.bindPopup(popup_ba36491ec3a56d722e8788163d0f58d4)
        ;




            var marker_40780845da5e0569994ff92af5edd3e1 = L.marker(
                [56.3398198, -2.8117937053149826],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8cb8d56200a9b0141df94084b7e377f3 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_a9a38bac11be1493480bbb01de0e2d86 = $(`&lt;div id=&quot;html_a9a38bac11be1493480bbb01de0e2d86&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of St Andrews&lt;/div&gt;`)[0];
                popup_8cb8d56200a9b0141df94084b7e377f3.setContent(html_a9a38bac11be1493480bbb01de0e2d86);



        marker_40780845da5e0569994ff92af5edd3e1.bindPopup(popup_8cb8d56200a9b0141df94084b7e377f3)
        ;




            var marker_842b39d86653e466e48b10860a7f0051 = L.marker(
                [52.33396225, 4.865196500737312],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_30bdb53805f907dd08feaf9174de7f1b = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_5718b4bc57c7d4b7ea53d3058e445e35 = $(`&lt;div id=&quot;html_5718b4bc57c7d4b7ea53d3058e445e35&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Vrije Universiteit Amsterdam&lt;/div&gt;`)[0];
                popup_30bdb53805f907dd08feaf9174de7f1b.setContent(html_5718b4bc57c7d4b7ea53d3058e445e35);



        marker_842b39d86653e466e48b10860a7f0051.bindPopup(popup_30bdb53805f907dd08feaf9174de7f1b)
        ;




            var marker_c3676436c6dcf5cf9594405423380587 = L.marker(
                [51.4486602, 5.4903995655080475],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_16e0f8b0b8b2c5320b854100b04b9324 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_880874e4ecce04b2c9308c84e750a97e = $(`&lt;div id=&quot;html_880874e4ecce04b2c9308c84e750a97e&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Eindhoven University of Technology&lt;/div&gt;`)[0];
                popup_16e0f8b0b8b2c5320b854100b04b9324.setContent(html_880874e4ecce04b2c9308c84e750a97e);



        marker_c3676436c6dcf5cf9594405423380587.bindPopup(popup_16e0f8b0b8b2c5320b854100b04b9324)
        ;




            var marker_66245d48a53ad048217161b48099b2b7 = L.marker(
                [52.62446355, -1.1257301398551323],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_17c7b34fa552378164f1c76e4c797b6a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_0e872ca16c62ed623b58173e091c2597 = $(`&lt;div id=&quot;html_0e872ca16c62ed623b58173e091c2597&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Leicester&lt;/div&gt;`)[0];
                popup_17c7b34fa552378164f1c76e4c797b6a.setContent(html_0e872ca16c62ed623b58173e091c2597);



        marker_66245d48a53ad048217161b48099b2b7.bindPopup(popup_17c7b34fa552378164f1c76e4c797b6a)
        ;




            var marker_2e1cfd157561aee6a3e48a2654a783c4 = L.marker(
                [54.98017505, -1.6146802127187847],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_88a100f243b3d31ba31b4155d75658f1 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_134ee52f681d7e29342e70b59da8dcc7 = $(`&lt;div id=&quot;html_134ee52f681d7e29342e70b59da8dcc7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Newcastle University&lt;/div&gt;`)[0];
                popup_88a100f243b3d31ba31b4155d75658f1.setContent(html_134ee52f681d7e29342e70b59da8dcc7);



        marker_2e1cfd157561aee6a3e48a2654a783c4.bindPopup(popup_88a100f243b3d31ba31b4155d75658f1)
        ;




            var marker_fbfdadbb2566f009a40fc468ef69f3b7 = L.marker(
                [46.5225695, 6.580949860268587],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_aa0935a09c454eda660653a50e7c3483 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_1fafef3eee3b877d085185e36dbf9ee7 = $(`&lt;div id=&quot;html_1fafef3eee3b877d085185e36dbf9ee7&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Lausanne&lt;/div&gt;`)[0];
                popup_aa0935a09c454eda660653a50e7c3483.setContent(html_1fafef3eee3b877d085185e36dbf9ee7);



        marker_fbfdadbb2566f009a40fc468ef69f3b7.bindPopup(popup_aa0935a09c454eda660653a50e7c3483)
        ;




            var marker_077a754bd51b514f5fd471cd8cc5fb2c = L.marker(
                [60.1860789, 24.828102074406736],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_31a1adca06f10073ec612bfff8a5f47c = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_64d21ef6b2b7a9f9ffc2f25def0255ef = $(`&lt;div id=&quot;html_64d21ef6b2b7a9f9ffc2f25def0255ef&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Aalto University&lt;/div&gt;`)[0];
                popup_31a1adca06f10073ec612bfff8a5f47c.setContent(html_64d21ef6b2b7a9f9ffc2f25def0255ef);



        marker_077a754bd51b514f5fd471cd8cc5fb2c.bindPopup(popup_31a1adca06f10073ec612bfff8a5f47c)
        ;




            var marker_7af6466ad625c4e581367ee32589d609 = L.marker(
                [53.40724285, -2.965833661018871],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_7f8d62281fd8f105128c3c76d314268a = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_494fa1ea6e6bb26ccf3947c65e26a61f = $(`&lt;div id=&quot;html_494fa1ea6e6bb26ccf3947c65e26a61f&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Liverpool&lt;/div&gt;`)[0];
                popup_7f8d62281fd8f105128c3c76d314268a.setContent(html_494fa1ea6e6bb26ccf3947c65e26a61f);



        marker_7af6466ad625c4e581367ee32589d609.bindPopup(popup_7f8d62281fd8f105128c3c76d314268a)
        ;




            var marker_9f2faf8e8fb9a14700b5f333ed6e19b7 = L.marker(
                [51.96734215, 7.599243326272159],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_8acedddf65826647909716824905fc6d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_cd553045e1fafb36b93a0bf288590daa = $(`&lt;div id=&quot;html_cd553045e1fafb36b93a0bf288590daa&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Münster&lt;/div&gt;`)[0];
                popup_8acedddf65826647909716824905fc6d.setContent(html_cd553045e1fafb36b93a0bf288590daa);



        marker_9f2faf8e8fb9a14700b5f333ed6e19b7.bindPopup(popup_8acedddf65826647909716824905fc6d)
        ;




            var marker_c3d80004ffd7433d45754b35a8913892 = L.marker(
                [52.2233862, 6.8854239028157],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_6dab767d3c8e69b5fa4dff69ad3e7712 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_56ad77695fb282cbe3d275145345a9bd = $(`&lt;div id=&quot;html_56ad77695fb282cbe3d275145345a9bd&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Twente&lt;/div&gt;`)[0];
                popup_6dab767d3c8e69b5fa4dff69ad3e7712.setContent(html_56ad77695fb282cbe3d275145345a9bd);



        marker_c3d80004ffd7433d45754b35a8913892.bindPopup(popup_6dab767d3c8e69b5fa4dff69ad3e7712)
        ;




            var marker_636d35cdf4c017febe1095b8f47e1e19 = L.marker(
                [51.4894008, -3.180860341001922],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_5b72b647b780dabe448756e532514a46 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_7e45059ac4454e4c0ea994d287982467 = $(`&lt;div id=&quot;html_7e45059ac4454e4c0ea994d287982467&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Cardiff University&lt;/div&gt;`)[0];
                popup_5b72b647b780dabe448756e532514a46.setContent(html_7e45059ac4454e4c0ea994d287982467);



        marker_636d35cdf4c017febe1095b8f47e1e19.bindPopup(popup_5b72b647b780dabe448756e532514a46)
        ;




            var marker_1cb64c3c9a3008ab242ac585886dee8a = L.marker(
                [59.2016758, 17.6203201],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_067f39074960c4d5a8afaa7f6383f494 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_739ce633e028df907acf8add5e9473c6 = $(`&lt;div id=&quot;html_739ce633e028df907acf8add5e9473c6&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;KTH Royal Institute of Technology&lt;/div&gt;`)[0];
                popup_067f39074960c4d5a8afaa7f6383f494.setContent(html_739ce633e028df907acf8add5e9473c6);



        marker_1cb64c3c9a3008ab242ac585886dee8a.bindPopup(popup_067f39074960c4d5a8afaa7f6383f494)
        ;




            var marker_2618fae355ee55f350aea1694252eaae = L.marker(
                [47.690094, 9.188246768461973],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_297f0e53d04c981691e2ce93daf3c4bd = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_5fa9ec66fa4f6b1a674aa2069a84d19b = $(`&lt;div id=&quot;html_5fa9ec66fa4f6b1a674aa2069a84d19b&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Konstanz&lt;/div&gt;`)[0];
                popup_297f0e53d04c981691e2ce93daf3c4bd.setContent(html_5fa9ec66fa4f6b1a674aa2069a84d19b);



        marker_2618fae355ee55f350aea1694252eaae.bindPopup(popup_297f0e53d04c981691e2ce93daf3c4bd)
        ;




            var marker_96b5e97c9925e3913ade320ace992a69 = L.marker(
                [51.4290899, 6.8008580326401],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_f93275b5cd6c8610588b60acd28572ee = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4ac5864cef43b537bc32f3c39db944a3 = $(`&lt;div id=&quot;html_4ac5864cef43b537bc32f3c39db944a3&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Duisburg-Essen&lt;/div&gt;`)[0];
                popup_f93275b5cd6c8610588b60acd28572ee.setContent(html_4ac5864cef43b537bc32f3c39db944a3);



        marker_96b5e97c9925e3913ade320ace992a69.bindPopup(popup_f93275b5cd6c8610588b60acd28572ee)
        ;




            var marker_dc55c99e0b6f34c44b101ac60024ad6f = L.marker(
                [52.62106225, 1.2356187242525833],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_e3b2e1dc2283ef4f96b6349eb24b1d3d = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_8c49c521105b0f03982c007284e9ab59 = $(`&lt;div id=&quot;html_8c49c521105b0f03982c007284e9ab59&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of East Anglia&lt;/div&gt;`)[0];
                popup_e3b2e1dc2283ef4f96b6349eb24b1d3d.setContent(html_8c49c521105b0f03982c007284e9ab59);



        marker_dc55c99e0b6f34c44b101ac60024ad6f.bindPopup(popup_e3b2e1dc2283ef4f96b6349eb24b1d3d)
        ;




            var marker_cd898d11373aca36744f6c4e427e3de9 = L.marker(
                [57.015907049999996, 9.975308243557345],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_a4a38ae7386d24fe483f771f7b7731ac = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_72b6b6772c13e3a894ad6f3d1937c691 = $(`&lt;div id=&quot;html_72b6b6772c13e3a894ad6f3d1937c691&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Aalborg University&lt;/div&gt;`)[0];
                popup_a4a38ae7386d24fe483f771f7b7731ac.setContent(html_72b6b6772c13e3a894ad6f3d1937c691);



        marker_cd898d11373aca36744f6c4e427e3de9.bindPopup(popup_a4a38ae7386d24fe483f771f7b7731ac)
        ;




            var marker_a7cac6568b98ab4c40a57fba6b024e06 = L.marker(
                [60.36887575, 5.351111541486731],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_5d6aca5392bea98f7092dae4d22ed6d4 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_8b2fcd351bc61e1c1feb7be02b1321b5 = $(`&lt;div id=&quot;html_8b2fcd351bc61e1c1feb7be02b1321b5&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Bergen&lt;/div&gt;`)[0];
                popup_5d6aca5392bea98f7092dae4d22ed6d4.setContent(html_8b2fcd351bc61e1c1feb7be02b1321b5);



        marker_a7cac6568b98ab4c40a57fba6b024e06.bindPopup(popup_5d6aca5392bea98f7092dae4d22ed6d4)
        ;




            var marker_eec88204a686b779e824a79d00d16905 = L.marker(
                [55.7055406, 37.5360595],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_d16943ebd4c3bd6a2675636ae5e9c191 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4cb87af77de7c68075d9900943e2fd09 = $(`&lt;div id=&quot;html_4cb87af77de7c68075d9900943e2fd09&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;Lomonosov Moscow State University&lt;/div&gt;`)[0];
                popup_d16943ebd4c3bd6a2675636ae5e9c191.setContent(html_4cb87af77de7c68075d9900943e2fd09);



        marker_eec88204a686b779e824a79d00d16905.bindPopup(popup_d16943ebd4c3bd6a2675636ae5e9c191)
        ;




            var marker_a55896860182d5f6fe7a3a6e2c1bbb90 = L.marker(
                [51.1843856, 4.41993868786375],
                {}
            ).addTo(map_4dcffdb3531d39924ea28668635b9ad5);


        var popup_1674ddb6d9cf5016317d481344eae134 = L.popup({&quot;maxWidth&quot;: &quot;100%&quot;});



                var html_4b4aa08aa8f9c17982a3b919ce5c366d = $(`&lt;div id=&quot;html_4b4aa08aa8f9c17982a3b919ce5c366d&quot; style=&quot;width: 100.0%; height: 100.0%;&quot;&gt;University of Antwerp&lt;/div&gt;`)[0];
                popup_1674ddb6d9cf5016317d481344eae134.setContent(html_4b4aa08aa8f9c17982a3b919ce5c366d);



        marker_a55896860182d5f6fe7a3a6e2c1bbb90.bindPopup(popup_1674ddb6d9cf5016317d481344eae134)
        ;



&lt;/script&gt;
&lt;/html&gt;" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



# Table joins


```python
world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
europe = world.loc[world.continent == 'Europe'].reset_index(drop=True)

europe_stats = europe[["name", "pop_est", "gdp_md_est"]]
europe_boundaries = europe[["name", "geometry"]]

europe_boundaries.head()
```





  <div id="df-76f6c438-b45a-40b4-91b2-1544dae8e6a2">
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
      <th>name</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Russia</td>
      <td>MULTIPOLYGON (((180.00000 71.51571, 180.00000 ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norway</td>
      <td>MULTIPOLYGON (((15.14282 79.67431, 15.52255 80...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>France</td>
      <td>MULTIPOLYGON (((-51.65780 4.15623, -52.24934 3...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sweden</td>
      <td>POLYGON ((11.02737 58.85615, 11.46827 59.43239...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Belarus</td>
      <td>POLYGON ((28.17671 56.16913, 29.22951 55.91834...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-76f6c438-b45a-40b4-91b2-1544dae8e6a2')"
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
          document.querySelector('#df-76f6c438-b45a-40b4-91b2-1544dae8e6a2 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-76f6c438-b45a-40b4-91b2-1544dae8e6a2');
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
europe_stats.head()
```





  <div id="df-4e72b8b6-093b-41da-9151-f5d49a99b5f3">
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
      <th>name</th>
      <th>pop_est</th>
      <th>gdp_md_est</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Russia</td>
      <td>144373535.0</td>
      <td>1699876</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norway</td>
      <td>5347896.0</td>
      <td>403336</td>
    </tr>
    <tr>
      <th>2</th>
      <td>France</td>
      <td>67059887.0</td>
      <td>2715518</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sweden</td>
      <td>10285453.0</td>
      <td>530883</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Belarus</td>
      <td>9466856.0</td>
      <td>63080</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-4e72b8b6-093b-41da-9151-f5d49a99b5f3')"
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
          document.querySelector('#df-4e72b8b6-093b-41da-9151-f5d49a99b5f3 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4e72b8b6-093b-41da-9151-f5d49a99b5f3');
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
# Use an attribute join to merge data about countries in Europe
europe = europe_boundaries.merge(europe_stats, on="name")
europe.head()
```





  <div id="df-4c1e5996-c8b7-4f59-b22d-84eea2b94f83">
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
      <th>name</th>
      <th>geometry</th>
      <th>pop_est</th>
      <th>gdp_md_est</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Russia</td>
      <td>MULTIPOLYGON (((180.00000 71.51571, 180.00000 ...</td>
      <td>144373535.0</td>
      <td>1699876</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Norway</td>
      <td>MULTIPOLYGON (((15.14282 79.67431, 15.52255 80...</td>
      <td>5347896.0</td>
      <td>403336</td>
    </tr>
    <tr>
      <th>2</th>
      <td>France</td>
      <td>MULTIPOLYGON (((-51.65780 4.15623, -52.24934 3...</td>
      <td>67059887.0</td>
      <td>2715518</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sweden</td>
      <td>POLYGON ((11.02737 58.85615, 11.46827 59.43239...</td>
      <td>10285453.0</td>
      <td>530883</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Belarus</td>
      <td>POLYGON ((28.17671 56.16913, 29.22951 55.91834...</td>
      <td>9466856.0</td>
      <td>63080</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-4c1e5996-c8b7-4f59-b22d-84eea2b94f83')"
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
          document.querySelector('#df-4c1e5996-c8b7-4f59-b22d-84eea2b94f83 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-4c1e5996-c8b7-4f59-b22d-84eea2b94f83');
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




# Spatial join


```python
# Use spatial join to match universities to countries in Europe
european_universities = gpd.sjoin(universities, europe)

# Investigate the result
# f-string으로 바꿔서 설정 --> print(f"We located {len(universities)} universities.")
print("We located {} universities.".format(len(universities)))
print("Only {} of the universities were located in Europe (in {} different countries).".format(
    len(european_universities), len(european_universities.name.unique())))

european_universities.head()
```

    We located 91 universities.
    Only 87 of the universities were located in Europe (in 14 different countries).
    





  <div id="df-3814f4ca-4f71-4652-ae50-3925e9a51623">
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
      <th>Latitude</th>
      <th>Longitude</th>
      <th>geometry</th>
      <th>index_right</th>
      <th>name</th>
      <th>pop_est</th>
      <th>gdp_md_est</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>University of Oxford</td>
      <td>51.759037</td>
      <td>-1.252430</td>
      <td>POINT (-1.25243 51.75904)</td>
      <td>28</td>
      <td>United Kingdom</td>
      <td>66834405.0</td>
      <td>2829108</td>
    </tr>
    <tr>
      <th>1</th>
      <td>University of Cambridge</td>
      <td>52.200623</td>
      <td>0.110474</td>
      <td>POINT (0.11047 52.20062)</td>
      <td>28</td>
      <td>United Kingdom</td>
      <td>66834405.0</td>
      <td>2829108</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Imperial College London</td>
      <td>51.498959</td>
      <td>-0.175641</td>
      <td>POINT (-0.17564 51.49896)</td>
      <td>28</td>
      <td>United Kingdom</td>
      <td>66834405.0</td>
      <td>2829108</td>
    </tr>
    <tr>
      <th>4</th>
      <td>UCL</td>
      <td>51.521785</td>
      <td>-0.135151</td>
      <td>POINT (-0.13515 51.52179)</td>
      <td>28</td>
      <td>United Kingdom</td>
      <td>66834405.0</td>
      <td>2829108</td>
    </tr>
    <tr>
      <th>5</th>
      <td>London School of Economics and Political Science</td>
      <td>51.514311</td>
      <td>-0.116781</td>
      <td>POINT (-0.11678 51.51431)</td>
      <td>28</td>
      <td>United Kingdom</td>
      <td>66834405.0</td>
      <td>2829108</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-3814f4ca-4f71-4652-ae50-3925e9a51623')"
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
          document.querySelector('#df-3814f4ca-4f71-4652-ae50-3925e9a51623 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-3814f4ca-4f71-4652-ae50-3925e9a51623');
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




# 지오코딩 및 테이블 조인을 사용하여 다음 스타벅스 리저브 로스터리에 적합한 위치를 식별합니다.


```python
starbucks = pd.read_csv("/content/drive/MyDrive/2023 데이터마이닝/archive/starbucks_locations.csv")
starbucks.head()
```





  <div id="df-5586ca89-6797-48bf-bcc4-20dc307d9cf1">
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
      <th>Store Number</th>
      <th>Store Name</th>
      <th>Address</th>
      <th>City</th>
      <th>Longitude</th>
      <th>Latitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10429-100710</td>
      <td>Palmdale &amp; Hwy 395</td>
      <td>14136 US Hwy 395 Adelanto CA</td>
      <td>Adelanto</td>
      <td>-117.40</td>
      <td>34.51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>635-352</td>
      <td>Kanan &amp; Thousand Oaks</td>
      <td>5827 Kanan Road Agoura CA</td>
      <td>Agoura</td>
      <td>-118.76</td>
      <td>34.16</td>
    </tr>
    <tr>
      <th>2</th>
      <td>74510-27669</td>
      <td>Vons-Agoura Hills #2001</td>
      <td>5671 Kanan Rd. Agoura Hills CA</td>
      <td>Agoura Hills</td>
      <td>-118.76</td>
      <td>34.15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29839-255026</td>
      <td>Target Anaheim T-0677</td>
      <td>8148 E SANTA ANA CANYON ROAD AHAHEIM CA</td>
      <td>AHAHEIM</td>
      <td>-117.75</td>
      <td>33.87</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23463-230284</td>
      <td>Safeway - Alameda 3281</td>
      <td>2600 5th Street Alameda CA</td>
      <td>Alameda</td>
      <td>-122.28</td>
      <td>37.79</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-5586ca89-6797-48bf-bcc4-20dc307d9cf1')"
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
          document.querySelector('#df-5586ca89-6797-48bf-bcc4-20dc307d9cf1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-5586ca89-6797-48bf-bcc4-20dc307d9cf1');
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
# How many rows in each column have missing values?
print(starbucks.isnull().sum())

# View rows with missing locations
```

    Store Number    0
    Store Name      0
    Address         0
    City            0
    Longitude       5
    Latitude        5
    dtype: int64
    


```python
rows_with_missing = starbucks[starbucks["City"]=="Berkeley"]
rows_with_missing
```





  <div id="df-2214fb03-7567-4e31-bcc7-f354d127d2d1">
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
      <th>Store Number</th>
      <th>Store Name</th>
      <th>Address</th>
      <th>City</th>
      <th>Longitude</th>
      <th>Latitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>153</th>
      <td>5406-945</td>
      <td>2224 Shattuck - Berkeley</td>
      <td>2224 Shattuck Avenue Berkeley CA</td>
      <td>Berkeley</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>154</th>
      <td>570-512</td>
      <td>Solano Ave</td>
      <td>1799 Solano Avenue Berkeley CA</td>
      <td>Berkeley</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>155</th>
      <td>17877-164526</td>
      <td>Safeway - Berkeley #691</td>
      <td>1444 Shattuck Place Berkeley CA</td>
      <td>Berkeley</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>156</th>
      <td>19864-202264</td>
      <td>Telegraph &amp; Ashby</td>
      <td>3001 Telegraph Avenue Berkeley CA</td>
      <td>Berkeley</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>157</th>
      <td>9217-9253</td>
      <td>2128 Oxford St.</td>
      <td>2128 Oxford Street Berkeley CA</td>
      <td>Berkeley</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-2214fb03-7567-4e31-bcc7-f354d127d2d1')"
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
          document.querySelector('#df-2214fb03-7567-4e31-bcc7-f354d127d2d1 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-2214fb03-7567-4e31-bcc7-f354d127d2d1');
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
geolocator = Nominatim(user_agent="kaggle_learn")

def my_geocoder(row):
    point = geolocator.geocode(row).point
    return pd.Series({'Latitude': point.latitude, 'Longitude': point.longitude})

berkeley_locations = rows_with_missing.apply(lambda x: my_geocoder(x['Address']), axis=1)
starbucks.update(berkeley_locations)
```


```python
m_2 = folium.Map(location=[37.88,-122.26], zoom_start=13)
# Add a marker for each Berkeley location
for idx, row in starbucks[starbucks["City"]=='Berkeley'].iterrows():
    Marker([row['Latitude'], row['Longitude']]).add_to(m_2)
```


```python
CA_counties = gpd.read_file("/content/drive/MyDrive/2023 데이터마이닝/archive/CA_county_boundaries/CA_county_boundaries/CA_county_boundaries.shp")
CA_counties.crs = {'init': 'epsg:4326'}
CA_counties.head()
```





  <div id="df-d4b1517d-3402-40fc-a4c2-cdc49ca49fa9">
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
      <th>GEOID</th>
      <th>name</th>
      <th>area_sqkm</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6091</td>
      <td>Sierra County</td>
      <td>2491.995494</td>
      <td>POLYGON ((-120.65560 39.69357, -120.65554 39.6...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6067</td>
      <td>Sacramento County</td>
      <td>2575.258262</td>
      <td>POLYGON ((-121.18858 38.71431, -121.18732 38.7...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6083</td>
      <td>Santa Barbara County</td>
      <td>9813.817958</td>
      <td>MULTIPOLYGON (((-120.58191 34.09856, -120.5822...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6009</td>
      <td>Calaveras County</td>
      <td>2685.626726</td>
      <td>POLYGON ((-120.63095 38.34111, -120.63058 38.3...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6111</td>
      <td>Ventura County</td>
      <td>5719.321379</td>
      <td>MULTIPOLYGON (((-119.63631 33.27304, -119.6360...</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d4b1517d-3402-40fc-a4c2-cdc49ca49fa9')"
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
          document.querySelector('#df-d4b1517d-3402-40fc-a4c2-cdc49ca49fa9 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d4b1517d-3402-40fc-a4c2-cdc49ca49fa9');
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
CA_pop = pd.read_csv("/content/drive/MyDrive/2023 데이터마이닝/archive/CA_county_population.csv", index_col="GEOID")
CA_high_earners = pd.read_csv("/content/drive/MyDrive/2023 데이터마이닝/archive/CA_county_high_earners.csv", index_col="GEOID")
CA_median_age = pd.read_csv("/content/drive/MyDrive/2023 데이터마이닝/archive/CA_county_median_age.csv", index_col="GEOID")
```


```python
cols_to_add = CA_pop.join([CA_high_earners, CA_median_age]).reset_index()
CA_stats = CA_counties.merge(cols_to_add, on="GEOID")
```


```python
CA_stats["density"] = CA_stats["population"] / CA_stats["area_sqkm"]
```


```python
sel_counties = CA_stats[((CA_stats.high_earners > 100000) &
                         (CA_stats.median_age < 38.5) &
                         (CA_stats.density > 285) &
                         ((CA_stats.median_age < 35.5) |
                         (CA_stats.density > 1400) |
                         (CA_stats.high_earners > 500000)))]
```


```python
starbucks_gdf = gpd.GeoDataFrame(starbucks, geometry=gpd.points_from_xy(starbucks.Longitude, starbucks.Latitude))
starbucks_gdf.crs = {'init': 'epsg:4326'}

locations_of_interest = gpd.sjoin(starbucks_gdf, sel_counties)
num_stores = len(locations_of_interest)
```


```python
#m_6 = folium.Map(location=[37,-120], zoom_start=6)

#mc = MarkerCluster()

#locations_of_interest = gpd.sjoin(starbucks_gdf, sel_counties)
#for idx, row in locations_of_interest.iterrows():
#    if not math.isnan(row['Longitude']) and not math.isnan(row['Latitude']):
#        mc.add_child(folium.Marker([row['Latitude'], row['Longitude']]))

#m_6.add_child(mc)
```


```python

```
