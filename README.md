# x62-data-challenge-student-pathways

### Q) Data quality: For each feature (column), what is the data type? Is there any missing data?

```
RangeIndex: 20705 entries, 0 to 20704
Data columns (total 11 columns):
 No.   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   DISTRICT_TYPE       20705 non-null  object 
 1   DISTRICT_NAME       20705 non-null  object 
 2   DISTRICT_CODE       17960 non-null  float64
 3   ACADEMIC_YEAR       20705 non-null  object 
 4   DEMO_CATEGORY       20705 non-null  object 
 5   STUDENT_POPULATION  20705 non-null  object 
 6   AWARD_CATEGORY      20705 non-null  object 
 7   WAGE_YEAR1          20705 non-null  float64
 8   WAGE_YEAR2          20705 non-null  float64
 9   WAGE_YEAR3          20705 non-null  float64
 10  WAGE_YEAR4          20705 non-null  float64
```

**Missing Data:** DISTRICT_CODE has 2,745 missing values (17,960 non-null out of 20,705)

### Q) Range: What are the unique values for each categorical column? What is the range of values of the numeric columns? Are the numeric column values normally distributed?

**Unique values**
```
DISTRICT_TYPE:
 ['School District' 'Legislative District' 'All']

ACADEMIC_YEAR:
 ['2018-2019']

DEMO_CATEGORY:
 ['Race' 'Homeless Status' 'All' 'Foster Status' 'Gender']

STUDENT_POPULATION:
 ['None Reported' 'Black or African American'
 'Did Not Experience Homelessness in K-12'
 'American Indian or Alaska Native'
 'Native Hawaiian or Other Pacific Islander' 'All' 'Two or More Races'
 'Foster Youth' 'Female' 'White' 'Experienced Homelessness in K-12'
 'Not Foster Youth' 'Male' 'Asian' 'Hispanic or Latino']

AWARD_CATEGORY:
 ["Bachelor's Degree - Did Not Transfer" 'Associate Degree'
 'Community College Certificate' "Bachelor's Degree - Transferred"]
 ```

 **Range**
 ```
WAGE_YEAR1: 0 - 97993
WAGE_YEAR2: 0 - 132847
WAGE_YEAR3: 0 - 146728
WAGE_YEAR4: 0 - 153910
 ```

 ![alt text](wage_histogram.png)
 The numeric values are not normally distributed. 

 ### Q) Semantics: What is the meaning of the columns? Are any columns related to other columns? (If so, how?)


- `DISTRICT_TYPE` - Geographic aggregation level (School District, Legislative District, or All)
- `DISTRICT_NAME` - Name of the specific district being reported
- `DISTRICT_CODE` - Numeric identifier code for the district
- `ACADEMIC_YEAR` - The academic/school year the data represents
- `DEMO_CATEGORY` - Demographic category of students (race/ethnicity, gender, etc.)
- `STUDENT_POPULATION` - Student subgroup or population segment being measured
- `AWARD_CATEGORY` - Type of credential or award earned by students (diploma, certificate, degree, etc.)
- `WAGE_YEAR1` - Student earnings in the first year after completion/graduation
- `WAGE_YEAR2` - Student earnings in the second year after completion/graduation
- `WAGE_YEAR3` - Student earnings in the third year after completion/graduation
- `WAGE_YEAR4` - Student earnings in the fourth year after completion/graduation


**District Identifiers (Hierarchical):**
- `DISTRICT_TYPE`, `DISTRICT_NAME`, `DISTRICT_CODE` - Three ways to identify the same district (type/category, text name, numeric code)

**Demographic Category-Value Pair:**
- `DEMO_CATEGORY` and `STUDENT_POPULATION` - Category-value relationship where DEMO_CATEGORY defines the dimension (Race, Gender, Homeless Status, Foster Status, All) and STUDENT_POPULATION provides the specific value within that dimension (e.g., Race → "Asian", Gender → "Female")

**Wage Progression (Temporal/Sequential):**
- `WAGE_YEAR1` → `WAGE_YEAR2` → `WAGE_YEAR3` → `WAGE_YEAR4` - Track the same cohort's earnings over time after graduation

**Outcome Relationships (Causal):**
- `AWARD_CATEGORY` → `Wage columns` - Type of credential influences earning trajectory
- `DEMO_CATEGORY` + `STUDENT_POPULATION` → `Wage columns` - Student demographics may reveal wage equity gaps

### Q) Which demographic shows the highest WAGE_YEAR3? Which demographic shows the lowest WAGE_YEAR3?

- Highest: ('Foster Status', 'Not Foster Youth') - $20,893.02
- Lowest: ('Race', 'None Reported') - $42.89

### Q) Are there any people with negative wage trends? Describe these people by their demographics.

- There are no people with negative wage trends. (As seen from cell 12 in the notebook)

### Q) Are there any people with positive wage trends? Describe these people by their demographics.

- Yes. Here are the top 5 demographics with counts > 10 that show positive wage trends:

```
Demographic                                Count    Mean Wage
-----------------------------------------  -----    ----------
Asian                                      174      $34898.20
White                                      244      $31525.92
Male                                       411      $31102.98
Did Not Experience Homelessness in K-12    236      $29582.42
Not Foster Youth                           419      $27618.57
```