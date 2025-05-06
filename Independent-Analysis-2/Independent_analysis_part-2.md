---
title: "Independent Analysis"
author: "Syed Jafar Raza Rizvi <br> NSID: cfr954 <br> Student ID: 11344782"
output:
  html_document:
    keep_md: true
date: "2025-02-11"
---


``` r
knitr::opts_chunk$set(echo = TRUE)
library(tidyverse)
library(tidymodels)
library(sjPlot)
library(finalfit)
library(knitr)
library(gtsummary)
library(mlbench)
library(kernlab)
library(vip)
library(rsample)
library(tune)
library(recipes)
library(yardstick)
library(parsnip)
library(glmnet)
library(themis)
library(microbenchmark)
library(naniar)
library(parsnip)
```

We are using the imputed (ie. no missing data) version of the synthetic cohort of patients who have no prior history of AF and had a baseline ECG performed between January 2010 and January 2023 , followed by a minimum follow-up of 12 months. 

### Research Questions:
Development and Validation of a New-Onset Atrial Fibrillation Prediction Model?

In this study, we utilized a comprehensive dataset comprising 12-lead electrocardiogram (ECG) measurements, laboratory results, medical history, and demographic variables. Missing data were observed in the laboratory variables, which were addressed using Multiple Imputation by Chained Equations (MICE), a robust statistical method for handling missing values. The imputation process was conducted with 20 imputations and 5 iterations to ensure convergence and stability of the estimates. This approach preserves statistical power and reduces bias while accounting for the uncertainty inherent in missing data.

## Reading data 

``` r
data_synt1 <- read_csv("data_synt1_mice.csv")
```

```
## Rows: 106747 Columns: 120
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr   (1): patient_id
## dbl (119): demographics_age_index_ecg, demographics_birth_sex, hypertension_...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


``` r
get_unique_values <- function(df, vars_to_exclude = NULL) {
  # Initialize results dataframe
  result <- data.frame(
    Variable_Name = character(),
    Unique_Values = character(),
    Is_Boolean = logical(),
    # Value_Count = integer(),
    stringsAsFactors = FALSE
  )
  
  # Get columns to analyze (excluding specified vars)
  cols_to_analyze <- setdiff(names(df), vars_to_exclude)
  
  for (col in cols_to_analyze) {
    # Get complete unique values (including NA)
    unique_vals <- unique(df[[col]])
    na_present <- any(is.na(unique_vals))
    na_sum<-sum(is.na(df[[col]]))
    na_sum_per<-((sum(is.na(df[[col]])))/length(df[[col]]))*100
    
    # Remove NA for boolean detection
    clean_vals <- unique_vals[!is.na(unique_vals)]
    val_count <- length(clean_vals)
    
    # Detect boolean variables (0/1 or 1/2 numeric)
    is_boolean <- if (val_count <= 2 && is.numeric(df[[col]])) {
      all(clean_vals %in% c(0, 1)) || all(clean_vals %in% c(1, 2))
    } else {
      FALSE
    }
    
    # Prepare values for display
    if (na_present) {
      display_vals <- c(sort(clean_vals), NA)
    } else {
      display_vals <- sort(clean_vals)
    }
    
    # Convert to character representation
    char_vals <- sapply(display_vals, function(x) {
      if (is.na(x)) "NA" else as.character(x)
    })
    
    result <- rbind(result, data.frame(
      Variable_Name = col,
      Unique_Values = paste(char_vals, collapse = ", "),
      Is_Boolean = is_boolean,
      Value_Count = val_count,
      missing=na_sum,
      missing_per=na_sum_per,
      stringsAsFactors = FALSE
    ))
  }
  
  return(result)
}
unique_values <- get_unique_values(data_synt1)
table(unique_values$Is_Boolean)
```

```
## 
## FALSE  TRUE 
##    26    94
```

``` r
unique_values<- unique_values %>%
  filter(Variable_Name!="patient_id")
unique_values1<- unique_values %>%
  filter(Value_Count==1)
print(unique_values1$Variable_Name)
```

```
## [1] "ecg_resting_afib"                           
## [2] "ecg_resting_aflutter"                       
## [3] "ranolazine_peri"                            
## [4] "diuretic_vasopressin_antagonist_peri"       
## [5] "amyloid_therapeutics_tafamidis_peri"        
## [6] "amyloid_therapeutics_patisiran_peri"        
## [7] "amyloid_therapeutics_inotersen_peri"        
## [8] "glucose_ohg_other_peri"                     
## [9] "smoking_cessation_nicotine_replacement_peri"
```
those variable have only outcome. so we are going to drop those variables.


``` r
data_synt1 <- data_synt1 %>% 
  select(-any_of(unique_values1$Variable_Name))
```

for this analysis we only consider the ECG variable which are

Heart rate from index 12 lead ECG [ecg_resting_hr]
PR interval duration from index 12 lead ECG [ecg_resting_pr]
QRS complex duration from index 12 lead ECG [ecg_resting_qrs]
Corrected QT interval  from index 12 lead ECG [ecg_resting_qtc]
Atrial fibrillation in index 12 lead ECG [ecg_resting_afib]
Paced rhythm in index 12 lead ECG [ecg_resting_paced]
Bigeminy in index 12 lead ECG [ecg_resting_bigeminy]
Left bundle branch block in index 12 lead ECG [ecg_resting_LBBB]
Right bundle branch block in index 12 lead ECG [ecg_resting_RBBB]
Incomplete left bundle branch block in index 12 lead ECG [ecg_resting_incomplete_LBBB]
Incomplete right bundle branch block in index 12 lead ECG [ecg_resting_incomplete_RBBB]
Left anterior fascicular block in index 12 lead ECG [ecg_resting_LAFB]
Left posterior fascicular block in index 12 lead ECG [ecg_resting_LPFB]
Bifascicular block in index 12 lead ECG [ecg_resting_bifascicular_block]
Trifascicular block in index 12 lead ECG [ecg_resting_trifascicular_block]
Intra-ventricular conduction delay in  index 12 lead ECG [ecg_resting_intraventricular_conduction_delay]
Chronological age at time of referenced index ECG, rounded down to nearest whole number [demographics_age_index_ecg]
Sex assigned at birth [demographics_birth_sex]
ICD-10 coding of hypertension in either DAD or NACRS databases at any time prior to or 6 months after date of index 12 lead ECG [hypertension_icd10]
Documented presence of hyperglycaemic state inclusive of Type 1 diabetes, Type 2 diabetes, Pre-diabetes, or Impaired fasting glucose (treated or untreated) by any of: labs, medications, or ICD-10,  at any time prior to or 6 months after date of index 12 lead ECG [diabetes_combined]
Documented presence of dyslipidemia (treated or untreated) by any of: labs, medications, or ICD-10,  at any time prior to or 6 months after date of index 12 lead ECG [dyslipidemia_combined]
ICD-10 coded presence of dilated cardiomyopathy at any time prior to or 6 months after date of index 12 lead ECG [dcm_icd10]
ICD-10 coded presence of hypertrophic cardiomyopathy at any time prior to or 6 months after date of index 12 lead ECG [hcm_icd10]
ICD-10 coded presence of acute myocarditis at any time prior to date of index 12 lead ECG [myocarditis_icd10_prior]
ICD-10 coded presence of acute pericarditis at any time prior todate of index 12 lead ECG [pericarditis_icd10_prior]
ICD-10 coded presence of aortic dilatation/aneurysm at any time prior to or 6 months after date of index 12 lead ECG [aortic_aneurysm_icd10]
ICD-10 coded presence of aortic dissection at any time prior to date of index 12 lead ECG [aortic_dissection_icd10_prior]
ICD-10 coded presence of pulmonary hypertension at any time prior to or 6 months after date of index 12 lead ECG [pulmonary_htn_icd10]
ICD-10 coded presence of amyloidosis at any time prior to or 6 months after date of index 12 lead ECG [amyloid_icd10]
ICD-10 coded presence of chronic obstructive airway disease (COPD) at any time prior to or 6 months after date of index 12 lead ECG [copd_icd10]
ICD-10 coded presence of hyperthyroidism at any time prior to or 6 months after date of index 12 lead ECG [hyperthyroid_icd10]
ICD-10 coded presence of hypothyroidism at any time prior to or 6 months after date of index 12 lead ECG [hypothyroid_icd10]
ICD-10 coded presence of rheumatoid arthritis at any time prior to or 6 months after date of index 12 lead ECG [rheumatoid_arthritis_icd10]
ICD-10 coded presence of systemic lupus erythematosus (SLE) at any time prior to or 6 months after date of index 12 lead ECG [sle_icd10]
ICD-10 coded presence of sarcoidosis at any time prior to or 6 months after date of index 12 lead ECG [sarcoid_icd10]
ICD-10 coded presence of cancer at any time prior to or 6 months after date of index 12 lead ECG [cancer_any_icd10]


``` r
data_synt1 <- data_synt1 %>%
  dplyr::select(ecg_resting_hr,
ecg_resting_pr,
ecg_resting_qrs,
ecg_resting_qtc,
ecg_resting_paced,
ecg_resting_bigeminy,
ecg_resting_LBBB,
ecg_resting_RBBB,
ecg_resting_incomplete_LBBB,
ecg_resting_incomplete_RBBB,
ecg_resting_LAFB,
ecg_resting_LPFB,
ecg_resting_bifascicular_block,
ecg_resting_trifascicular_block,
ecg_resting_intraventricular_conduction_delay,
outcome_afib_aflutter_new_post,
demographics_age_index_ecg,
demographics_birth_sex,
hypertension_icd10,
diabetes_combined,
dyslipidemia_combined,
dcm_icd10,
hcm_icd10,
myocarditis_icd10_prior,
pericarditis_icd10_prior,
aortic_aneurysm_icd10,
aortic_dissection_icd10_prior,
pulmonary_htn_icd10,
amyloid_icd10,
copd_icd10,
hyperthyroid_icd10,
hypothyroid_icd10,
rheumatoid_arthritis_icd10,
sle_icd10,
sarcoid_icd10,
cancer_any_icd10)
```

**Missing Data Information**


``` r
missing_table <- miss_var_summary(data_synt1)
missing_table
```

```
## # A tibble: 36 × 3
##    variable                    n_miss pct_miss
##    <chr>                        <int>    <num>
##  1 ecg_resting_hr                   0        0
##  2 ecg_resting_pr                   0        0
##  3 ecg_resting_qrs                  0        0
##  4 ecg_resting_qtc                  0        0
##  5 ecg_resting_paced                0        0
##  6 ecg_resting_bigeminy             0        0
##  7 ecg_resting_LBBB                 0        0
##  8 ecg_resting_RBBB                 0        0
##  9 ecg_resting_incomplete_LBBB      0        0
## 10 ecg_resting_incomplete_RBBB      0        0
## # ℹ 26 more rows
```


``` r
factor_vars <- unique_values %>% 
  filter(Is_Boolean== TRUE) %>% 
  pull(Variable_Name)
data_synt1 <- data_synt1 %>% 
  mutate(across(any_of(factor_vars), as.factor))
data_synt1$patient_id<-NULL
```


``` r
table(data_synt1$outcome_afib_aflutter_new_post)
```

```
## 
##      0      1 
## 100256   6491
```

### Prepare the data split and cross validation folds


``` r
set.seed(10)

#### Cross Validation Split
cv_split <- initial_validation_split(data_synt1, 
                            strata = outcome_afib_aflutter_new_post, 
                            prop = c(0.70, 0.20))

# Create data frames for the two sets:
train_data <- training(cv_split)
table(train_data$outcome_afib_aflutter_new_post)
```

```
## 
##     0     1 
## 70238  4484
```

``` r
test_data  <- testing(cv_split)
table(test_data$outcome_afib_aflutter_new_post)
```

```
## 
##     0     1 
## 10005   670
```
### V folds


``` r
folds <- vfold_cv(training(cv_split), v = 5, strata = outcome_afib_aflutter_new_post)
```




``` r
all_recipe <- 
  recipe(outcome_afib_aflutter_new_post ~ ., data = train_data) %>%
  step_smotenc(outcome_afib_aflutter_new_post, over_ratio = 0.9) %>%
  step_dummy(all_nominal_predictors()) %>%
  step_zv(all_predictors(), -all_outcomes()) %>%
  step_normalize(all_numeric_predictors())
```

### logistic regression 


``` r
logistic_model <- logistic_reg(penalty = tune(), mixture = tune(),
                                mode = "classification",
                                engine = "glmnet"
                               )

logistic_workflow <- workflow() %>% 
          add_model(logistic_model) %>% 
          add_recipe(all_recipe) %>% 
          tune_grid(resamples = folds,
                    control = control_grid(save_pred = TRUE, 
                                            verbose = FALSE)) ## Edit for running live

collect_metrics(logistic_workflow) 
```

```
## # A tibble: 30 × 8
##          penalty mixture .metric     .estimator   mean     n  std_err .config   
##            <dbl>   <dbl> <chr>       <chr>       <dbl> <int>    <dbl> <chr>     
##  1 0.00633        0.0659 accuracy    binary     0.916      5 0.000752 Preproces…
##  2 0.00633        0.0659 brier_class binary     0.0645     5 0.000504 Preproces…
##  3 0.00633        0.0659 roc_auc     binary     0.961      5 0.000787 Preproces…
##  4 0.00000000138  0.214  accuracy    binary     0.916      5 0.000730 Preproces…
##  5 0.00000000138  0.214  brier_class binary     0.0637     5 0.000528 Preproces…
##  6 0.00000000138  0.214  roc_auc     binary     0.960      5 0.000920 Preproces…
##  7 0.000163       0.269  accuracy    binary     0.916      5 0.000722 Preproces…
##  8 0.000163       0.269  brier_class binary     0.0637     5 0.000527 Preproces…
##  9 0.000163       0.269  roc_auc     binary     0.960      5 0.000916 Preproces…
## 10 0.00000207     0.351  accuracy    binary     0.916      5 0.000717 Preproces…
## # ℹ 20 more rows
```



``` r
show_best(logistic_workflow, metric='accuracy', n=5)  # only show the results for the best 5 models
```

```
## # A tibble: 5 × 8
##       penalty mixture .metric  .estimator  mean     n  std_err .config          
##         <dbl>   <dbl> <chr>    <chr>      <dbl> <int>    <dbl> <chr>            
## 1 0.725        0.682  accuracy binary     0.940     5 0.000915 Preprocessor1_Mo…
## 2 0.00633      0.0659 accuracy binary     0.916     5 0.000752 Preprocessor1_Mo…
## 3 0.000163     0.269  accuracy binary     0.916     5 0.000722 Preprocessor1_Mo…
## 4 0.000000175  0.457  accuracy binary     0.916     5 0.000713 Preprocessor1_Mo…
## 5 0.0000128    0.890  accuracy binary     0.916     5 0.000667 Preprocessor1_Mo…
```

``` r
autoplot(logistic_workflow, metric = 'accuracy') 
```

![](Independent_analysis_part-2_files/figure-html/unnamed-chunk-14-1.png)<!-- -->
### Random Forest 


``` r
cores <- parallel::detectCores()
cores
```

```
## [1] 11
```


``` r
rf_model <- rand_forest(mtry = tune(), min_n = tune(), trees = tune()) %>% 
              set_engine("ranger", num.threads = cores) %>% 
              set_mode("classification")

rf_workflow <- workflow() %>% 
          add_model(rf_model) %>% 
          add_recipe(all_recipe) %>% 
          tune_grid(resamples = folds,
                    control = control_grid(save_pred = TRUE, 
                                            verbose = FALSE)) ## Edit for running live
```

```
## i Creating pre-processing data to finalize unknown parameter: mtry
```


``` r
collect_metrics(rf_workflow) 
```

```
## # A tibble: 30 × 9
##     mtry trees min_n .metric     .estimator   mean     n  std_err .config       
##    <int> <int> <int> <chr>       <chr>       <dbl> <int>    <dbl> <chr>         
##  1    12   869    31 accuracy    binary     0.952      5 0.000355 Preprocessor1…
##  2    12   869    31 brier_class binary     0.0360     5 0.000274 Preprocessor1…
##  3    12   869    31 roc_auc     binary     0.969      5 0.00126  Preprocessor1…
##  4    22  1161     3 accuracy    binary     0.957      5 0.000326 Preprocessor1…
##  5    22  1161     3 brier_class binary     0.0327     5 0.000262 Preprocessor1…
##  6    22  1161     3 roc_auc     binary     0.967      5 0.00145  Preprocessor1…
##  7    29  1835    14 accuracy    binary     0.955      5 0.000463 Preprocessor1…
##  8    29  1835    14 brier_class binary     0.0340     5 0.000279 Preprocessor1…
##  9    29  1835    14 roc_auc     binary     0.966      5 0.00154  Preprocessor1…
## 10    17  1530    12 accuracy    binary     0.955      5 0.000409 Preprocessor1…
## # ℹ 20 more rows
```


``` r
show_best(rf_workflow, metric='accuracy', n=5)  # only show the results for the best 5 models
```

```
## # A tibble: 5 × 9
##    mtry trees min_n .metric  .estimator  mean     n  std_err .config            
##   <int> <int> <int> <chr>    <chr>      <dbl> <int>    <dbl> <chr>              
## 1    22  1161     3 accuracy binary     0.957     5 0.000326 Preprocessor1_Mode…
## 2    21  1388     8 accuracy binary     0.956     5 0.000341 Preprocessor1_Mode…
## 3    17  1530    12 accuracy binary     0.955     5 0.000409 Preprocessor1_Mode…
## 4    29  1835    14 accuracy binary     0.955     5 0.000463 Preprocessor1_Mode…
## 5    27    97    21 accuracy binary     0.954     5 0.000385 Preprocessor1_Mode…
```


``` r
autoplot(rf_workflow, metric = 'accuracy') 
```

![](Independent_analysis_part-2_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

<!-- #### Support Vector Machine -->

<!-- ```{r} -->
<!-- svm_model <- svm_rbf(cost = tune(), rbf_sigma = tune()) %>%  -->
<!--   set_mode("classification") %>% -->
<!--   set_engine("kernlab") -->

<!-- svm_workflow <- workflow() %>%  -->
<!--           add_model(svm_model) %>%  -->
<!--           add_recipe(all_recipe) %>%  -->
<!--           tune_grid(resamples = folds, -->
<!--                     control = control_grid(save_pred = FALSE,  -->
<!--                                             verbose = FALSE)) ## Edit for running live -->
<!-- ``` -->

<!-- ```{r} -->
<!-- collect_metrics(svm_workflow)  -->
<!-- ``` -->

<!-- ```{r} -->
<!-- show_best(svm_workflow, metric='accuracy', n=5)  # only show the results for the best 5 models -->
<!-- ``` -->

<!-- ```{r} -->
<!-- autoplot(svm_workflow, metric = 'accuracy')  -->
<!-- ``` -->

### Best Model 

## logistic Regression


``` r
logistic_best <- 
  logistic_workflow %>% 
  select_best(metric = "brier_class")

logistic_final_model <- finalize_model(
                          logistic_model,
                          logistic_best
                          )
logistic_final_model
```

```
## Logistic Regression Model Specification (classification)
## 
## Main Arguments:
##   penalty = 4.15464079456826e-08
##   mixture = 0.928711206504377
## 
## Computational engine: glmnet
```


``` r
final_logistic_workflow <- workflow() %>%
                      add_recipe(all_recipe) %>%
                      add_model(logistic_final_model)

final_logistic_results <- final_logistic_workflow %>%
                    last_fit(cv_split)

lr_results <- final_logistic_results %>% collect_metrics()
```


## Random Forest


``` r
rf_best <- 
  rf_workflow %>% 
  select_best(metric = "brier_class")

rf_final_model <- finalize_model(
                          rf_model,
                          rf_best
                          )
rf_final_model
```

```
## Random Forest Model Specification (classification)
## 
## Main Arguments:
##   mtry = 22
##   trees = 1161
##   min_n = 3
## 
## Engine-Specific Arguments:
##   num.threads = cores
## 
## Computational engine: ranger
```


``` r
final_rf_workflow <- workflow() %>%
                      add_recipe(all_recipe) %>%
                      add_model(rf_final_model)

final_rf_results <- final_rf_workflow %>%
                    last_fit(cv_split)

rf_results <- final_rf_results %>% collect_metrics()
```

<!-- ## Support Vector Machine -->

<!-- ```{r} -->
<!-- svm_best <-  -->
<!--   svm_workflow %>%  -->
<!--   select_best(metric = "brier_class") -->

<!-- svm_final_model <- finalize_model( -->
<!--                           svm_model, -->
<!--                           svm_best -->
<!--                           ) -->
<!-- svm_final_model -->
<!-- ``` -->

<!-- ```{r} -->
<!-- final_svm_workflow <- workflow() %>% -->
<!--                       add_recipe(all_recipe) %>% -->
<!--                       add_model(svm_final_model) -->

<!-- final_svm_results <- final_svm_workflow %>% -->
<!--                       last_fit(cv_split) -->

<!-- # svm_results <- final_svm_results %>% collect_metrics() -->
<!-- ``` -->

### Final Resul

## Logistic Regression 


``` r
kable(lr_results)
```



|.metric     |.estimator | .estimate|.config              |
|:-----------|:----------|---------:|:--------------------|
|accuracy    |binary     | 0.9127869|Preprocessor1_Model1 |
|roc_auc     |binary     | 0.9638731|Preprocessor1_Model1 |
|brier_class |binary     | 0.0645191|Preprocessor1_Model1 |

## Random Forest 


``` r
kable(rf_results)
```



|.metric     |.estimator | .estimate|.config              |
|:-----------|:----------|---------:|:--------------------|
|accuracy    |binary     | 0.9573770|Preprocessor1_Model1 |
|roc_auc     |binary     | 0.9696015|Preprocessor1_Model1 |
|brier_class |binary     | 0.0320880|Preprocessor1_Model1 |

Comment: The accuracy of the random forest model is 0.95, which is higher than the logistic model, which is 0.91. However, the area of the ROC curve is a bit higher for the random forest model (0.97) than the logistic model (0.96)

<!-- ## SVM  -->

<!-- ```{r} -->
<!-- kable(svm_results) -->
<!-- ``` -->


