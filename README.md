# Calorie Expenditure Prediction Model

## Project Overview
Machine learning pipeline to predict calories burned during workouts based on biometric and activity data.  
**Best Model**: Polynomial Regression (R²: 0.95, MAE: ~44 kcal)

## Dataset Features
- **Biometrics**: 
  - Age (18-59 after outlier removal)  
  - Gender (52.5% Male, 47.5% Female)  
  - Weight (57-77kg), Height (1.62-1.78m), BMI (19-27)  
  - Fat_Percentage (13-35%)  
- **Activity Metrics**:  
  - BPM (Max: 170-189, Avg: 121-156, Resting: 50-74)  
  - Session_Duration (0.63-1.88 hours - strongest predictor)  
  - Workout_Type (Yoga 24.6%, HIIT 22.7%, Cardio 26.2%, Strength 26.5%)  
- **Lifestyle**:  
  - Water_Intake (2.1-3.7 liters)  
  - Workout_Frequency (3-4 days/week most common)  
  - Experience_Level (41.7% Level 2)  

## Key Steps
1. **Preprocessing**:
   - Removed 24% outliers using IQR (fold=1.0)
   - Label encoded categoricals (Gender, Workout_Type, Experience_Level)
   - MinMax scaled numerical features

2. **Feature Analysis**:
   - Session Duration → 0.87 correlation with calories
   - Avg_BPM & Workout_Frequency → Secondary predictors
   - BMI-Weight correlation: 0.81 (expected)

3. **Modeling**:
   - **Polynomial Regression**: Best performance (R²: 0.95, MAE: ~44 kcal)
   - **Random Forest**: Competitive results (R²: 0.92-0.94 range across splits)
   - **OLS Regression**: Identified significant predictors:
     - Gender (p<0.001) 
     - Session Duration (p<0.001)
     - BMI (p=0.038)

4. **Validation**:
   - 3 random splits (random_state=42,7,99) → Consistent results
   - 5-fold cross-validation
   - Residual analysis (Studentized residuals <|2.37|)

## Key Findings
- **Top 3 Influencers**:  
  1. Session Duration (87% correlation)  
  2. Avg_BPM  
  3. Gender (Males burn +86 kcal on avg)  
- **Insignificant Features**: Experience_Level, Fat_Percentage (p>0.8)  
- **Non-linear Effects**: BMI & Water_Intake show threshold effects  

