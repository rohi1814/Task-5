# Task-5
# 🚦 US Traffic Accident Analysis

# Step 1: Import Libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

# Load Data (make sure to upload 'US_Accidents_Dec21_updated.csv')
df = pd.read_csv("US_Accidents_Dec21_updated.csv")

# Step 2: Basic Overview
print("Shape of data:", df.shape)
print("\nMissing values (%):")
print((df.isnull().sum() / len(df)) * 100)

# Drop columns with too many missing values
df = df.drop(columns=["Number", "Wind_Chill(F)", "Precipitation(in)", "Humidity(%)", "Visibility(mi)"], errors='ignore')

# Step 3: Convert DateTime and Extract Time Info
df["Start_Time"] = pd.to_datetime(df["Start_Time"])
df["Hour"] = df["Start_Time"].dt.hour
df["DayOfWeek"] = df["Start_Time"].dt.day_name()

# Step 4: Accidents by Time of Day
plt.figure(figsize=(10, 5))
sns.countplot(x="Hour", data=df, palette="crest")
plt.title("Accidents by Hour of Day")
plt.xlabel("Hour")
plt.ylabel("Count")
plt.grid(True)
plt.show()

# Step 5: Accidents by Weather Condition
top_weather = df["Weather_Condition"].value_counts().nlargest(10)
plt.figure(figsize=(12, 5))
sns.barplot(x=top_weather.index, y=top_weather.values, palette="magma")
plt.title("Top 10 Weather Conditions During Accidents")
plt.xticks(rotation=45)
plt.ylabel("Accident Count")
plt.show()

# Step 6: Accidents by Road Condition
top_conditions = df["Traffic_Signal"].value_counts()
plt.figure(figsize=(6, 4))
sns.barplot(x=top_conditions.index.astype(str), y=top_conditions.values, palette="Set2")
plt.title("Traffic
