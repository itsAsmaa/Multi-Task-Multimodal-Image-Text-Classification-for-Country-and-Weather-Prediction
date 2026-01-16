# Data Concatenation & Cleaning Pipeline – Assignment 3

## 📋 Project Overview

This comprehensive pipeline performs two critical stages for multi-student CSV submissions:

### **Stage 1: Exploratory Data Analysis (EDA)**
- Analyzes raw student submissions before cleaning
- Identifies data quality issues, encoding problems, and schema inconsistencies
- Generates detailed statistical reports and visualizations
- Produces EDA summary reports saved to `processed_files/`

### **Stage 2: Data Cleaning & Consolidation**
- Collects CSV files from multiple student folders
- Handles multiple file encodings (UTF-8, Latin1, ISO-8859-1, CP1252)
- Standardizes inconsistent column names and schemas
- Validates and filters image URLs
- Normalizes categorical labels with intelligent imputation
- Produces a single, clean CSV file ready for **image, text, or multi-modal machine learning tasks**

This pipeline is **mandatory before running the main ML notebooks**.

---

## 📁 Required Files & Setup

### 1. Google Drive Structure

⚠️ **Important Note**: Copy the required files to the folder you will create or use them directly by moving to your "My Drive"

📎 [Access the dataset here](https://drive.google.com/drive/folders/1KjwzSlqG_EnS0HLGd4zvatCPQq5y_WkU?usp=drive_link)


**Notes:**
- Each student folder may contain **one or more CSV files**
- Folders named `processed` or `processed_files` are automatically ignored
- Excluded files: `all_students_final.csv`, `all_students_combined_and_cleaned.csv`

---

### 2. Required Notebook

Upload and open the following file in **Google Colab**:

```
Data_concatenation_and_clean.ipynb
```

---

## 🚀 How to Run the Code

### Step 1: Open in Google Colab

1. Go to [Google Colab](https://colab.research.google.com/)
2. Click **File → Upload notebook**
3. Upload `Data_concatenation_and_clean.ipynb`

---

### Step 2: Mount Google Drive

Run the first cell to mount Google Drive:

```python
from google.colab import drive
drive.mount('/content/drive')
```

Follow the authentication steps:
1. Choose your Google account
2. Allow Colab to access your Drive
3. Confirm the connection

---

### Step 3: Verify Base Directory

The pipeline expects the following path:

```python
BASE_DIR = "/content/drive/MyDrive/Assignment3_ENCS5341/compressed-attachments"
```

⚠️ **If your folder name is different, update this path in TWO locations:**
- In the **EDA section** (Configuration cell)
- In the **Configuration section** (Section #2)

---

### Step 4: Run the Pipeline

Run all cells sequentially:
- **Runtime → Run all**
- or **Ctrl + F9** (Windows/Linux) / **Cmd + F9** (Mac)

#### **The script will execute in stages:**

**Stage 1 - EDA (Exploratory Data Analysis):**
1. Collect all student CSV files
2. Analyze individual submissions (rows, columns, encodings)
3. Generate visualizations:
   - Distribution of rows per student
   - Boxplot of submission sizes
   - Encoding distribution
   - Column count distribution
4. Identify data quality issues and outliers
5. Save EDA reports to `processed_files/`

**Stage 2 - Data Cleaning:**
1. Load CSV files using multiple encoding strategies
2. Normalize column names (handle variations like 'describtion', 'description:', etc.)
3. Standardize to canonical schema
4. Filter invalid Image URLs
5. Normalize categorical variables (Weather, Time of Day, Season)
6. Impute missing values with 'Not Clear'
7. Merge all cleaned datasets
8. Save final consolidated CSV

---

## 📊 Pipeline Features

### **Robust Data Loading**
- Multi-encoding support: UTF-8, Latin1, ISO-8859-1, CP1252
- Automatic handling of malformed rows
- Description column normalization with quote handling

### **Column Standardization**
The pipeline maps various column name variations to standard names:

| **Input Variations** | **Standard Name** |
|---------------------|-------------------|
| image url, image_url, url | Image URL |
| description, description:, describtion | Description |
| country | Country |
| weather | Weather |
| time of day | Time of Day |
| season | Season |
| activity | Activity |
| mood/emotion, mood | Mood/Emotion |

### **Data Validation & Cleaning**
- **Image URLs**: Rows with empty or 'nan' URLs are deleted
- **Categorical normalization**:
  - Weather: sunny, cloudy, rainy, snowy, clear, not clear
  - Time of Day: morning, afternoon, evening, night, not clear
  - Season: spring, summer, fall, autumn, winter, not clear
- **Missing data imputation**: All empty values replaced with "Not Clear"
- **Case normalization**: Title case applied (except Description and Image URL)

---

## 📂 Output Files

After successful execution, outputs will be saved to:

```
compressed-attachments/
└── processed_files/
    ├── RAW_DATA_EDA_REPORT.txt                  # EDA summary report
    ├── student_submission_stats.csv             # Detailed per-student statistics
    └── all_students_combined_and_cleaned.csv    # Final cleaned dataset
```

### **Final Dataset Properties:**
- ✅ UTF-8 encoded
- ✅ Fully cleaned and validated
- ✅ Schema-consistent across all students
- ✅ Ready for ML pipelines (image, text, multimodal)

### **Standard Schema (8 columns):**
```
Image URL | Description | Country | Weather | Time of Day | Season | Activity | Mood/Emotion
```

---

## 📈 EDA Outputs

The EDA stage generates:

### **Visualizations:**
- Distribution histogram of rows per student submission
- Boxplot showing submission size outliers
- Encoding distribution bar chart
- Column count distribution

### **Reports:**
- **RAW_DATA_EDA_REPORT.txt**: Summary statistics, issues detected, top findings
- **student_submission_stats.csv**: Per-file details including:
  - Student name
  - File name
  - Row count
  - Column count
  - Column names
  - Encoding used
  - Error status

### **Console Output:**
- Column name variations analysis
- Unusual submission sizes (outliers)
- Data quality issues summary
- Sample data inspection (first 3 files)

---

## 🔧 Troubleshooting

### **Problem: No CSVs Found**

```python
print(os.listdir(BASE_DIR))
```

**Solution:** Ensure student folders exist inside `compressed-attachments/` and contain CSV files.

---

### **Problem: Drive Not Mounted**

```python
from google.colab import drive
drive.mount('/content/drive', force_remount=True)
```

**Solution:** Clear browser cache and re-authenticate if needed.

---

### **Problem: Output Files Not Created**

Check if output directory exists:

```python
import os
OUTPUT_DIR = os.path.join(BASE_DIR, "processed_files")
print(f"Output directory exists: {os.path.exists(OUTPUT_DIR)}")
print(f"Files in output directory: {os.listdir(OUTPUT_DIR) if os.path.exists(OUTPUT_DIR) else 'N/A'}")
```

---

### **Problem: Encoding Errors**

The pipeline automatically tries multiple encodings. If issues persist:
- Check if CSV files are corrupted
- Verify files are actually CSV format (not Excel saved as CSV)
- Review the `student_submission_stats.csv` for files marked with `Has_Errors=True`

---

### **Problem: Memory Issues (Large Dataset)**

If concatenating many large files causes memory errors:

```python
# Process in smaller batches
batch_size = 50
for i in range(0, len(csv_paths), batch_size):
    batch_paths = csv_paths[i:i+batch_size]
    # Process batch...
```

---

## ✅ Quick Checklist

Before running the pipeline:

- [ ] Google Drive mounted successfully
- [ ] Student CSV files placed in correct folder structure
- [ ] `BASE_DIR` path verified in **both** configuration sections
- [ ] No CSV files opened in Excel/other programs during execution
- [ ] Sufficient storage space in Google Drive
- [ ] All cells executed in order (don't skip cells)

