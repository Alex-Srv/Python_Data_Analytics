# The Analysis 

## 1. What are the most demanded skills for top 3 most popular data roles in Russia?

To find the most demanded skills for the top 3 most popular data roles in Russia, I filtered the dataset to identify the most common positions and extracted the top 5 skills for each role. This analysis highlights the core technologies required in the Russian job market, providing clear insights into which skills to prioritize depending on the targeted role.

View my notebook with detailed steps here: [2_Skills_Count.ipynb](3_Project/2_Skills_Count.ipynb)

### Visualize Data
```python
fig , ax = plt.subplots(len(job_titles), 1)

for i , job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short']== job_title].head(5)
    df_plot[::-1].plot(kind='barh', x= 'job_skills', y= 'skill_count', ax=ax[i], title= job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend('')
plt.tight_layout()   
```

## Results
![Visualization of top skills](3_Project/images/Skills_Demand.png)

### Insights

- **Python and SQL are essential across all data roles:** Both skills consistently dominate the top rankings. SQL is the #1 required skill for Data Engineers, while Python is the clear leader for Data Scientists and Machine Learning Engineers.
- **Data Engineers focus heavily on data pipelines and big data tools:** Unlike the other roles, Data Engineering demand is strongly driven by orchestration and distributed systems, specifically **Airflow**, **Hadoop**, and **Spark**.
- **Machine Learning Engineers require deep learning and containerization:** Beyond programming and SQL, ML Engineers are uniquely expected to know framework and deployment tools like **PyTorch** and **Docker**.

# The Analysis 

## 2. How are in_demand skills trending for Data Engineer?

View my notebook with detailed steps here: [3_Skills_Trend.ipynb](3_Project/3_Skills_Trend.ipynb)


```python
df_plot = df_DE_RUS_percent.iloc[:,:5]
sns.set_theme(style='ticks')
sns.lineplot(df_plot, legend=False, dashes=False, palette='tab10')
sns.despine()
plt.title('What are The top skills in Russia for Data Engineers?')
plt.xlabel('2023')
plt.ylabel('Likelihood in Job Posting')
plt.ylim(0,100)
from matplotlib.ticker import PercentFormatter
ax=plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter())
#ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos:f'{int(y)}%'))
for i in range(4):
    plt.text(11.5, df_plot.iloc[-1, i]+3, df_plot.columns[i])
plt.text(11.5, df_plot.iloc[-1, 4]-3,df_plot.columns[4])

plt.tight_layout()
```

## Results
![Skills Demand](/3_Project/images/Skills_demand_for_DE.png)

### Insights

- **SQL and Python remain the undisputed market leaders throughout the entire year:** Both technologies consistently dominate the job postings in Russia. SQL holds the solid #1 position, required in 70% to over 90% of vacancies each month, while Python securely holds the #2 spot at roughly 65–80%.
- **Airflow is the primary pipeline orchestration tool:** Airflow maintains a stable third-place position, hovering around a 45–65% requirement rate across all 12 months, highlighting workflow automation as an indispensable competency for data engineers.
- **Spark and Hadoop compete closely in big data processing:** Both frameworks display parallel fluctuations between 30% and 50% throughout the year (with a notable surge for Spark in August), demonstrating consistent, specialized demand for distributed computing frameworks in the Russian market.