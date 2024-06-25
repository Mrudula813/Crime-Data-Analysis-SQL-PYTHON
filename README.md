# Crime-Data-Analysis-SQL-PYTHON

import pymysql
import seaborn as sns
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px


#%%
conn=pymysql.connect(host='localhost',
                    user="root",
                    password= "12345",
                    database="crime_data")

conn
#%%
sql_query ="SELECT * FROM crime_data.crime";
df=pd.read_sql(sql_query,conn)
df.head()
#%%
df1=pd.read_csv('crime_data.csv')
df1.info()
#%%
df1.tail()
#%%
import matplotlib.pyplot as plt
sql_query ="SELECT Vict_Age FROM crime_data.crime";
df=pd.read_sql(sql_query,conn)
plt.figure(figsize=(10,3))
plt.hist(df["Vict_Age"],color= 'red',edgecolor="black")
plt.xlabel("Victim_Age")
plt.ylabel("Frequency")
plt.title("Disctribution of Victim Age")
plt.show()
#%%
fig = px.scatter(df1, x="LAT", y="LON", color="Location",
                 labels={
                     "LATTITUDE": "LATITTUDE",
                     "LONGTITUDE": "LONGTITUDE",
                     "LOCATION": "LOCATION"
                 },
                title=" Crime Data: Spatial Analysis")
              
fig.show()
#%%

fig = px.scatter_mapbox(df1, lat="LAT", lon="LON",
                        color_discrete_sequence=["fuchsia"], zoom=10, height=400)
fig.update_layout(mapbox_style="open-street-map")

fig.show()
#%%
print(df1['Vict_Sex'].unique())
print(df1['Vict_Sex'].value_counts())

#%%
sns.countplot(data= df1 ,x='Vict_Sex',hue='Vict_Sex')
#%%
import pandas as pd
sql_query ="SELECT Location FROM crime_data.crime";
df=pd.read_sql(sql_query,conn)
plt.figure(figsize=(10,70))
sns.countplot(y="Location",data=df)
plt.title("Crimes Occurred Based on Location")
plt.show()
#%%
import matplotlib.pyplot as plt
sql_query ="SELECT Crm_Cd FROM crime_data.crime";
df=pd.read_sql(sql_query,conn)
plt.figure(figsize=(10,3))
plt.hist(df["Crm_Cd"],color= 'Blue',edgecolor="black")
plt.xlabel("Crime Code")
plt.ylabel("count")
plt.title("Disctribution of Reported Crime Code")
plt.show()
#%%

#%%
import matplotlib.pyplot as plt
sns.histplot(df1["Crm_Cd"], kde=True)
#%%
