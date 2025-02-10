

# Amusement Park Data Analysis

This document summarizes various tasks performed on the amusement park dataset, including data analysis, visualization, and storytelling.

---

## Task 1: Mean, Median, and Mode of Ride Counts

### Analysis
- **MartianRide**
  - Mean: `0.9073`
  - Median: `0.0`
  - Mode: `0`
- **TeacupRide**
  - Mean: `0.5862`
  - Median: `0.0`
  - Mode: `0`
- **RiverRide**
  - Mean: `1.2007`
  - Median: `1.0`
  - Mode: `0`

### Code
```python
ride_stats = {}
for ride in ["MartianRide", "TeacupRide", "RiverRide"]:
    ride_stats[ride] = {
        "mean": df[ride].mean(),
        "median": df[ride].median(),
        "mode": df[ride].mode().iloc[0]
    }
ride_stats

Task 2: Grouped Statistics by Date

Analysis
	•	Calculated the mean, median, and mode of ride counts for each day using groupby().

Code

grouped_stats = df.groupby("VisitDate")[["MartianRide", "TeacupRide", "RiverRide"]].agg(["mean", "median", lambda x: x.mode().iloc[0]])
grouped_stats.columns = ["_".join(col) for col in grouped_stats.columns]  # Flatten column names
grouped_stats.head()

Task 3: Standard Deviation and Variance of Ride Counts

Results
	•	MartianRide
	•	Standard Deviation: 2.077
	•	Variance: 4.315
	•	TeacupRide
	•	Standard Deviation: 1.233
	•	Variance: 1.520
	•	RiverRide
	•	Standard Deviation: 1.296
	•	Variance: 1.679

Code

ride_variance_std = {}
for ride in ["MartianRide", "TeacupRide", "RiverRide"]:
    ride_variance_std[ride] = {
        "std_dev": df[ride].std(),
        "variance": df[ride].var()
    }
ride_variance_std

Task 4: 90th Percentile for Ride Counts

Results
	•	MartianRide: 2
	•	TeacupRide: 2
	•	RiverRide: 3

Code

ride_percentiles = {}
for ride in ["MartianRide", "TeacupRide", "RiverRide"]:
    ride_percentiles[ride] = df[ride].quantile(0.9)
ride_percentiles

Task 5: Histogram of Ride Counts

Analysis
	•	Plotted histograms of total and mean ride counts for each day.

Code

# Total Ride Count per Day
total_rides_per_day = df.groupby("VisitDate")[["MartianRide", "TeacupRide", "RiverRide"]].sum()
total_rides_per_day.sum(axis=1).plot.hist(title="Total Ride Counts Per Day")

# Mean Ride Count per Day
mean_rides_per_day = df.groupby("VisitDate")[["MartianRide", "TeacupRide", "RiverRide"]].mean()
mean_rides_per_day.mean(axis=1).plot.hist(title="Mean Ride Counts Per Day")

Task 6: Stacked Bar Chart

Analysis
	•	Created a stacked bar chart showing the number of Adult and Child visits for the River Ride.

Code

adult_child_counts = df.groupby(["RiverRide", "IsAdult"]).size().unstack(fill_value=0)
adult_child_counts.columns = ["Child", "Adult"]
adult_child_counts.plot(kind="bar", stacked=True, figsize=(10, 6), title="River Ride Counts by Adults and Children")

Task 7: Kernel Density Estimation (KDE) Plot

Code

import seaborn as sns
sns.kdeplot(data=df, x="MoneySpent", hue="IsAdult", fill=True, palette="Set2")
plt.title("KDE Plot: Money Spent by Adult/Child")

Task 8: Storytelling With Data: Scatterplot

Analysis
	•	Scatterplot between TeacupRide and RiverRide counts for first 100 rows.
	•	Differentiated Adults and Children with colors and added a dashed separation line.

Code

subset_df = df.iloc[:100]
plt.figure(figsize=(10, 6))
plt.scatter(subset_df[subset_df["IsAdult"]]["TeacupRide"],
            subset_df[subset_df["IsAdult"]]["RiverRide"],
            color="blue", label="Adult", alpha=0.7, s=80)
plt.scatter(subset_df[~subset_df["IsAdult"]]["TeacupRide"],
            subset_df[~subset_df["IsAdult"]]["RiverRide"],
            color="orange", label="Child", alpha=0.7, s=80)

# Dashed line
x_vals = np.linspace(0, subset_df["TeacupRide"].max(), 100)
y_vals = 2.5 + 0.5 * x_vals
plt.plot(x_vals, y_vals, "--", color="gray", label="Separation Line")
plt.text(3, 4, "AVG", fontsize=12, color="gray", ha="center", rotation=30)

plt.title("Teacup vs. River Ride Counts", fontsize=14)
plt.xlabel("Teacup Ride Count", fontsize=12)
plt.ylabel("River Ride Count", fontsize=12)
plt.legend(fontsize=10)
plt.grid(alpha=0.3)
plt.show()

Summary of Findings
	•	Ride Usage: Adults tend to ride Martian and River rides more, while children prefer the Teacup ride.
	•	Spending Patterns: Adults generally spend more money compared to children.
	•	Visualizations: KDE plots and scatterplots effectively highlight spending and ride preferences, respectively.

This document provides a complete analysis of the amusement park dataset using pandas, matplotlib, and seaborn.

You can save this content in a `.md` file for use in VS Code or other markdown editors. Let me know if you’d like to refine or add additional sections!