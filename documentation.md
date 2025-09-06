Name: Enis Kadiroğlu
E-mail: enis.kadiroglu@ogr.dpu.edu.tr

Date: 06.09.2025
Name Surname: Enis Kadiroğlu
E-mail: enis.kadiroglu@ogr.dpu.edu.tr
Date: 09/06/2025

### Patient Data Exploratory Data Analysis (EDA) Report
# 1. Executive Summary
This report summarizes the findings of the Exploratory Data Analysis (EDA) process conducted on patient data obtained from the projectpus.xlsx file. The main objective of the analysis is to understand the patient demographics, treatment characteristics, and the relationships between variables within the dataset, as well as to assess data quality and derive insights that will form the basis for future modeling studies.

The analysis concluded that the patient population is predominantly composed of middle-aged women, with the most common treatment session counts being 15, 10, and 20. No strong correlation was observed between numerical variables such as age and treatment duration. The significant amount of missing data and duplicate records in the dataset highlights the importance of data preprocessing steps.

# 2. Data Preprocessing and Cleaning
To improve data quality before starting the analysis, the following steps were implemented:

Removal of Duplicate Data: Duplicate rows in the dataset were identified using the df.duplicated().sum() command and removed with the df.drop_duplicates() function to prevent bias in the analysis.

Missing Data Detection: Missing values in the dataset were examined using df.isnull().sum(). The high rate of missing data, especially in the Alerji (Allergy), KanGrubu (Blood Type), and KronikHastalik (Chronic Disease) columns, necessitates a cautious approach in further analyses involving these variables.

# 3. Analysis and Key Findings
# 3.1. Demographic Analysis
Age Distribution: An examination of the patient age distribution reveals that the population is concentrated in the 30-60 age range. This indicates that the dataset primarily covers middle-aged and older individuals.

Gender Distribution: As noted in previous analyses, the majority of patients in the dataset are female.

# 3.2. Analysis of Treatment Characteristics
Number of Treatment Sessions: When analyzing the distribution of the TedaviSuresi_Numerical column, it is observed that a large portion of the treatments are planned for 15 sessions. This is followed by 10 sessions and 20 sessions, respectively. This points to the existence of standardized treatment packages. Lower or higher session counts are seen less frequently.

# 3.3. Analysis of Relationships Between Variables
Gender and Treatment Duration: A box plot was examined to understand whether gender has a significant effect on the treatment duration (number of sessions). The graph showed that the median treatment durations for male and female patients are very close, with no significant difference in their distributions. This finding suggests that treatment duration planning is not a gender-dependent factor.

Correlation Between Numerical Variables: A correlation matrix was created and visualized with a heatmap to measure the relationship between numerical variables such as Yas (Age), TedaviSuresi_Numerical, and UygulamaSuresi_Sayi.

Finding: The heatmap indicated that there is no strong linear relationship among the examined numerical variables. For instance, there is no significant correlation between the patient's age and the required number of treatment sessions (-0.03). This suggests that treatment planning depends more on other factors like the diagnosis and the patient's current condition rather than their age.

# 4. Conclusion and Recommendations
This exploratory data analysis has successfully revealed the basic structure and characteristics of the patient and treatment data.

Key Takeaways:
Target Audience: The patient profile served is predominantly middle-aged women.
Standard Treatment Packages: Treatment plans of 10, 15, and 20 sessions are common. This may indicate operational efficiency or standard protocols for specific diagnostic groups.

Unrelated Variables: Demographic characteristics such as the patient's age and gender do not appear to be direct factors influencing treatment duration, at least on the basis of session count.
###  DATA PRE PROCESS
Data Preprocessing Pipeline Documentation
# 1. Overview

This project is designed to perform a comprehensive preprocessing workflow on a medical dataset.
The goal is to clean raw data and make it ready for machine learning models.

The implementation is built on top of the Scikit-Learn Pipeline architecture, ensuring that preprocessing steps are consistent and reproducible.

# 2. Libraries Used

pandas, numpy → Data manipulation

scikit-learn → Pipeline, preprocessing, train/test splitting

sys → Error handling

# 3. Main Classes and Functions
# 3.1 GuvenliEtiketleyici (Safe Label Encoder)

A custom transformer compatible with Scikit-Learn
Provides a safe version of LabelEncoder
Creates a separate encoder for each column
Unseen categories in the test set are encoded as -1
Missing values are replaced with "EKSİK_DEGER" before encoding

# 3.2 VeriOnIsleyici (Data Preprocessor)
The core class for loading, cleaning, and preprocessing raw data
# Methods

veri_yukle()
Loads the Excel file and strips whitespace from column names
kapsamli_temizlik() (comprehensive cleaning)
Removes unnecessary columns (HastaNo, KanGrubu)
Handles missing values with appropriate strategies
UygulamaSuresi → Extracts minutes, fills missing with median
Alerji, KronikHastalik, UygulamaYerleri → Replaced with default values
Cinsiyet → Filled with mode (most frequent value)
Removes duplicate rows
pipeline_olustur_ve_calistir(target_column, test_size, random_state)
Splits data into features (X) and target (y)
For numerical columns
Missing values filled with median
Standardized with StandardScaler
For categorical columns
Missing values filled with a constant
Encoded with GuvenliEtiketleyici
Produces training and test datasets
veri_ozeti_goster(df, title)
Displays dataset shape and missing value summary

# 4. Workflow

Load the data

processor = VeriOnIsleyici("projectpus.xlsx")
processor.veri_yukle()
Show pre-cleaning summary
processor.veri_ozeti_goster(processor.orijinal_veri, "Pre-cleaning Data")
Clean the data
cleaned_data = processor.kapsamli_temizlik()
Show post-cleaning summary
processor.veri_ozeti_goster(cleaned_data, "Post-cleaning Data")
# Run the preprocessing pipeline

X_train, X_test, y_train, y_test = processor.pipeline_olustur_ve_calistir(
    target_column="TedaviSuresi",
    test_size=0.2,
    random_state=42
)

# 5. Example Output
DATA PREPROCESSING PIPELINE STARTED
 Data loaded successfully. Shape: (350, 12)

 === PRE-CLEANING DATA ===
Shape: (350, 12)
Missing Values:
UygulamaSuresi     20
Cinsiyet            5
...

 Data cleaning in progress...
 Cleaning completed. Final shape: (340, 10)

 === POST-CLEANING DATA ===
 No missing values detected.
------------------------------

Pipeline executed successfully.

PIPELINE COMPLETED
------------------------------
RESULT SUMMARY
 Processed Training Data Shape: (272, 25)
 Processed Test Data Shape:    (68, 25)
 Training Target Count: 272
 Test Target Count:     68

 You can now train machine learning models:
   Usage: model.fit(X_train, y_train)

# 6. Conclusion

With this pipeline

Raw data is systematically cleaned

Missing values, duplicates, and categorical variables are handled safely

The process is reproducible and transparent

Final outputs can be fed directly into machine learning algorithms
