# The Analysis 

## 1. What are the most demanded skills for top 3 most popular data roles in Russia?

To find the most demanded skills for the top 3 most popular data roles in Russia, I filtered the dataset to identify the most common positions and extracted the top 5 skills for each role. This analysis highlights the core technologies required in the Russian job market, providing clear insights into which skills to prioritize depending on the targeted role.

View my notebook with detailed steps here: [2_Skills_Count.ipynb](/Python_Data_Project/3_Project/2_Skills_Count.ipynb)

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
![Visualization of top skills](/Python_Data_Project/3_Project/images/Skills_Demand.png)

### Insights

- **Python and SQL are essential across all data roles:** Both skills consistently dominate the top rankings. SQL is the #1 required skill for Data Engineers, while Python is the clear leader for Data Scientists and Machine Learning Engineers.
- **Data Engineers focus heavily on data pipelines and big data tools:** Unlike the other roles, Data Engineering demand is strongly driven by orchestration and distributed systems, specifically **Airflow**, **Hadoop**, and **Spark**.
- **Machine Learning Engineers require deep learning and containerization:** Beyond programming and SQL, ML Engineers are uniquely expected to know framework and deployment tools like **PyTorch** and **Docker**.

# The Analysis 

## 2. How are in_demand skills trending for Data Engineer?

View my notebook with detailed steps here: [3_Skills_Trend.ipynb](/Python_Data_Project/3_Project/3_Skills_Trend.ipynb)


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
![Skills Demand](/Python_Data_Project/3_Project/images/Skills_demand_for_DE.png)

### Insights

- **SQL and Python remain the undisputed market leaders throughout the entire year:** Both technologies consistently dominate the job postings in Russia. SQL holds the solid #1 position, required in 70% to over 90% of vacancies each month, while Python securely holds the #2 spot at roughly 65–80%.
- **Airflow is the primary pipeline orchestration tool:** Airflow maintains a stable third-place position, hovering around a 45–65% requirement rate across all 12 months, highlighting workflow automation as an indispensable competency for data engineers.
- **Spark and Hadoop compete closely in big data processing:** Both frameworks display parallel fluctuations between 30% and 50% throughout the year (with a notable surge for Spark in August), demonstrating consistent, specialized demand for distributed computing frameworks in the Russian market.

# The Analysis 


## 3. How well do jobs and skills pay for Data Analysis?

View my notebook with detailed steps here: [4_Salary_Analysis.ipynb](/Python_Data_Project/3_Project/4_Salary_Analysis.ipynb)

```python
sns.boxplot(data= df_US_top6, x='salary_year_avg', y= 'job_title_short', order= job_order)

plt.title('Salary Distribution in the United States')
plt.xlabel('Yearly Salary($USD)')
ax = plt.gca()
ax.set_ylabel('')
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos:f'${int(x/1000)}K'))
plt.xlim(0,600000)
plt.show()
```

## Results
![Visualization of top roles by median salary](/Python_Data_Project/3_Project/images/By_median_salary.png)

### Insights

* **Data Analyst has the lowest salary ceiling among core data roles:** While entry and mid-level Data Analysts start at around $90K–$100K median salary, their overall compensation range remains the narrowest, lagging behind Data Engineering and Data Science roles at comparable seniority levels.
* **Seniority yields a direct pay jump, but role specialization yields higher returns:** Transitioning from a Data Analyst to a Senior Data Analyst increases median pay, but shifting horizontally into engineering or science tracks (such as Data Engineer or Data Scientist) offers an equivalent or higher baseline along with significantly greater upside potential.
* **Breaking the compensation plateau requires deeper programming and software engineering skills:** To move past the limits of pure data analytics (typically centered on SQL, BI tools, and exploratory scripting), practitioners need to transition toward roles that demand rigorous software engineering principles. This involves mastering compiled and high-performance languages (such as C++, Go, or optimized low-level Python/Rust integrations) and understanding distributed systems, backend architectures, and production-grade algorithms.

# The Analysis 

## 4. Highest Paid and Most Demanded Skills for Data Analyst

View my notebook with detailed steps here: [4_Salary_Analysis.ipynb](/Python_Data_Project/3_Project/4_Salary_Analysis.ipynb)

```python 
fig, ax = plt.subplots(2, 1)

sns.set_theme(style='ticks')

# Top 10 Highest Paid Skills for Data Analysts
#df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False)

sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0],hue = 'median', palette='dark:b_r' )
ax[0].legend().remove()

ax[0].set_title('Top 10 Highest Paid Skills for Data Analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

# Top 10 Most In-Demand Skills for Data Analysts
#df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)

sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median', palette='light:b')
ax[1].legend().remove()

ax[1].set_title('Top 10 Most In-Demand Skills Pay for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim()) # Set the same x-axis limits as the first plot
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

plt.tight_layout()
plt.show()
```
## Results
![Visualization of top median salary by count and by highest pay](/Python_Data_Project/3_Project/images/compare_median.png)

### Insights

* **Niche and specialized technologies command the highest salary premiums:** Specialized skills such as Debian, RingCentral, Mongo, Lua, and Hugging Face dominate top earnings, yielding median salaries between $150K and $200K. These high compensation levels reflect talent scarcity at the intersection of analytics, systems engineering, blockchain (Solidity), and modern machine learning.
* **Core analytical skills ensure broad demand but hit an earlier compensation ceiling:** Foundational tools like Excel, SAS, Tableau, and SQL sit at the lower end of the top-paying in-demand spectrum, centering around a $100K–$120K median salary. While essential for breaking into data analytics, relying solely on them leads to a compensation plateau.
* **Big Data and Cloud platforms offer the optimal balance of market demand and high pay:** Widely requested technologies such as Spark, AWS, Java, Python, and Azure achieve the sweet spot, driving median salaries up to the $125K–$140K bracket. Mastering distributed data processing and cloud infrastructure represents the most direct pathway to maximizing earnings without pivoting to rare micro-niches.

# The Analysis 

## 4. What are the most optimal skill to learn for Data Analyst in US? 

View my notebook with detailed steps here: [5_Optimal_Skills.ipynb](/Python_Data_Project/3_Project/5_Optimal_Skills.ipynb)

```python
from adjustText import adjust_text


#df_DA_skills_high_demand.plot(kind='scatter', x='skills_percent',y='median_salary')
sns.set_theme(style='ticks')
sns.scatterplot(
    data=df_plot,
    x='skills_percent',
    y='median_salary',
    hue='technology'
)
texts= []
plt.xlabel('Likelihood in Job Finding')
plt.ylabel('Median Salary')
plt.title(f'Optimal Skills for Data Analyst in the US')
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(
        df_DA_skills_high_demand['skills_percent'].iloc[i],          
        df_DA_skills_high_demand['median_salary'].iloc[i] + 500,  
        txt,                              
        ha='right',                     
        fontsize=9)
    )
sns.despine()


adjust_text(texts, arrowprops=dict(arrowstyle="->",color ="g",lw=1.5))

ax=plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos:f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos:f'{int(x)}%'))

plt.ylim(75000, 100000)
plt.tight_layout()
```

## Results
![Visualization of Most Oprimal Skills for Data Analyst in the US](/Python_Data_Project/3_Project/images/Optimal_skills.png)

### Insights

* **High-Probability Foundational Skills (Fastest Path to Employment):** For candidates aiming to secure their first data analytics role, **SQL** is the single most vital skill, appearing in nearly 58% of job postings with a solid median compensation of approximately $91K. Combined with **Excel** (over 40% likelihood, ~$84K median) and visualization tools like **Tableau** (~31% likelihood, ~$93K median), this foundational cluster delivers the highest probability of landing a job.
* **High-Earning Value Skills (Higher Salary, Moderate-to-Low Market Demand):** **Python** offers the strongest return on investment, leading top-tier compensation at around $97K median salary while maintaining a robust  around 33% market presence. More specialized technologies such as **Oracle** also reach the peak salary tier (~$97K), but with a much lower hiring frequency (<5% likelihood), representing high-reward but niche specialization opportunities.
* **Deprioritized Skills (Low Demand and Low Compensation):** General office software like **PowerPoint** and **Word** should not be prioritized during skill development. Both demonstrate minimal presence in technical requirements (~6% likelihood) and sit at the bottom of the compensation curve ($81K–$85K), indicating that basic tooling adds little competitive edge in the data analytics job market.
