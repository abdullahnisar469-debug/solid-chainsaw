# solid-chainsaw
Decodlab 
# DecodeLabs - Data Analytics Project 2: Exploratory Data Analysis (EDA)
# Author: Abdullah Nisar

import pandas as pd
import numpy as np

def perform_eda(df):
    print("--- 1. DATA SUMMARY & BASIC STATISTICS ---")
    # Display basic info and count
    print(df.info())
    print("\n--- Five-Number Summary / Descriptive Statistics ---")
    print(df.describe()) # Provides count, mean, std, min, percentiles, max[span_7](start_span)[span_7](end_span)
    
    print("\n--- 2. CHECKING MISSING VALUES ---")
    missing_values = df.isnull().sum()
    print(missing_values)
    
    print("\n--- 3. DETECTING OUTLIERS (IQR METHOD) ---")
    # Example using a numerical column if available, e.g., 'Value' or 'Salary'
    for col in df.select_dtypes(include=[np.number]).columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower_bound = Q1 - (1.5 * IQR)
        upper_bound = Q3 + (1.5 * IQR)
        
        outliers = df[(df[col] < lower_bound) | (df[col] > upper_bound)]
        print(f"Column '{col}': Found {len(outliers)} outliers using IQR[span_8](start_span)[span_8](end_span).")

# --- Main Execution ---
if __name__ == "__main__":
    # Creating a sample dataset for demonstration (IPO Model: Input)[span_9](start_span)[span_9](end_span)
    data = {
        'CustomerID': [101, 102, 103, 104, 105, 106, 107, 108, 109, 110],
        'Age': [25, 32, 47, 51, 22, 38, 41, 29, 65, 33],
        'Monthly_Spend': [150.5, 320.0, 1200.0, 450.2, 99.9, 340.0, 510.5, 210.0, 4500.0, 310.0],
        'Tenure_Months': [12, 24, 36, 48, 6, 18, 30, 12, 60, 24]
    }
    
    df = pd.DataFrame(data)
    
    # Run the EDA process
    perform_eda(df)
