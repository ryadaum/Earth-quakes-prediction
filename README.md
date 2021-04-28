### Earth quakes prediction

**In this project we will working with earth quakes data**

1. Transform the data into sammary tables.
2. Using these tables to train predictive model and predict future earth quakes.
3. Analyze the data by bulding reports and dashboards in PowerBI as shown below.

<img width="611" alt="ee" src="https://user-images.githubusercontent.com/83231879/116381677-cc4c4300-a81d-11eb-9464-94980b62ecc7.PNG">

### Project Structure

- We will use `quakes_etl.py` module to read `database.csv`

_Data Sample_:
```
[Row(Date='01/02/1965', Time='13:44:18', Latitude='19.246', Longitude='145.616', Type='Earthquake', Depth='131.6', Depth Error=None, Depth Seismic Stations=None, Magnitude='6', Magnitude Type='MW', Magnitude Error=None, Magnitude Seismic Stations=None, Azimuthal Gap=None, Horizontal Distance=None, Horizontal Error=None, Root Mean Square=None, ID='ISCGEM860706', Source='ISCGEM', Location Source='ISCGEM', Magnitude Source='ISCGEM', Status='Automatic')]
```
Cleansing and transforming the data.
Creating dataframes that will be used to build our reports and applying machine learning Random Forest Regression algorethem to them

_Quakes cleansed and transformed dataframe sampel:_


|      Date|Latitude|Longitude|      Type|Depth|Magnitude|Magnitude Type|          ID|Year|
|----------|--------|---------|----------|-----|---------|--------------|------------|----|
|01/02/1965|  19.246|  145.616|Earthquake|131.6|      6.0|            MW|ISCGEM860706|1965|
|01/04/1965|   1.863|  127.352|Earthquake| 80.0|      5.8|            MW|ISCGEM860737|1965|
|01/05/1965| -20.579| -173.972|Earthquake| 20.0|      6.2|            MW|ISCGEM860762|1965|
|01/08/1965| -59.076|  -23.557|Earthquake| 15.0|      5.8|            MW|ISCGEM860856|1965|
|01/09/1965|  11.938|  126.427|Earthquake| 15.0|      5.8|            MW|ISCGEM860890|1965|

_avg magnitude and max magnitude dataframe sample_:
|Year|Counts|    Avg_Magnitude|Max_Magnitude|
|----|------|-----------------|-------------|
|1990|   196|5.858163265306125|          7.6|
|1975|   150| 5.84866666666667|          7.8|
|1977|   148|5.757432432432437|          7.6|
|2003|   187|5.850802139037435|          7.6|
|2007|   211| 5.89099526066351|          8.4|

Then load them into MongoDB.

- We will use `quakes_ml.py` for our machine learning pipeline. Reading `query.csv` and use it as a test data.
_Data sample_:
```
[Row(time='2017-01-02T00:13:06.300Z', latitude='-36.0365', longitude='51.9288', depth='10', mag='5.7', magType='mwb', nst=None, gap='26', dmin='14.685', rms='1.37', net='us', id='us10007p5d', updated='2017-03-27T23:53:17.040Z', place='Southwest Indian Ridge', type='earthquake', horizontalError='10.3', depthError='1.7', magError='0.068', magNst='21', status='reviewed', locationSource='us', magSource='us')]
```
Read the quakes data from MongoDB
Applying machine learning Random Forest Regression algorethem to end up with this sample results:

|Latitude|Longitude|   Pred_Magnitude|Year|               RMSE|
|--------|---------|-----------------|----|-------------------|
|-36.0365|  51.9288|5.843170216800219|2017|0.40255793832136677|
|  -4.895| -76.3675|5.857753269910164|2017|0.40255793832136677|
|-23.2513| 179.2383|5.903879708543907|2017|0.40255793832136677|
| 24.0151|  92.0177|5.928559166925568|2017|0.40255793832136677|
|-43.3527| -74.5017|5.918127389861314|2017|0.40255793832136677|

The `Earh Quakes Prediction Map.pbix` is the PowerBI dashboard and report file
