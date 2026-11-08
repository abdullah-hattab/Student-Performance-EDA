# Student Performance in Exams — Exploratory Data Analysis

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/abdullah-hattab/Student-Performance-EDA/blob/main/Student_Performance_EDA.ipynb)

**Which students are most at risk of failing math, and where should a school focus its support?**

An end-to-end analysis of the exam results of 1,000 students, written for school administrators and teachers.

---

## Project Overview

A school wants to understand which factors are related to student exam performance, so it can decide where to focus its support. This project analyzes the math, reading and writing scores of 1,000 students alongside their background, with **math** as the main focus.

**Key takeaways**

- **13.5%** of students fail math (score below 50).
- Students on free/reduced lunch fail math **4.5× as often** as other students, and make up **71%** of all math failures.
- The test preparation course is linked to higher scores in every subject, but its gain is **smallest in math**.

**Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn, SciPy, Google Colab

---

## Business Problem and Objective

**Problem.** The school wants to decide where to focus its student support. To do that, it needs evidence on which students are most likely to struggle, especially in math, the subject it cares about most.

**Objective.** Identify which background factors (test preparation, lunch type, parental education and gender) are associated with exam scores, and turn the results into practical recommendations.

The analysis answers five questions:

1. Is the math score normally distributed?
2. Does test preparation affect exam scores?
3. Is there a relationship between reading and writing scores?
4. Which subject has the greatest variation?
5. Does parental education relate to student performance?

---

## Dataset Summary

| Item | Details |
|---|---|
| **Source** | [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) (Kaggle) |
| **Size** | 1,000 students, 8 columns |
| **Scores** | Math, reading and writing, each from 0 to 100 |
| **Background** | Gender, race/ethnicity (anonymized groups A–E), parental level of education, lunch type (standard or free/reduced, an indicator of family income), test preparation course (completed or none) |
| **Quality** | No missing values, no duplicate rows, no scores outside 0–100 |

---

## Methodology

1. **Checked data quality.** Looked for missing values, duplicates, inconsistent categories and impossible scores. None were found. A few unusually low scores were kept, because they belong to real students who are struggling, the group this analysis exists to find.
2. **Added new measures.** An average score across the three subjects, a pass/fail flag for math (pass mark 50), and a performance level (Low, Medium, High, with cut-offs at 50 and 75).
3. **Described each variable.** The average, spread and shape of each score, and the size of each student group.
4. **Compared groups.** Average scores and fail rates by test preparation, lunch type, parental education and gender.
5. **Tested the key difference.** A standard statistical test (t-test) confirmed that the test preparation gap is very unlikely to be due to chance.

---

## Key Findings

### 1. Math scores follow a near-bell curve, and 13.5% of students fail

![Distribution of math scores](images/math_distribution.png)

Math scores average 66.1 with a median of 66.0, and the distribution is close to symmetric, with a slightly longer tail toward low scores. A formal normality test rejects a perfect bell curve, but with 1,000 students it flags even small departures, so in practice the scores are approximately normal. **13.5% of students scored below the pass mark of 50.**

### 2. Students on free/reduced lunch fail math 4.5 times as often

![Math fail rate by lunch type](images/fail_rate_by_lunch.png)

27.0% of students on free/reduced lunch fail math, compared with 6.0% of students on standard lunch. They make up 35.5% of all students but **71.1% of those failing math** (96 of 135). Apart from the anonymized race/ethnicity groups, this is the largest math gap in the data: an average of 58.9 versus 70.0.

### 3. Test preparation lifts every subject, but math the least

![Average score by subject and test preparation](images/test_prep_by_subject.png)

Students who completed the preparation course scored higher in all three subjects: **+5.6 points in math, +7.4 in reading and +9.9 in writing**, all statistically significant. Only 35.8% of students completed the course. It helps math the least, even though math is the school's priority.

### Other findings

- **Reading and writing go together.** Their scores are very strongly correlated (r = 0.95). Math is more independent (r = 0.80 to 0.82).
- **Variation.** Writing (standard deviation 15.20) and math (15.16) vary the most and are effectively tied. Reading is the most consistent (14.60).
- **Parental education.** Average scores broadly rise with parental education, from 63.1 ("high school") to 73.6 ("master's degree"), though not in a perfectly ordered way. The master's group has only 59 students.
- **Gender.** The gap reverses by subject: male students score 5.1 points higher in math, while female students score 7.1 points higher in reading and 9.2 in writing.

---

## Recommendations

1. **Prioritize math support for students on free/reduced lunch.** Focusing on about a third of the school reaches 71% of the students currently failing math.
2. **Encourage more students to complete the test preparation course.** Only 35.8% do today, and completers score higher in every subject.
3. **Strengthen the course's math content.** Its math gain (+5.6 points) is the smallest of the three subjects.
4. **Make support subject-specific.** Because the gender gap reverses between math and literacy, a single "low performer" program would miss students on both sides. Reading and writing move together, so one literacy program can serve both.

---

## Limitations

- **Likely synthetic data.** This dataset is widely understood to be generated for teaching, so the results describe this dataset rather than real students.
- **Associations, not causes.** Students chose whether to take the course, and nothing was randomly assigned, so the analysis shows what is linked to higher scores, not what causes them.
- **One factor at a time.** Each factor was compared on its own, without controlling for the others.
- **Missing context.** There is no data on attendance, prior grades, study time or school, and lunch type is only a rough proxy for family income.
- **Small or anonymous groups.** Results for small groups (59 students with a master's-educated parent, 89 in group A) are less reliable, and the race/ethnicity labels cannot be interpreted.

---

## Next Steps

1. **Multiple regression** to measure each factor's effect while holding the others constant, for example whether test preparation still matters once lunch type is accounted for.
2. **ANOVA with post-hoc tests** to check which parental education levels differ significantly.
3. **An early-warning model** that predicts math failure from background information available before the exam.
4. **Real, richer data** (attendance, prior grades, several terms) to confirm these patterns and measure the impact of any new support program.

---

## Technical Notebook

The full analysis, including data cleaning, statistics, tests and every chart, is in **[`Student_Performance_EDA.ipynb`](Student_Performance_EDA.ipynb)**. Use the **Open in Colab** badge at the top of this page to run it in your browser.

To run it, load the data straight from this repository:

```python
url = "https://raw.githubusercontent.com/abdullah-hattab/Student-Performance-EDA/main/StudentsPerformance.csv"
df = pd.read_csv(url)
```

### Repository structure

```
Student-Performance-EDA/
├── README.md                       # Project summary (this file)
├── Student_Performance_EDA.ipynb   # Full technical analysis
├── StudentsPerformance.csv         # Raw dataset
└── images/                         # Charts used in this README
```

---

## Author

**Abdallah Hattab** —  · [GitHub @abdullah-hattab](https://github.com/abdullah-hattab)
