# 📊 Data Analyst Skills & Salary Analysis (US Job Market)

# INTRODUCTION

The data job market is constantly evolving, and knowing which skills are truly valuable can make a significant difference in career decisions. This project analyzes U.S. job postings to uncover which skills are most demanded, how those skills trend over time, how they are compensated, and ultimately, which skills provide the best return on investment for Data Analysts.

# BACKGROUND

Data roles such as Data Analyst, Data Engineer, and Data Scientist often overlap, yet each requires a different combination of tools and technical expertise. Many aspiring analysts focus on learning popular tools without understanding how demand, salary, and specialization interact. This project aims to bridge that gap by using real job market data to provide actionable, data-driven insights.

# TOOLS USED

* Python – data analysis and visualization

* Pandas & NumPy – data manipulation

* Matplotlib & Seaborn – data visualization

* AdjustText – label optimization in scatter plots

* Jupyter Notebook – exploratory analysis and documentation

# ANALYSIS

The analysis is divided into four key questions:

* Most demanded skills across top data roles
Identifies core and role-specific skills for Data Analysts, Data Engineers, and Data Scientists.

* Skill demand trends for Data Analysts
Examines how in-demand skills evolve throughout the year to detect stability or change.

* Salary analysis by role and skill
Compares job salaries and evaluates the gap between high-demand and high-paying skills.

* Optimal skills for Data Analysts
Combines demand and salary metrics to determine which skills offer the highest overall career value.

Each section is supported by Python-based visualizations and detailed notebooks.

## 1. What are the most demanded skills for the top 3 most popular data roles? 

The data job market is highly competitive, and understanding which skills are most in demand is essential for making informed career decisions. In this section, we analyze job posting data using Python to identify the most requested skills for Data Analysts, Data Engineers, and Data Scientists. The following analysis reveals key patterns and differences across roles, providing valuable insights into current market expectations.

### Visualize Data

View my notebook with detailed steps here: 
[2_skill_count.ipynb](3_Proyect\2_skill_count.ipynb)

````python
fig, ax = plt.subplots(len(job_titles),1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot= df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent',y='job_skills', ax=ax[i],hue='skill_count',palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].legend().remove()
    ax[i].set_xlim(0,78)

    for n, v in enumerate(df_plot['skill_percent']):   # add data labels ejemplo %
        ax[i].text(v + 1,n, f'{v:.0f}%', va='center')
    
    if i !=len(job_titles) -1:  #keep x axis ticks only in the last plot
        ax[i].set_xticks([]) #remuve x axis ticks

fig.suptitle('Likelihood of Skills Requested in the US Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
````
### Results

![Visualization of Top Skills for Data Nerds](3_Proyect/IMAGES_2_SKILL_COUNT.png)
*Note: Percentages represent the share of U.S. job postings that explicitly mention each skill for the respective role. Only the top five most frequently requested skills per role are shown to highlight core market requirements.


### Insights

* SQL is foundational across all roles, especially for Data Engineers (68%) and Data Scientists (51%).

* Python dominates technical roles, with highest demand for Data Scientists (72%) and Data Engineers (65%).

* Data Analysts rely more on Excel and BI tools, with Excel (41%) and Tableau (28%) appearing prominently.

* Cloud skills matter mainly for Data Engineers, particularly AWS (43%) and Azure (32%).

* R is still relevant for Data Scientists (44%) but far less requested for other roles.

* SAS shows declining relevance overall, appearing at lower rates across all three roles.

Role specialization is clear:

* Analysts → SQL, Excel, Tableau
* Engineers → SQL, Python, Cloud, Spark
* Scientists → Python, SQL, R


## 2. How are in-demand skills trending for Data Analysts?  

Beyond identifying the most demanded skills, it is equally important to understand how these skills evolve over time. In this section, we analyze trends in Data Analyst skill demand using Python to observe patterns, fluctuations, and potential shifts throughout the year. This time-based analysis helps uncover which skills remain stable and which show signs of growing or declining relevance.

### Visualize Data

View my notebook with detailed steps here: 
[3_skill_trend.ipynb](3_Proyect\3_skills_trend.ipynb)

````python
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
````

### Results

![Visualization of Skills Trend for Data Nerds](3_Proyect\IMAGES_\3_Skills_trend.png)
*Note: This chart shows monthly trends in the likelihood that specific skills appear in U.S. Data Analyst job postings during 2024. Percentages reflect relative demand over time and highlight seasonal patterns and stability in core analytical skills.

### Insights

* SQL remains the top skill all year, though it shows a mild downward trend toward year-end 📉

* Excel demand gradually declines, with a noticeable dip in Q4 before a small rebound in December

* Python and Tableau stay relatively stable, indicating consistent but moderate demand for Data Analysts

* Tableau peaks mid-year (around August), suggesting seasonal demand for visualization skills 📊

* Python shows slight volatility, but no strong upward or downward trend

* SAS is the least requested skill throughout the year, remaining consistently low

* Overall insight: core analyst skills are stable, but advanced or niche tools don’t show strong growth signals


## 3. How well do jobs and skills pay for Data Analysts?

### Highest Paid & Most Demanded Skills for Data 

Understanding which skills are in demand is only part of the picture—compensation plays a crucial role as well. In this section, we use Python to analyze salary data for Data Analysts, examining how pay varies across roles and specific skills. This analysis provides insight into which skills are not only popular but also offer higher earning potential.

### Visualize Data

View my notebook with detailed steps here: 
[3_salary_analysus.ipynb](3_Proyect\4_salary_analysis.ipynb)

````python

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay,x='median',y=df_DA_top_pay.index,ax=ax[0], hue='median', palette='dark:b_r')

# Top 10 Most In-demand Skills for Data Analyst
sns.barplot(data= df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1], hue='median',palette = 'light:b')

plt.show()
````

### Results

![Visualization of Salary Analysis for Data Nerds](3_Proyect\IMAGES_\4_salary_analysis.png)
*Note: This boxplot illustrates the distribution of annual salaries in the U.S. across data roles and seniority levels. Medians, interquartile ranges, and outliers highlight salary progression, variability, and the impact of seniority on compensation.


![Visualization of Salary Analysis for Data Nerds](3_Proyect\IMAGES_\4_salary_analysis2.png)
*Note: These charts compare the top 10 highest-paid skills with the top 10 most in-demand skills for Data Analysts in the U.S. Median salaries are shown to highlight the gap between market demand and compensation, emphasizing the trade-off between accessibility and specialization.

### Insights 

* Highest-paid skills are niche and specialized, often outside the typical Data Analyst toolkit (e.g., DevOps, cloud, blockchain) 💰

* There is a clear gap between pay and demand: the most in-demand skills are not the highest paid

* Popular tools like Python, SQL, Excel, and Tableau offer solid but moderate salaries, reflecting their widespread use

* Advanced or less common skills command salary premiums, likely due to lower supply and cross-functional value

* Demand-focused skills prioritize accessibility, while pay-focused skills reward specialization

* Key takeaway: combining core analyst skills with niche or technical expertise can significantly boost earning potential 📈


## 4. What is the most optimal skill to learn for Data Analyst?

With both demand and salary in mind, the final step is identifying which skills offer the best overall return for Data Analysts. In this section, we use Python to combine skill popularity and median salary data to determine the most optimal skills to learn. This analysis highlights skills that balance strong market demand with competitive pay, helping prioritize learning paths with the highest career impact.

### Visualize Data

View my notebook with detailed steps here: 
[5_optimal_skills.ipynb](3_Proyect\5_optimal_skills.ipynb)

````python
from adjustText import adjust_text

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary']) 
plt.show()

````

### Results

![Visualization of Optimal Skills for Data Analysis in US](3_Proyect\IMAGES_\5_optimal_skills.png)
*Note: This scatter plot compares skill demand (percentage of Data Analyst job postings) with median annual salary in the U.S. Skills positioned toward the upper-right offer the most optimal balance between high demand and strong compensation, highlighting Python as the strongest overall skill investment.

### INSIGHTS

* Python stands out as the most optimal skill: combina alta demanda (~35%) con el salario mediano más alto (~$97K) 🚀

* SQL is the most in-demand skill, pero su salario mediano es menor que el de Python, lo que lo posiciona como un skill base más que diferenciador

* Cloud-related skills (Oracle) muestran alto salario con baja demanda, indicando especialización bien pagada pero de nicho 💰

* Visualization tools like Tableau logran un buen equilibrio entre demanda y salario, ideales para Data Analysts orientados al negocio 📊

* Excel sigue siendo muy demandado, pero ofrece uno de los salarios medianos más bajos, reflejando su carácter básico

* Word y PowerPoint presentan baja demanda y baja compensación, con bajo retorno de inversión para perfiles de Data Analyst

* Key takeaway: el skill más óptimo no es el más demandado ni el mejor pagado por separado, sino el que equilibra demanda + salario, donde Python lidera claramente



# CONCLUSION

This project demonstrates that the most optimal skill to learn is not simply the most popular or the highest paid in isolation. Instead, skills that balance strong demand with competitive compensation provide the greatest career impact. For Data Analysts, Python clearly stands out as the most optimal skill, while SQL and Excel remain essential foundations. Strategic upskilling—combining core tools with specialized knowledge—offers the best path for long-term career growth in the data field.