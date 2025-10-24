# 🎬 AniLytica  
**Anime Data Analysis using Python & Pandas**

AniLytica is a data-driven project designed to analyze and visualize information from an anime dataset. The project demonstrates the power of Python for data preprocessing, extraction, and analysis — uncovering insights such as top-rated anime, longest-running series, and episode distributions.  

---

## 📊 Project Overview  

The project uses **Python** along with **Pandas**, **NumPy**, and **DateTime** libraries to clean, transform, and analyze anime data extracted from a CSV file.  
It focuses on identifying patterns in anime ratings, episode counts, and airing durations.  

**Key Objectives:**  
- Clean raw anime data for structured analysis.  
- Extract the number of episodes and airing period from complex text data.  
- Calculate total months each anime aired using date parsing.  
- Identify highest-rated anime and longest-running titles.  

---

## 🧠 Features  

- 🧩 **Data Extraction:** Extracts anime title, score, episode count, and airing period.  
- 🧹 **Data Cleaning:** Removes irrelevant text and formats columns for analysis.  
- 🗓 **Duration Calculation:** Computes total months of airing using `datetime` and `relativedelta`.  
- 🏆 **Top Ranking Insights:** Finds the top-rated and longest-running anime in the dataset.  
- 📈 **Structured DataFrame:** Final output presented in a clean, well-organized tabular format.  

---

## 🛠️ Tech Stack  

| Tool | Purpose |
|------|----------|
| **Python** | Core programming language |
| **Pandas** | Data manipulation and analysis |
| **NumPy** | Numerical operations |
| **DateTime & dateutil** | Time and date calculations |
| **Jupyter Notebook / VS Code** | Execution and visualization |

---

## 📁 Dataset  

- File: `anime.csv`  
- Columns analyzed: *Title*, *Rank*, *Score*, *Members* (if available)  
- Additional columns generated: *Episodes*, *Time*, *Months*  

---

## ⚙️ Code Workflow  

1. **Load Dataset:**  
   ```python
   df = pd.read_csv('anime.csv')
   
2. **Extract Episode Count**
   ```python
   def extract_episodes(txt):
    check = False
    data = ""
    for i in txt:
        if i == ')':
            check = False
            return data
        if check:
            data += i
        if i == '(':
            check = True
   df['Episodes'] = df['Title'].apply(extract_episodes)

3. **Calculate Airing Duration (Months)**
    ```python
    from dateutil.relativedelta import relativedelta
    from datetime import datetime

   def calculate_total_months(period):
    try:
        start_str, end_str = period.split(' - ')
        start_date = datetime.strptime(start_str, '%b %Y')
        end_date = datetime.strptime(end_str, '%b %Y')
        r = relativedelta(end_date, start_date)
        return r.years * 12 + r.months + 1
    except:
        return None
   df['Months'] = df['Time'].apply(calculate_total_months)

4. **Find Top-Rated and Longest Anime**
   ```python
   df[df['Score'] == df['Score'].max()]
   df[df['Episodes'] == df['Episodes'].max()]
    
   

