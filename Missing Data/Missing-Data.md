---
title: "Missing Data"
author: "Syed Jafar Raza Rizvi <br> NSID: cfr954 <br> Student ID: 11344782"
output:
  html_document:
    keep_md: true
date: "2025-02-11"
zotero: true
bibliography: scholar.bib
---


# 1. **Dataset Exploration**  
   - Load the provided health administrative dataset.  
   - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.  
   - Summarize findings using tables, charts, or heatmaps to visualize missingness.  
   
## - Load the provided health administrative dataset.

``` r
data<-read.csv("can_path_data.csv")
# data <- data %>% select(ID:HS_GEN_HEALTH, PA_TOTAL_SHORT, PM_BMI_SR, contains("_EVER"), contains("WRK_"))
```

## - Explore the dataset to identify the extent, patterns, and potential reasons for missing data.

### Explore Dataset 

**Check the structure of the dataset**


``` r
dim(data)
```

```
## [1] 41187   440
```

``` r
df_info <- data.frame(
  Variable = names(data), 
  Type = sapply(data, class)  # Gets the data type of each variable
)
print(df_info, row.names = FALSE)  # Print full output
```

```
##                             Variable      Type
##                                   ID character
##                         ADM_STUDY_ID   integer
##                           SDC_GENDER   integer
##                         SDC_AGE_CALC   integer
##                   SDC_MARITAL_STATUS   integer
##                        SDC_EDU_LEVEL   integer
##                    SDC_EDU_LEVEL_AGE   integer
##                           SDC_INCOME   integer
##                    SDC_INCOME_IND_NB   integer
##              SDC_HOUSEHOLD_ADULTS_NB   integer
##            SDC_HOUSEHOLD_CHILDREN_NB   integer
##                        HS_GEN_HEALTH   integer
##                HS_ROUTINE_VISIT_EVER   integer
##                HS_ROUTINE_VISIT_LAST   integer
##                 HS_DENTAL_VISIT_EVER   integer
##                 HS_DENTAL_VISIT_LAST   integer
##                         HS_FOBT_EVER   integer
##                         HS_FOBT_LAST   integer
##                          HS_COL_EVER   integer
##                          HS_COL_LAST   integer
##                          HS_SIG_EVER   integer
##                          HS_SIG_LAST   integer
##                      HS_SIG_COL_EVER   integer
##                      HS_SIG_COL_LAST   integer
##                        HS_POLYP_EVER   integer
##                          HS_PSA_EVER   integer
##                          HS_PSA_LAST   integer
##                 MH_CHILDREN_FATHERED   integer
##                  WH_MENSTRUATION_AGE   integer
##               WH_CONTRACEPTIVES_EVER   integer
##                WH_CONTRACEPTIVES_AGE   integer
##           WH_CONTRACEPTIVES_DURATION   integer
##                         WH_GRAVIDITY   integer
##                    WH_PREG_FIRST_AGE   integer
##                          WH_PREG_CUR   integer
##                       WH_PREG_CUR_WK   integer
##                     WH_PREG_LAST_AGE   integer
##            WH_BREASTFEEDING_DURATION   integer
##                          WH_HFT_EVER   integer
##                    WH_MENOPAUSE_EVER   integer
##                  WH_MENOPAUSE_REASON   integer
##                     WH_MENOPAUSE_AGE   integer
##                          WH_HRT_EVER   integer
##                           WH_HRT_AGE   integer
##                      WH_HRT_DURATION   integer
##                 WH_HYSTERECTOMY_EVER   integer
##                  WH_HYSTERECTOMY_AGE   integer
##                 WH_OOPHORECTOMY_EVER   integer
##                WH_OVARIES_REMOVED_NB   integer
##                   WH_BI_OOPHORECTOMY   integer
##                  WH_OVARIES_LAST_AGE   integer
##                          HS_MMG_EVER   integer
##                          HS_MMG_LAST   integer
##                          HS_PAP_EVER   integer
##                          HS_PAP_LAST   integer
##                         DIS_HBP_EVER   integer
##                          DIS_HBP_AGE   integer
##                           DIS_HBP_TX   integer
##                          DIS_MI_EVER   integer
##                           DIS_MI_AGE   integer
##                            DIS_MI_TX   integer
##                      DIS_STROKE_EVER   integer
##                       DIS_STROKE_AGE   integer
##                        DIS_STROKE_TX   integer
##                      DIS_ASTHMA_EVER   integer
##                       DIS_ASTHMA_AGE   integer
##                        DIS_ASTHMA_TX   integer
##                   DIS_EMPHYSEMA_EVER   integer
##                    DIS_EMPHYSEMA_AGE   integer
##                     DIS_EMPHYSEMA_TX   integer
##                          DIS_CB_EVER   integer
##                           DIS_CB_AGE   integer
##                            DIS_CB_TX   integer
##                        DIS_COPD_EVER   integer
##                         DIS_COPD_AGE   integer
##                          DIS_COPD_TX   integer
##                         DIS_DEP_EVER   integer
##                          DIS_DEP_AGE   integer
##                        DIS_DIAB_EVER   integer
##                        DIS_DIAB_TYPE   integer
##                         DIS_DIAB_AGE   integer
##                          DIS_DIAB_TX   integer
##                          DIS_LC_EVER   integer
##                           DIS_LC_AGE   integer
##                          DIS_CH_EVER   integer
##                           DIS_CH_AGE   integer
##                       DIS_CROHN_EVER   integer
##                        DIS_CROHN_AGE   integer
##                          DIS_UC_EVER   integer
##                           DIS_UC_AGE   integer
##                         DIS_IBS_EVER   integer
##                          DIS_IBS_AGE   integer
##                      DIS_ECZEMA_EVER   integer
##                       DIS_ECZEMA_AGE   integer
##                         DIS_SLE_EVER   integer
##                          DIS_SLE_AGE   integer
##                          DIS_PS_EVER   integer
##                           DIS_PS_AGE   integer
##                          DIS_MS_EVER   integer
##                           DIS_MS_AGE   integer
##                          DIS_OP_EVER   integer
##                           DIS_OP_AGE   integer
##                   DIS_ARTHRITIS_EVER   integer
##                    DIS_ARTHRITIS_AGE   integer
##                  DIS_ARTHRITIS_TYPE1   integer
##                  DIS_ARTHRITIS_TYPE2   integer
##                  DIS_ARTHRITIS_TYPE3   integer
##                      DIS_CANCER_EVER   integer
##                          DIS_CANCER1   integer
##                      DIS_CANCER1_AGE   integer
##                       DIS_CANCER1_TX   integer
##                 DIS_CANCER1_TX_CHEMO   integer
##                   DIS_CANCER1_TX_RAD   integer
##                  DIS_CANCER1_TX_SURG   integer
##                 DIS_CANCER1_TX_OTHER   integer
##                     DIS_HBP_FAM_EVER   integer
##                      DIS_MI_FAM_EVER   integer
##                  DIS_STROKE_FAM_EVER   integer
##                  DIS_ASTHMA_FAM_EVER   integer
##               DIS_EMPHYSEMA_FAM_EVER   integer
##                      DIS_CB_FAM_EVER   integer
##                    DIS_COPD_FAM_EVER   integer
##                     DIS_DEP_FAM_EVER   integer
##                    DIS_DIAB_FAM_EVER   integer
##                      DIS_LC_FAM_EVER   integer
##                      DIS_CH_FAM_EVER   integer
##                   DIS_CROHN_FAM_EVER   integer
##                      DIS_UC_FAM_EVER   integer
##                     DIS_IBS_FAM_EVER   integer
##                  DIS_ECZEMA_FAM_EVER   integer
##                     DIS_SLE_FAM_EVER   integer
##                      DIS_PS_FAM_EVER   integer
##                      DIS_MS_FAM_EVER   integer
##                      DIS_OP_FAM_EVER   integer
##               DIS_ARTHRITIS_FAM_EVER   integer
##                  DIS_CANCER_FAM_EVER   integer
##                    DIS_CANCER_F_EVER   integer
##                    DIS_CANCER_M_EVER   integer
##                  DIS_CANCER_SIB_EVER   integer
##                DIS_CANCER_CHILD_EVER   integer
##                             SLE_TIME   integer
##                         SLE_TIME_CAT   integer
##                     SLE_TROUBLE_FREQ   integer
##                        SLE_LIGHT_EXP   integer
##                      UVE_TANNING_CUR   integer
##                    UVE_SKIN_REACTION   integer
##                       UVE_TIME_WKDAY   integer
##                       UVE_TIME_WKEND   integer
##                       UVE_PROTECTION   integer
##                             UVE_HAIR   integer
##                              UVE_EYE   integer
##                          NUT_VEG_QTY   integer
##                       NUT_FRUITS_QTY   integer
##                        NUT_JUICE_QTY   integer
##                             ALC_EVER   integer
##                         ALC_CUR_FREQ   integer
##                            ALC_WKEND   integer
##                  ALC_BINGE_FREQ_MALE   integer
##                ALC_BINGE_FREQ_FEMALE   integer
##                       SMK_CIG_STATUS   integer
##                         SMK_CIG_EVER   integer
##                   SMK_CIG_WHOLE_EVER   integer
##                  SMK_CIG_WHOLE_ONSET   integer
##                     SMK_CIG_CUR_FREQ   integer
##              SMK_CIG_DAILY_CUR_ONSET   integer
##                        SMK_PATCH_CUR   integer
##                          SMK_GUM_CUR   integer
##               PSE_CHILDHOOD_DURATION   integer
##              PSE_ADULT_HOME_DURATION   integer
##               PSE_ADULT_WRK_DURATION   integer
##                        PSE_HOME_FREQ   integer
##                     PSE_LEISURE_FREQ   integer
##                         PSE_WRK_FREQ   integer
##                          PA_VIG_FREQ   integer
##                          PA_VIG_TIME   integer
##                          PA_MOD_FREQ   integer
##                          PA_MOD_TIME   integer
##                         PA_WALK_FREQ   integer
##                         PA_WALK_TIME   integer
##                   PA_TOTAL_VIG_SHORT   integer
##                   PA_TOTAL_MOD_SHORT   integer
##                  PA_TOTAL_WALK_SHORT   numeric
##                       PA_TOTAL_SHORT   numeric
##                       PA_LEVEL_SHORT   integer
##                    PA_JOB_UNPAID_WRK   integer
##                    PA_TOTAL_VIG_LONG   integer
##                    PA_TOTAL_MOD_LONG   numeric
##                   PA_TOTAL_WALK_LONG   numeric
##                        PA_TOTAL_LONG   numeric
##                        PA_LEVEL_LONG   integer
##                    PA_SIT_TIME_WKDAY   integer
##                    PA_SIT_TIME_WKEND   integer
##                    PA_TOTAL_SIT_TIME   integer
##                  PA_SIT_AVG_TIME_DAY   numeric
##                    SDC_EB_ABORIGINAL   integer
##                          SDC_EB_ARAB   integer
##                         SDC_EB_BLACK   integer
##                       SDC_EB_E_ASIAN   integer
##                      SDC_EB_FILIPINO   integer
##                        SDC_EB_JEWISH   integer
##                         SDC_EB_LATIN   integer
##                       SDC_EB_S_ASIAN   integer
##                      SDC_EB_SE_ASIAN   integer
##                       SDC_EB_W_ASIAN   integer
##                         SDC_EB_WHITE   integer
##                         SDC_EB_OTHER   integer
##                    SDC_BIRTH_COUNTRY   integer
##                      SDC_ARRIVAL_AGE   integer
##                        WRK_FULL_TIME   integer
##                        WRK_PART_TIME   integer
##                       WRK_RETIREMENT   integer
##                      WRK_HOME_FAMILY   integer
##                           WRK_UNABLE   integer
##                       WRK_UNEMPLOYED   integer
##                           WRK_UNPAID   integer
##                          WRK_STUDENT   integer
##                       WRK_EMPLOYMENT   integer
##                 WRK_IND_TYPE_CUR_CAT   integer
##                 WRK_SCHEDULE_CUR_CAT   integer
##               PM_STAND_HEIGHT_SR_AVG   numeric
##                     PM_WEIGHT_SR_AVG   numeric
##                        PM_HIP_SR_AVG   numeric
##                      PM_WAIST_SR_AVG   numeric
##                PM_WAIST_HIP_RATIO_SR   numeric
##                            PM_BMI_SR   numeric
##                        DIS_ENDO_EVER   integer
##                DIS_ENDO_HB_CHOL_EVER   integer
##                 DIS_ENDO_HB_CHOL_AGE   integer
##                  DIS_ENDO_SUGAR_EVER   integer
##                   DIS_ENDO_SUGAR_AGE   integer
##                     DIS_ENDO_TD_EVER   integer
##                      DIS_ENDO_TD_AGE   integer
##                DIS_ENDO_TD_HYPO_EVER   integer
##               DIS_ENDO_TD_HYPER_EVER   integer
##              DIS_ENDO_TD_NODULE_EVER   integer
##         DIS_ENDO_TD_THYROIDITIS_EVER   integer
##         DIS_CARDIO_PREM_HD_MALE_EVER   integer
##       DIS_CARDIO_PREM_HD_FEMALE_EVER   integer
##                      DIS_CARDIO_EVER   integer
##                  DIS_CARDIO_DVT_EVER   integer
##                   DIS_CARDIO_DVT_AGE   integer
##                   DIS_CARDIO_PE_EVER   integer
##                    DIS_CARDIO_PE_AGE   integer
##               DIS_CARDIO_ANGINA_EVER   integer
##                DIS_CARDIO_ANGINA_AGE   integer
##               DIS_CARDIO_ANGINA_LAST   integer
##                  DIS_CARDIO_TIA_EVER   integer
##                   DIS_CARDIO_TIA_AGE   integer
##                   DIS_CARDIO_HF_EVER   integer
##                    DIS_CARDIO_HF_AGE   integer
##                   DIS_CARDIO_HD_EVER   integer
##                  DIS_CARDIO_VHD_EVER   integer
##                   DIS_CARDIO_VHD_AGE   integer
##           DIS_CARDIO_VHD_AORTIC_EVER   integer
##  DIS_CARDIO_VHD_MITRAL_STENOSIS_EVER   integer
##     DIS_CARDIO_VHD_MITRAL_VALVE_EVER   integer
##        DIS_CARDIO_VHD_RHEUMATIC_EVER   integer
##            DIS_CARDIO_VHD_OTHER_EVER   integer
##                  DIS_CARDIO_CHD_EVER   integer
##                   DIS_CARDIO_CHD_AGE   integer
##                 DIS_CARDIO_PERI_EVER   integer
##                  DIS_CARDIO_PERI_AGE   integer
##               DIS_CARDIO_ATRIAL_EVER   integer
##                DIS_CARDIO_ATRIAL_AGE   integer
##      DIS_CARDIO_ATRIAL_THINNERS_EVER   integer
##                 DIS_CARDIO_ARRH_EVER   integer
##                  DIS_CARDIO_ARRH_AGE   integer
##                DIS_CARDIO_OTHER_EVER   integer
##                 DIS_CARDIO_OTHER_AGE   integer
##                        DIS_RESP_EVER   integer
##               DIS_RESP_HAYFEVER_EVER   integer
##                DIS_RESP_HAYFEVER_AGE   integer
##            DIS_RESP_SLEEP_APNEA_EVER   integer
##             DIS_RESP_SLEEP_APNEA_AGE   integer
##                  DIS_RESP_OTHER_EVER   integer
##                   DIS_RESP_OTHER_AGE   integer
##                      DIS_GASTRO_EVER   integer
##               DIS_GASTRO_ULCERS_EVER   integer
##                DIS_GASTRO_ULCERS_AGE   integer
##                 DIS_GASTRO_GERD_EVER   integer
##                  DIS_GASTRO_GERD_AGE   integer
##             DIS_GASTRO_H_PYLORI_EVER   integer
##              DIS_GASTRO_H_PYLORI_AGE   integer
##             DIS_GASTRO_BARRETTS_EVER   integer
##              DIS_GASTRO_BARRETTS_AGE   integer
##          DIS_GASTRO_INDIGESTION_EVER   integer
##           DIS_GASTRO_INDIGESTION_AGE   integer
##         DIS_GASTRO_DIVERTICULAR_EVER   integer
##          DIS_GASTRO_DIVERTICULAR_AGE   integer
##                  DIS_GASTRO_EOE_EVER   integer
##                   DIS_GASTRO_EOE_AGE   integer
##               DIS_GASTRO_CELIAC_EVER   integer
##                DIS_GASTRO_CELIAC_AGE   integer
##                       DIS_LIVER_EVER   integer
##                 DIS_LIVER_FATTY_EVER   integer
##                  DIS_LIVER_FATTY_AGE   integer
##          DIS_LIVER_PANCREATITIS_EVER   integer
##           DIS_LIVER_PANCREATITIS_AGE   integer
##            DIS_LIVER_GALLSTONES_EVER   integer
##             DIS_LIVER_GALLSTONES_AGE   integer
##                          DIS_RD_EVER   integer
##                          DIS_MH_EVER   integer
##                  DIS_MH_BIPOLAR_EVER   integer
##                   DIS_MH_BIPOLAR_AGE   integer
##                  DIS_MH_ANXIETY_EVER   integer
##                   DIS_MH_ANXIETY_AGE   integer
##                   DIS_MH_EATING_EVER   integer
##                    DIS_MH_EATING_AGE   integer
##                 DIS_MH_ANOREXIA_EVER   integer
##                  DIS_MH_BULIMIA_EVER   integer
##                DIS_MH_BINGE_EAT_EVER   integer
##                     DIS_MH_PTSD_EVER   integer
##                      DIS_MH_PTSD_AGE   integer
##            DIS_MH_SCHIZOPHRENIA_EVER   integer
##             DIS_MH_SCHIZOPHRENIA_AGE   integer
##                      DIS_MH_OCD_EVER   integer
##                       DIS_MH_OCD_AGE   integer
##                DIS_MH_ADDICTION_EVER   integer
##                 DIS_MH_ADDICTION_AGE   integer
##                       DIS_NEURO_EVER   integer
##             DIS_NEURO_PARKINSON_EVER   integer
##              DIS_NEURO_PARKINSON_AGE   integer
##              DIS_NEURO_MIGRAINE_EVER   integer
##               DIS_NEURO_MIGRAINE_AGE   integer
##                DIS_NEURO_AUTISM_EVER   integer
##                 DIS_NEURO_AUTISM_AGE   integer
##              DIS_NEURO_EPILEPSY_EVER   integer
##               DIS_NEURO_EPILEPSY_AGE   integer
##                DIS_NEURO_SPINAL_EVER   integer
##                 DIS_NEURO_SPINAL_AGE   integer
##                        DIS_BONE_EVER   integer
##                   DIS_BONE_GOUT_EVER   integer
##                    DIS_BONE_GOUT_AGE   integer
##                    DIS_BONE_CBP_EVER   integer
##                     DIS_BONE_CBP_AGE   integer
##                    DIS_BONE_CNP_EVER   integer
##                     DIS_BONE_CNP_AGE   integer
##           DIS_BONE_FIBROMYALGIA_EVER   integer
##            DIS_BONE_FIBROMYALGIA_AGE   integer
##             DIS_BONE_OSTEOPENIA_EVER   integer
##              DIS_BONE_OSTEOPENIA_AGE   integer
##                       DIS_INFEC_EVER   integer
##            DIS_INFEC_MENINGITIS_EVER   integer
##             DIS_INFEC_MENINGITIS_AGE   integer
##                   DIS_INFEC_HIV_EVER   integer
##                    DIS_INFEC_HIV_AGE   integer
##               DIS_INFEC_MALARIA_EVER   integer
##                DIS_INFEC_MALARIA_AGE   integer
##                    DIS_INFEC_TB_EVER   integer
##                     DIS_INFEC_TB_AGE   integer
##             DIS_INFEC_CHLAMYDIA_EVER   integer
##              DIS_INFEC_CHLAMYDIA_AGE   integer
##                DIS_INFEC_HERPES_EVER   integer
##                 DIS_INFEC_HERPES_AGE   integer
##             DIS_INFEC_GONORRHEA_EVER   integer
##              DIS_INFEC_GONORRHEA_AGE   integer
##              DIS_INFEC_SYPHILIS_EVER   integer
##               DIS_INFEC_SYPHILIS_AGE   integer
##                   DIS_INFEC_HPV_EVER   integer
##                    DIS_INFEC_HPV_AGE   integer
##                   DIS_INFEC_STI_EVER   integer
##                    DIS_INFEC_STI_AGE   integer
##                         DIS_GYN_EVER   integer
##                    DIS_GYN_PCOS_EVER   integer
##                     DIS_GYN_PCOS_AGE   integer
##                DIS_GYN_FIBROIDS_EVER   integer
##                 DIS_GYN_FIBROIDS_AGE   integer
##           DIS_GYN_ENDOMETRIOSIS_EVER   integer
##            DIS_GYN_ENDOMETRIOSIS_AGE   integer
##                         DIS_GEN_EVER   integer
##                      DIS_GEN_DS_EVER   logical
##                     DIS_GEN_SCA_EVER   logical
##                      DIS_GEN_SCA_AGE   integer
##             DIS_GEN_THALASSEMIA_EVER   logical
##              DIS_GEN_THALASSEMIA_AGE   integer
##                     DIS_GEN_CAH_EVER   logical
##                     DIS_GEN_AIS_EVER   logical
##                      DIS_GEN_AIS_AGE   integer
##              DIS_GEN_HEMOPHILIA_EVER   logical
##               DIS_GEN_HEMOPHILIA_AGE   integer
##                      DIS_GEN_CF_EVER   logical
##                       DIS_GEN_CF_AGE   integer
##                      DIS_GEN_KS_EVER   logical
##                       DIS_GEN_KS_AGE   integer
##                      DIS_GEN_TS_EVER   logical
##                       DIS_GEN_TS_AGE   integer
##                         DIS_EYE_EVER   integer
##                 DIS_EYE_MACULAR_EVER   integer
##                  DIS_EYE_MACULAR_AGE   integer
##                DIS_EYE_GLAUCOMA_EVER   integer
##                 DIS_EYE_GLAUCOMA_AGE   integer
##               DIS_EYE_CATARACTS_EVER   integer
##                DIS_EYE_CATARACTS_AGE   integer
##                DIS_EYE_DIAB_RET_EVER   integer
##                 DIS_EYE_DIAB_RET_AGE   integer
##                         DIS_EAR_EVER   integer
##                DIS_EAR_TINNITUS_EVER   integer
##                 DIS_EAR_TINNITUS_AGE   integer
##                 DIS_EAR_TINNITUS_DUR   integer
##                DIS_EAR_TINNITUS_FREQ   integer
##              DIS_EAR_TINNITUS_NATURE   integer
##              DIS_EAR_TINNITUS_AFFECT   integer
##                    DIS_EAR_LOSS_EVER   integer
##                     DIS_EAR_LOSS_AGE   integer
##                             ALE06_06   numeric
##                             ALE06_07   integer
##                             ALE16_06   numeric
##                             ALE16_07   numeric
##                          MSD11_DAPOP   integer
##                             MSD11_PR character
##                            MSD11_REG character
##                           MSD11_ZONE character
##                            MSD11_CMA character
##                            MSD11_MFS   numeric
##                            MSD11_SFS   numeric
##                           GRLAN10_09   numeric
##                        NO2LUR06_A_01   numeric
##                       NO2LUR08_RA_01   numeric
##                           O3CHG15_01   numeric
##                         PM25DAL12_01   numeric
##                          SO2OMI12_01   numeric
##                          WTHNRC15_01   numeric
##                          WTHNRC15_02   numeric
##                          WTHNRC15_03   numeric
##                          WTHNRC15_04   numeric
##                          WTHNRC15_05   numeric
##                          WTHNRC15_07   numeric
##                          WTHNRC15_08   integer
##                          WTHNRC15_09   integer
##                          WTHNRC15_10   numeric
##                          WTHNRC15_11   numeric
##                          WTHNRC15_12   numeric
##                          WTHNRC15_13   integer
##                          WTHNRC15_14   integer
##                          WTHNRC15_15   numeric
##                          WTHNRC15_16   numeric
##                          WTHNRC15_17   integer
##                          WTHNRC15_18   integer
##                          WTHNRC15_19   numeric
##                          LGTNLT12_01   integer
```

In this health administrative dataset, there are 41,187 observations and 440 variables. Most of these variables are integers, numeric, or character, which makes sense. However, some variables are being treated as logical. Let’s identify those logical variables.


``` r
data %>% 
  select_if(is_logical) %>% 
  glimpse()
```

```
## Rows: 41,187
## Columns: 9
## $ DIS_GEN_DS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_SCA_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_THALASSEMIA_EVER <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_CAH_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_AIS_EVER         <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_HEMOPHILIA_EVER  <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_CF_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_KS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ DIS_GEN_TS_EVER          <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
```


We have 9 variables that are logical so let's drop those.



``` r
### Select specific columns
logical_cols <- c("DIS_GEN_DS_EVER", "DIS_GEN_SCA_EVER", "DIS_GEN_THALASSEMIA_EVER", "DIS_GEN_CAH_EVER", "DIS_GEN_AIS_EVER", "DIS_GEN_HEMOPHILIA_EVER", "DIS_GEN_CF_EVER", "DIS_GEN_KS_EVER", "DIS_GEN_TS_EVER")

data <- data %>% select(!(logical_cols))
```

```
## Warning: Using an external vector in selections was deprecated in tidyselect 1.1.0.
## ℹ Please use `all_of()` or `any_of()` instead.
##   # Was:
##   data %>% select(logical_cols)
## 
##   # Now:
##   data %>% select(all_of(logical_cols))
## 
## See <https://tidyselect.r-lib.org/reference/faq-external-vector.html>.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```
**Identify Missing Data**



``` r
missing_table <- miss_var_summary(data)
missing_table
```

```
## # A tibble: 431 × 3
##    variable                       n_miss pct_miss
##    <chr>                           <int>    <num>
##  1 DIS_CARDIO_PREM_HD_FEMALE_EVER  41081     99.7
##  2 DIS_CARDIO_PREM_HD_MALE_EVER    41061     99.7
##  3 DIS_MH_BIPOLAR_EVER             40914     99.3
##  4 DIS_EAR_TINNITUS_NATURE         40880     99.3
##  5 DIS_ENDO_TD_AGE                 40862     99.2
##  6 DIS_ENDO_SUGAR_AGE              40861     99.2
##  7 DIS_RESP_OTHER_EVER             40858     99.2
##  8 DIS_MH_EATING_EVER              40857     99.2
##  9 DIS_LIVER_FATTY_EVER            40856     99.2
## 10 DIS_EAR_TINNITUS_FREQ           40854     99.2
## # ℹ 421 more rows
```
Although the proportion of missing data can influence statistical inference, there are no universally accepted guidelines for the maximum amount of missing data for which multiple imputation (MI) remains beneficial. One study suggests that when over 10% of data are missing, the estimates may become biased [@bennett2001can]. Another paper proposes 5% as a threshold, below which MI is unlikely to provide significant benefits [@schafer1999multiple]. However, limited evidence exists to support these cutoff points. Few studies have explored how bias and efficiency change with increasing levels of missing data, with the most extreme case being 50% missing data, which showed growing inconsistency in effect estimates as missingness increased [@mishra2014comparative] for the small sample. However, when both high missing data and large sample sizes are considered as missing data being at random (MAR) [@lee2012recovery]. In this analysis, I consider missing values with less than 50 percent in this dataset.

let's review filter out all variables with more than 50% missing.



``` r
data <- data %>%
          select(where(~sum(is.na(.x))/length(.x) < 0.50))

missing_table <- miss_var_summary(data)
```

``` r
missing_table <- miss_var_summary(data)
missing_table
```

```
## # A tibble: 232 × 3
##    variable              n_miss pct_miss
##    <chr>                  <int>    <num>
##  1 PM_WAIST_HIP_RATIO_SR  17734     43.1
##  2 PM_HIP_SR_AVG          17349     42.1
##  3 WH_MENSTRUATION_AGE    17026     41.3
##  4 PM_WAIST_SR_AVG        16400     39.8
##  5 HS_PAP_EVER            16182     39.3
##  6 HS_MMG_EVER            15995     38.8
##  7 PM_BMI_SR              11976     29.1
##  8 PM_WEIGHT_SR_AVG       11707     28.4
##  9 PA_TOTAL_SIT_TIME      11272     27.4
## 10 PA_SIT_AVG_TIME_DAY    11257     27.3
## # ℹ 222 more rows
```

### Summarize findings using tables, charts, or heatmaps to visualize missingness. 


``` r
gg_miss_upset(data, order.by = "freq", nsets = 10)
```

![](Missing-Data_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

Suppose we want to make model where 
We have identified the outcome and predictors variable. Follwoing are the outcoma and predictor variables.

## Main Outcome of Interest: 

BMI: Body Mass Index (PM_BMI_SR).

## Expouser

PA: Physical Activities: PA_TOTAL_SHORT

SL: Sedentary lifestyle: Total sitting time per week:PA_TOTAL_SIT_TIME 

## Predictors:

### Social and demographic factor:

EB: Participant's ethnic background is Aboriginal (e.g. First Nations, Metis, Inuit).:SDC_EB_ABORIGINAL

AGE: Age of the respondent: SDC_AGE_CALC

GE: Gender: SDC_GENDER

ES: Employment Status: WRK_EMPLOYMENT

GPH: General perception of health: HS_GEN_HEALTH

FI: Food Intake: NUT_VEG_QTY, NUT_FRUITS_QTY

SM: Smoking status: SMK_CIG_STATUS

AC: Alcohol consumption: ALC_CUR_FREQ

### Phychological factor:

DE: Depression: DIS_DEP_EVER

### Choronic health condition 

DIA: Diabetes: DIS_DIAB_TYPE

RE: Region: ADM_STUDY_ID

``` r
data<- data %>%
  select(ID, PM_BMI_SR, PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME , SDC_EB_ABORIGINAL, SDC_AGE_CALC, SDC_GENDER, WRK_EMPLOYMENT, HS_GEN_HEALTH, NUT_VEG_QTY, NUT_FRUITS_QTY, SMK_CIG_STATUS, ALC_CUR_FREQ, DIS_DEP_EVER, DIS_DIAB_TYPE , ADM_STUDY_ID)
col<-c("SDC_EB_ABORIGINAL", "SDC_GENDER", "WRK_EMPLOYMENT", "WRK_EMPLOYMENT", "HS_GEN_HEALTH", "SMK_CIG_STATUS", "ALC_CUR_FREQ",
       "DIS_DEP_EVER", "DIS_DIAB_TYPE", "ADM_STUDY_ID")
data <- data %>% 
  dplyr:: mutate_at(col, factor)
```

2. **Apply Imputation Methods**
   - Select and apply at least three different methods for imputing missing data, such as:
     - Mean/Median/Mode imputation.
We have used mean for continuous variable and median for categorical variables. 

``` r
set.seed(123)
data_mean <- data
summary(data_mean)
```

```
##       ID              PM_BMI_SR     PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME
##  Length:41187       Min.   : 8.86   Min.   :    0   Min.   :   0     
##  Class :character   1st Qu.:23.38   1st Qu.:  600   1st Qu.:1740     
##  Mode  :character   Median :26.58   Median : 1782   Median :2520     
##                     Mean   :27.55   Mean   : 2574   Mean   :2661     
##                     3rd Qu.:30.55   3rd Qu.: 3732   3rd Qu.:3390     
##                     Max.   :69.40   Max.   :19278   Max.   :6720     
##                     NA's   :11976   NA's   :6763    NA's   :11272    
##  SDC_EB_ABORIGINAL  SDC_AGE_CALC   SDC_GENDER WRK_EMPLOYMENT HS_GEN_HEALTH
##  0   :36601        Min.   :30.00   1:15200    0   :11770     1   :  808   
##  1   : 1431        1st Qu.:43.00   2:25987    1   :27490     2   : 3290   
##  NA's: 3155        Median :52.00              NA's: 1927     3   :12572   
##                    Mean   :51.48                             4   :16938   
##                    3rd Qu.:60.00                             5   : 6907   
##                    Max.   :74.00                             NA's:  672   
##                                                                           
##   NUT_VEG_QTY     NUT_FRUITS_QTY   SMK_CIG_STATUS  ALC_CUR_FREQ   DIS_DEP_EVER
##  Min.   : 0.000   Min.   : 0.000   0   :21248     1      : 7195   0   :31530  
##  1st Qu.: 2.000   1st Qu.: 1.000   1   :13102     5      : 7174   1   : 4539  
##  Median : 2.000   Median : 2.000   2   :  990     3      : 4877   2   :  413  
##  Mean   : 2.672   Mean   : 2.132   3   : 3430     4      : 4308   NA's: 4705  
##  3rd Qu.: 3.000   3rd Qu.: 3.000   NA's: 2417     6      : 4102               
##  Max.   :35.000   Max.   :25.000                  (Other):11848               
##  NA's   :2549     NA's   :2426                    NA's   : 1683               
##  DIS_DIAB_TYPE ADM_STUDY_ID
##  -7  :36807    1: 4450     
##  1   :  315    2: 6000     
##  2   : 2160    3:25437     
##  3   :  425    5: 5300     
##  NA's: 1480                
##                            
## 
```

``` r
for(var in names(data_mean)){
  if (anyNA(data_mean[[var]])) {
    # print(var)
    # use median for catagorical variables
    if (class(data_mean[[var]])=="factor") {
      # new_var <- paste0(var, "_imput")
      # data_mean[[new_var]] <- data_mean[[var]]
      data_mean <- impute_median_at(data_mean, .vars = vars(all_of(var)))
      # print(var)
    }
    #Have use mean for interger or continuous variable
    else{
      # new_var <- paste0(var, "_imput")
      # data_mean[[new_var]] <- data_mean[[var]]
      data_mean <- impute_mean_at(data_mean, .vars = vars(all_of(var)))
    }
    # print(data_shadow[[var]])
  }

}
```
  - K-Nearest Neighbors (KNN) imputation.

KNN imputation replaces missing values based on the values of the nearest neighbors.

Implementation:

``` r
set.seed(456)
imputed_data_KNN <- kNN(data, k = 3)  # k = number of nearest neighbors
```

- Multiple Imputation by Chained Equations (MICE).

MICE is a robust method for handling missing data by creating multiple imputed datasets and combining the results. Here we consider 5 imputation (according to theory this sould be more thanb 20 ) and 5 number of iteration


``` r
imputed_data_mice <- mice(data, m = 5, seed = 567, maxit=5)
```

```
## 
##  iter imp variable
##   1   1  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   1   2  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   1   3  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   1   4  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   1   5  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   2   1  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   2   2  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   2   3  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   2   4  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   2   5  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   3   1  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   3   2  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   3   3  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   3   4  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   3   5  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   4   1  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   4   2  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   4   3  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   4   4  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   4   5  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   5   1  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   5   2  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   5   3  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   5   4  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
##   5   5  PM_BMI_SR  PA_TOTAL_SHORT  PA_TOTAL_SIT_TIME  SDC_EB_ABORIGINAL  WRK_EMPLOYMENT  HS_GEN_HEALTH  NUT_VEG_QTY  NUT_FRUITS_QTY  SMK_CIG_STATUS  ALC_CUR_FREQ  DIS_DEP_EVER  DIS_DIAB_TYPE
```

```
## Warning: Number of logged events: 1
```

``` r
imputed_data_mice_c<-complete(imputed_data_mice)
```
   - Document the implementation process for each method.

3. **Evaluation of Imputation Methods**
   - Compare the imputed datasets by analyzing:
     - Changes in key summary statistics (e.g., means, variances).
     PM_BMI_SR, PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME , SDC_EB_ABORIGINAL, SDC_AGE_CALC, SDC_GENDER, WRK_EMPLOYMENT, HS_GEN_HEALTH, NUT_VEG_QTY, NUT_FRUITS_QTY, SMK_CIG_STATUS, ALC_CUR_FREQ, DIS_DEP_EVER, DIS_DIAB_TYPE , ADM_STUDY_ID

``` r
# Function to calculate mean and standard deviation
calculate_stats <- function(data) {
  numeric_stats<-data %>%
    summarise(across(where(is.numeric), list(mean = ~ mean(., na.rm = TRUE), sd = ~ sd(., na.rm = TRUE))))
  freq_tables <- data %>%
    select(where(is.factor)) %>%
    map(~ table(.x) %>% as.data.frame() %>% rename(Value = .x, Frequency = Freq))
  list(
    numeric_stats = numeric_stats,
    freq_tables = freq_tables
  )
}

# Calculate statistics for each dataset

data_selct <- data %>%
  select(-c(SDC_GENDER, SDC_AGE_CALC, ADM_STUDY_ID))
original_stats<-calculate_stats(data)
data_selct <- data_mean %>%
  select(-c(SDC_GENDER, SDC_AGE_CALC, ADM_STUDY_ID))
mean_imputed_stats <- calculate_stats(data_selct)
data_selct <- imputed_data_KNN %>%
  select(-c(SDC_GENDER, SDC_AGE_CALC, ADM_STUDY_ID))
KNN_imputed_stats <- calculate_stats(data_selct)
data_selct <- imputed_data_mice_c %>%
  select(-c(SDC_GENDER, SDC_AGE_CALC, ADM_STUDY_ID))
mice_imputed_stats <- calculate_stats(imputed_data_mice_c)

original_stats_num<-data.frame(original_stats$numeric_stats)
mean_imputed_stats_num<-data.frame(mean_imputed_stats$numeric_stats)
KNN_imputed_stats_num<-data.frame(KNN_imputed_stats$numeric_stats)
mice_imputed_stats_num<-data.frame(mice_imputed_stats$numeric_stats)

original_fre <- original_stats$freq_tables %>%
  bind_rows(.id = "Variable")
wide_original_fre <- original_fre %>%
  pivot_wider(names_from = Variable, values_from = Frequency, values_fill = list(Frequency = 0))

mean_fre <- mean_imputed_stats$freq_tables %>%
  bind_rows(.id = "Variable")
wide_mean_fre <- mean_fre %>%
  pivot_wider(names_from = Variable, values_from = Frequency, values_fill = list(Frequency = 0))
KNN_fre <- KNN_imputed_stats$freq_tables %>%
  bind_rows(.id = "Variable")
wide_KNN_fre <- KNN_fre %>%
  pivot_wider(names_from = Variable, values_from = Frequency, values_fill = list(Frequency = 0))

mice_fre <- mice_imputed_stats$freq_tables %>%
  bind_rows(.id = "Variable")
wide_mice_fre <- mice_fre %>%
  pivot_wider(names_from = Variable, values_from = Frequency, values_fill = list(Frequency = 0))


# Combine results into a single table for comparison
comparable_fre <- bind_rows(
  wide_original_fre %>% mutate(Dataset = "Original"),
  wide_mean_fre %>% mutate(Dataset = "Median Imputed"),
  wide_KNN_fre %>% mutate(Dataset = "KNN Imputed"),
  wide_mice_fre %>% mutate(Dataset = "mice Imputed")
)

comparison_table<- bind_rows(
  original_stats_num %>% mutate(Dataset = "Original"),
  mean_imputed_stats_num %>% mutate(Dataset = "Mean Imputed"),
  KNN_imputed_stats_num %>% mutate(Dataset = "KNN Imputed"),
  mice_imputed_stats_num %>% mutate(Dataset = "mice Imputed")
)

comparable_fre %>%
  select(Value, SDC_EB_ABORIGINAL, Dataset) %>%
  filter(SDC_EB_ABORIGINAL!=0)
```

```
## # A tibble: 8 × 3
##   Value SDC_EB_ABORIGINAL Dataset       
##   <fct>             <int> <chr>         
## 1 0                 36601 Original      
## 2 1                  1431 Original      
## 3 0                 39756 Median Imputed
## 4 1                  1431 Median Imputed
## 5 0                 39595 KNN Imputed   
## 6 1                  1592 KNN Imputed   
## 7 0                 39605 mice Imputed  
## 8 1                  1582 mice Imputed
```

``` r
# Display the comparison table
print(comparison_table)
```

```
##   PM_BMI_SR_mean PM_BMI_SR_sd PA_TOTAL_SHORT_mean PA_TOTAL_SHORT_sd
## 1       27.54980     6.155106            2574.089          2656.189
## 2       27.54980     5.183541            2574.089          2428.335
## 3       27.51440     5.806502            2479.315          2550.077
## 4       27.64476     6.202088            2588.118          2671.081
##   PA_TOTAL_SIT_TIME_mean PA_TOTAL_SIT_TIME_sd SDC_AGE_CALC_mean SDC_AGE_CALC_sd
## 1               2660.601             1204.772          51.48005        10.80263
## 2               2660.601             1026.756                NA              NA
## 3               2664.911             1129.135                NA              NA
## 4               2682.866             1213.641          51.48005        10.80263
##   NUT_VEG_QTY_mean NUT_VEG_QTY_sd NUT_FRUITS_QTY_mean NUT_FRUITS_QTY_sd
## 1         2.671929       1.677674            2.131653          1.414370
## 2         2.671929       1.624930            2.131653          1.372082
## 3         2.645908       1.644643            2.103649          1.400936
## 4         2.660208       1.676790            2.124311          1.416851
##        Dataset
## 1     Original
## 2 Mean Imputed
## 3  KNN Imputed
## 4 mice Imputed
```
     
     - The preservation of relationships between variables (e.g., correlations).

``` r
# Select only numeric variables
# data_com
original_cor <- data %>%
  select(PM_BMI_SR,  PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME) %>%
  na.omit() %>%
  cor() 

mean_cor <- data_mean %>%
  select(PM_BMI_SR,  PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME) %>%
  cor() 
KNN_cor <- imputed_data_KNN %>%
  select(PM_BMI_SR,  PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME) %>%
  cor() 
mice_cor <- imputed_data_mice_c %>%
  select(PM_BMI_SR,  PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME) %>%
  cor() 
# Compute the correlation matrix
print ("Correlation matrix for orginal dataset")
```

```
## [1] "Correlation matrix for orginal dataset"
```

``` r
print (original_cor)
```

```
##                     PM_BMI_SR PA_TOTAL_SHORT PA_TOTAL_SIT_TIME
## PM_BMI_SR          1.00000000    -0.06926963          0.059150
## PA_TOTAL_SHORT    -0.06926963     1.00000000         -0.278986
## PA_TOTAL_SIT_TIME  0.05915000    -0.27898597          1.000000
```

``` r
print ("Correlation matrix for mean imputation")
```

```
## [1] "Correlation matrix for mean imputation"
```

``` r
print(mean_cor)
```

```
##                     PM_BMI_SR PA_TOTAL_SHORT PA_TOTAL_SIT_TIME
## PM_BMI_SR          1.00000000    -0.05562002        0.04329926
## PA_TOTAL_SHORT    -0.05562002     1.00000000       -0.23071719
## PA_TOTAL_SIT_TIME  0.04329926    -0.23071719        1.00000000
```

``` r
print ("Correlation matrix for KNN imputation")
```

```
## [1] "Correlation matrix for KNN imputation"
```

``` r
print(KNN_cor)
```

```
##                     PM_BMI_SR PA_TOTAL_SHORT PA_TOTAL_SIT_TIME
## PM_BMI_SR          1.00000000    -0.06312364        0.04378642
## PA_TOTAL_SHORT    -0.06312364     1.00000000       -0.24580010
## PA_TOTAL_SIT_TIME  0.04378642    -0.24580010        1.00000000
```

``` r
print ("Correlation matrix for MICE imputation" )
```

```
## [1] "Correlation matrix for MICE imputation"
```

``` r
print(mice_cor)
```

```
##                     PM_BMI_SR PA_TOTAL_SHORT PA_TOTAL_SIT_TIME
## PM_BMI_SR          1.00000000    -0.06696019         0.0501639
## PA_TOTAL_SHORT    -0.06696019     1.00000000        -0.2802741
## PA_TOTAL_SIT_TIME  0.05016390    -0.28027413         1.0000000
```
Cross tabulation for catagorical variables 


``` r
library(gmodels)
var_names<-data %>%
  select(where(is.factor)) %>%
  names()
# variable_pairs <- combn(var_names, 2, simplify = FALSE)
# 
# # Create an empty list to store cross-tabulations
# cross_tabs <- list()
# 
# # Loop through each pair and generate cross-tabulations
# for (pair in variable_pairs) {
#   var1 <- pair[1]
#   var2 <- pair[2]
#   cross_tab <- table(data_shadow[[var1]], data_shadow[[var2]])
#   cross_tabs[[paste(var1, "vs", var2)]] <- cross_tab
# }
# 
# # Display all cross-tabulations
# print(cross_tabs)


for (i in 1:(length(var_names)-1)) {
  for (j in (i+1):length(var_names)) {
    cat("\nCross-tabulation between", var_names[i], "and", var_names[j], "\n", "For Orginal data")
    CrossTable(data[[var_names[i]]], data[[var_names[j]]], prop.chisq  = FALSE, prop.r = TRUE, prop.c = FALSE, prop.t = FALSE, chisq = TRUE)
    cat("\nCross-tabulation between", var_names[i], "and", var_names[j], "\n", "For Median Imputation")
    CrossTable(data_mean[[var_names[i]]], data_mean[[var_names[j]]], prop.chisq  = FALSE, prop.r = TRUE, prop.c = FALSE, prop.t = FALSE, chisq = TRUE)
    cat("\nCross-tabulation between", var_names[i], "and", var_names[j], "\n", "For KNN Imputation")
    CrossTable(imputed_data_KNN[[var_names[i]]], imputed_data_KNN[[var_names[j]]], prop.chisq  = FALSE, prop.r = TRUE, prop.c = FALSE, prop.t = FALSE, chisq = TRUE)
    cat("\nCross-tabulation between", var_names[i], "and", var_names[j], "\n", "For MICE Imputation")
    CrossTable(imputed_data_mice_c[[var_names[i]]], imputed_data_mice_c[[var_names[j]]], prop.chisq  = FALSE, prop.r = TRUE, prop.c = FALSE, prop.t = FALSE, chisq = TRUE)
  }
}
```

```
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SDC_GENDER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38032 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|
##                    0 |     13934 |     22667 |     36601 | 
##                      |     0.381 |     0.619 |     0.962 | 
## ---------------------|-----------|-----------|-----------|
##                    1 |       395 |      1036 |      1431 | 
##                      |     0.276 |     0.724 |     0.038 | 
## ---------------------|-----------|-----------|-----------|
##         Column Total |     14329 |     23703 |     38032 | 
## ---------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  64.25407     d.f. =  1     p =  1.093658e-15 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  63.80909     d.f. =  1     p =  1.3708e-15 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SDC_GENDER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|
##                         0 |     14805 |     24951 |     39756 | 
##                           |     0.372 |     0.628 |     0.965 | 
## --------------------------|-----------|-----------|-----------|
##                         1 |       395 |      1036 |      1431 | 
##                           |     0.276 |     0.724 |     0.035 | 
## --------------------------|-----------|-----------|-----------|
##              Column Total |     15200 |     25987 |     41187 | 
## --------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  55.08702     d.f. =  1     p =  1.153101e-13 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  54.67394     d.f. =  1     p =  1.422803e-13 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SDC_GENDER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|
##                                0 |     14665 |     24930 |     39595 | 
##                                  |     0.370 |     0.630 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|
##                                1 |       535 |      1057 |      1592 | 
##                                  |     0.336 |     0.664 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|
##                     Column Total |     15200 |     25987 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  7.741633     d.f. =  1     p =  0.005396197 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  7.594946     d.f. =  1     p =  0.005853215 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SDC_GENDER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|
##                                   0 |     14782 |     24823 |     39605 | 
##                                     |     0.373 |     0.627 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|
##                                   1 |       418 |      1164 |      1582 | 
##                                     |     0.264 |     0.736 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|
##                        Column Total |     15200 |     25987 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  77.63813     d.f. =  1     p =  1.237575e-18 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  77.17067     d.f. =  1     p =  1.568046e-18 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and WRK_EMPLOYMENT 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  37504 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 | Row Total | 
## ---------------------|-----------|-----------|-----------|
##                    0 |     10786 |     25314 |     36100 | 
##                      |     0.299 |     0.701 |     0.963 | 
## ---------------------|-----------|-----------|-----------|
##                    1 |       430 |       974 |      1404 | 
##                      |     0.306 |     0.694 |     0.037 | 
## ---------------------|-----------|-----------|-----------|
##         Column Total |     11216 |     26288 |     37504 | 
## ---------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  0.3613521     d.f. =  1     p =  0.5477563 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.3265199     d.f. =  1     p =  0.5677155 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and WRK_EMPLOYMENT 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 | Row Total | 
## --------------------------|-----------|-----------|-----------|
##                         0 |     11340 |     28416 |     39756 | 
##                           |     0.285 |     0.715 |     0.965 | 
## --------------------------|-----------|-----------|-----------|
##                         1 |       430 |      1001 |      1431 | 
##                           |     0.300 |     0.700 |     0.035 | 
## --------------------------|-----------|-----------|-----------|
##              Column Total |     11770 |     29417 |     41187 | 
## --------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1.5737     d.f. =  1     p =  0.2096705 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  1.499875     d.f. =  1     p =  0.2206907 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and WRK_EMPLOYMENT 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|
##                                0 |     11935 |     27660 |     39595 | 
##                                  |     0.301 |     0.699 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|
##                                1 |       471 |      1121 |      1592 | 
##                                  |     0.296 |     0.704 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|
##                     Column Total |     12406 |     28781 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  0.225805     d.f. =  1     p =  0.6346519 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.2001054     d.f. =  1     p =  0.6546358 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and WRK_EMPLOYMENT 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|
##                                   0 |     11892 |     27713 |     39605 | 
##                                     |     0.300 |     0.700 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|
##                                   1 |       491 |      1091 |      1582 | 
##                                     |     0.310 |     0.690 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|
##                        Column Total |     12383 |     28804 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  0.7382616     d.f. =  1     p =  0.3902183 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.6910005     d.f. =  1     p =  0.4058243 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and HS_GEN_HEALTH 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  37776 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    0 |       710 |      2902 |     11148 |     15334 |      6269 |     36363 | 
##                      |     0.020 |     0.080 |     0.307 |     0.422 |     0.172 |     0.963 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |        43 |       139 |       481 |       532 |       218 |      1413 | 
##                      |     0.030 |     0.098 |     0.340 |     0.377 |     0.154 |     0.037 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |       753 |      3041 |     11629 |     15866 |      6487 |     37776 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  28.21172     d.f. =  4     p =  1.129924e-05 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and HS_GEN_HEALTH 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         0 |       765 |      3151 |     12091 |     17060 |      6689 |     39756 | 
##                           |     0.019 |     0.079 |     0.304 |     0.429 |     0.168 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |        43 |       139 |       481 |       550 |       218 |      1431 | 
##                           |     0.030 |     0.097 |     0.336 |     0.384 |     0.152 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |       808 |      3290 |     12572 |     17610 |      6907 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  26.94236     d.f. =  4     p =  2.041952e-05 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and HS_GEN_HEALTH 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                0 |       770 |      3214 |     12320 |     16540 |      6751 |     39595 | 
##                                  |     0.019 |     0.081 |     0.311 |     0.418 |     0.171 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |        53 |       162 |       601 |       544 |       232 |      1592 | 
##                                  |     0.033 |     0.102 |     0.378 |     0.342 |     0.146 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |       823 |      3376 |     12921 |     17084 |      6983 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  70.94192     d.f. =  4     p =  1.435834e-14 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and HS_GEN_HEALTH 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |       776 |      3222 |     12256 |     16576 |      6775 |     39605 | 
##                                     |     0.020 |     0.081 |     0.309 |     0.419 |     0.171 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |        49 |       162 |       543 |       598 |       230 |      1582 | 
##                                     |     0.031 |     0.102 |     0.343 |     0.378 |     0.145 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |       825 |      3384 |     12799 |     17174 |      7005 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  35.51534     d.f. =  4     p =  3.640165e-07 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SMK_CIG_STATUS 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  36799 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |     19605 |     11936 |       912 |      3007 |     35460 | 
##                      |     0.553 |     0.337 |     0.026 |     0.085 |     0.964 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       644 |       460 |        25 |       210 |      1339 | 
##                      |     0.481 |     0.344 |     0.019 |     0.157 |     0.036 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     20249 |     12396 |       937 |      3217 |     36799 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  91.4149     d.f. =  3     p =  1.088006e-19 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SMK_CIG_STATUS 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |     22929 |     12642 |       965 |      3220 |     39756 | 
##                           |     0.577 |     0.318 |     0.024 |     0.081 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       736 |       460 |        25 |       210 |      1431 | 
##                           |     0.514 |     0.321 |     0.017 |     0.147 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     23665 |     13102 |       990 |      3430 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  83.79482     d.f. =  3     p =  4.707901e-18 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SMK_CIG_STATUS 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |     22013 |     13254 |       995 |      3333 |     39595 | 
##                                  |     0.556 |     0.335 |     0.025 |     0.084 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       786 |       547 |        25 |       234 |      1592 | 
##                                  |     0.494 |     0.344 |     0.016 |     0.147 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     22799 |     13801 |      1020 |      3567 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  86.26924     d.f. =  3     p =  1.385768e-18 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and SMK_CIG_STATUS 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |     21819 |     13341 |      1039 |      3406 |     39605 | 
##                                     |     0.551 |     0.337 |     0.026 |     0.086 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       744 |       551 |        26 |       261 |      1582 | 
##                                     |     0.470 |     0.348 |     0.016 |     0.165 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     22563 |     13892 |      1065 |      3667 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  130.8762     d.f. =  3     p =  3.501459e-28 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ALC_CUR_FREQ 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  37530 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      2063 |      2359 |      6505 |      2782 |      4455 |      3994 |      6611 |      3765 |      3598 |     36132 | 
##                      |     0.057 |     0.065 |     0.180 |     0.077 |     0.123 |     0.111 |     0.183 |     0.104 |     0.100 |     0.963 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       102 |        92 |       278 |       108 |       186 |       133 |       225 |       135 |       139 |      1398 | 
##                      |     0.073 |     0.066 |     0.199 |     0.077 |     0.133 |     0.095 |     0.161 |     0.097 |     0.099 |     0.037 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      2165 |      2451 |      6783 |      2890 |      4641 |      4127 |      6836 |      3900 |      3737 |     37530 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  16.79515     d.f. =  8     p =  0.03231427 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ALC_CUR_FREQ 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      2215 |      2499 |      8567 |      2930 |      4691 |      4175 |      6949 |      3967 |      3763 |     39756 | 
##                           |     0.056 |     0.063 |     0.215 |     0.074 |     0.118 |     0.105 |     0.175 |     0.100 |     0.095 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       102 |        92 |       311 |       108 |       186 |       133 |       225 |       135 |       139 |      1431 | 
##                           |     0.071 |     0.064 |     0.217 |     0.075 |     0.130 |     0.093 |     0.157 |     0.094 |     0.097 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      2317 |      2591 |      8878 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  12.61957     d.f. =  8     p =  0.1256266 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ALC_CUR_FREQ 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      2384 |      2600 |      7207 |      3057 |      4879 |      4274 |      7173 |      4116 |      3905 |     39595 | 
##                                  |     0.060 |     0.066 |     0.182 |     0.077 |     0.123 |     0.108 |     0.181 |     0.104 |     0.099 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       174 |       114 |       291 |       118 |       196 |       141 |       251 |       155 |       152 |      1592 | 
##                                  |     0.109 |     0.072 |     0.183 |     0.074 |     0.123 |     0.089 |     0.158 |     0.097 |     0.095 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      2558 |      2714 |      7498 |      3175 |      5075 |      4415 |      7424 |      4271 |      4057 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  71.23289     d.f. =  8     p =  2.79151e-12 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ALC_CUR_FREQ 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      2322 |      2597 |      7238 |      3070 |      4868 |      4327 |      7173 |      4116 |      3894 |     39605 | 
##                                     |     0.059 |     0.066 |     0.183 |     0.078 |     0.123 |     0.109 |     0.181 |     0.104 |     0.098 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       123 |       107 |       307 |       123 |       210 |       153 |       257 |       152 |       150 |      1582 | 
##                                     |     0.078 |     0.068 |     0.194 |     0.078 |     0.133 |     0.097 |     0.162 |     0.096 |     0.095 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      2445 |      2704 |      7545 |      3193 |      5078 |      4480 |      7430 |      4268 |      4044 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  17.95163     d.f. =  8     p =  0.02159206 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  34641 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    0 |     28973 |      4001 |       359 |     33333 | 
##                      |     0.869 |     0.120 |     0.011 |     0.962 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |      1051 |       234 |        23 |      1308 | 
##                      |     0.804 |     0.179 |     0.018 |     0.038 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     30024 |      4235 |       382 |     34641 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  47.24088     d.f. =  2     p =  5.517906e-11 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         0 |     35061 |      4305 |       390 |     39756 | 
##                           |     0.882 |     0.108 |     0.010 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |      1174 |       234 |        23 |      1431 | 
##                           |     0.820 |     0.164 |     0.016 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  49.58261     d.f. =  2     p =  1.711094e-11 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                0 |     34512 |      4605 |       478 |     39595 | 
##                                  |     0.872 |     0.116 |     0.012 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |      1260 |       300 |        32 |      1592 | 
##                                  |     0.791 |     0.188 |     0.020 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  86.1708     d.f. =  2     p =  1.941992e-19 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   0 |     34252 |      4929 |       424 |     39605 | 
##                                     |     0.865 |     0.124 |     0.011 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |      1264 |       292 |        26 |      1582 | 
##                                     |     0.799 |     0.185 |     0.016 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  55.59894     d.f. =  2     p =  8.449733e-13 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  36959 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |     33084 |       270 |      1891 |       356 |     35601 | 
##                      |     0.929 |     0.008 |     0.053 |     0.010 |     0.963 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      1234 |         7 |        81 |        36 |      1358 | 
##                      |     0.909 |     0.005 |     0.060 |     0.027 |     0.037 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     34318 |       277 |      1972 |       392 |     36959 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  36.29123     d.f. =  3     p =  6.498425e-08 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |     36980 |       308 |      2079 |       389 |     39756 | 
##                           |     0.930 |     0.008 |     0.052 |     0.010 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      1307 |         7 |        81 |        36 |      1431 | 
##                           |     0.913 |     0.005 |     0.057 |     0.025 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  34.01598     d.f. =  3     p =  1.965855e-07 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |     36773 |       305 |      2124 |       393 |     39595 | 
##                                  |     0.929 |     0.008 |     0.054 |     0.010 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      1450 |        12 |        93 |        37 |      1592 | 
##                                  |     0.911 |     0.008 |     0.058 |     0.023 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  27.17551     d.f. =  3     p =  5.409066e-06 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |     36733 |       316 |      2157 |       399 |     39605 | 
##                                     |     0.927 |     0.008 |     0.054 |     0.010 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      1422 |        10 |       108 |        42 |      1582 | 
##                                     |     0.899 |     0.006 |     0.068 |     0.027 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  45.70434     d.f. =  3     p =  6.554735e-10 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38032 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      4230 |      4948 |     22816 |      4607 |     36601 | 
##                      |     0.116 |     0.135 |     0.623 |     0.126 |     0.962 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       105 |       363 |       788 |       175 |      1431 | 
##                      |     0.073 |     0.254 |     0.551 |     0.122 |     0.038 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4335 |      5311 |     23604 |      4782 |     38032 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  171.8199     d.f. =  3     p =  5.149522e-37 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      4345 |      5637 |     24649 |      5125 |     39756 | 
##                           |     0.109 |     0.142 |     0.620 |     0.129 |     0.965 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       105 |       363 |       788 |       175 |      1431 | 
##                           |     0.073 |     0.254 |     0.551 |     0.122 |     0.035 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  146.3991     d.f. =  3     p =  1.575781e-31 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      4345 |      5634 |     24497 |      5119 |     39595 | 
##                                  |     0.110 |     0.142 |     0.619 |     0.129 |     0.961 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       105 |       366 |       940 |       181 |      1592 | 
##                                  |     0.066 |     0.230 |     0.590 |     0.114 |     0.039 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  112.6544     d.f. =  3     p =  2.944582e-24 
## 
## 
##  
## 
## Cross-tabulation between SDC_EB_ABORIGINAL and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      4342 |      5588 |     24579 |      5096 |     39605 | 
##                                     |     0.110 |     0.141 |     0.621 |     0.129 |     0.962 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       108 |       412 |       858 |       204 |      1582 | 
##                                     |     0.068 |     0.260 |     0.542 |     0.129 |     0.038 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  187.8888     d.f. =  3     p =  1.744434e-40 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and WRK_EMPLOYMENT 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39260 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 | Row Total | 
## ---------------------|-----------|-----------|-----------|
##                    1 |      4388 |     10083 |     14471 | 
##                      |     0.303 |     0.697 |     0.369 | 
## ---------------------|-----------|-----------|-----------|
##                    2 |      7382 |     17407 |     24789 | 
##                      |     0.298 |     0.702 |     0.631 | 
## ---------------------|-----------|-----------|-----------|
##         Column Total |     11770 |     27490 |     39260 | 
## ---------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1.285165     d.f. =  1     p =  0.2569409 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  1.25941     d.f. =  1     p =  0.2617628 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and WRK_EMPLOYMENT 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 | Row Total | 
## --------------------------|-----------|-----------|-----------|
##                         1 |      4388 |     10812 |     15200 | 
##                           |     0.289 |     0.711 |     0.369 | 
## --------------------------|-----------|-----------|-----------|
##                         2 |      7382 |     18605 |     25987 | 
##                           |     0.284 |     0.716 |     0.631 | 
## --------------------------|-----------|-----------|-----------|
##              Column Total |     11770 |     29417 |     41187 | 
## --------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1.002536     d.f. =  1     p =  0.3166976 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.9800328     d.f. =  1     p =  0.3221907 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and WRK_EMPLOYMENT 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|
##                                1 |      4601 |     10599 |     15200 | 
##                                  |     0.303 |     0.697 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|
##                                2 |      7805 |     18182 |     25987 | 
##                                  |     0.300 |     0.700 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|
##                     Column Total |     12406 |     28781 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  0.2526756     d.f. =  1     p =  0.6151974 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.2416114     d.f. =  1     p =  0.6230447 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and WRK_EMPLOYMENT 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|
##                                   1 |      4612 |     10588 |     15200 | 
##                                     |     0.303 |     0.697 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|
##                                   2 |      7771 |     18216 |     25987 | 
##                                     |     0.299 |     0.701 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|
##                        Column Total |     12383 |     28804 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  0.8778103     d.f. =  1     p =  0.3488021 
## 
## Pearson's Chi-squared test with Yates' continuity correction 
## ------------------------------------------------------------
## Chi^2 =  0.8570701     d.f. =  1     p =  0.3545599 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and HS_GEN_HEALTH 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  40515 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       301 |      1206 |      4786 |      6162 |      2472 |     14927 | 
##                      |     0.020 |     0.081 |     0.321 |     0.413 |     0.166 |     0.368 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       507 |      2084 |      7786 |     10776 |      4435 |     25588 | 
##                      |     0.020 |     0.081 |     0.304 |     0.421 |     0.173 |     0.632 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |       808 |      3290 |     12572 |     16938 |      6907 |     40515 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  13.07961     d.f. =  4     p =  0.01089331 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and HS_GEN_HEALTH 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       301 |      1206 |      4786 |      6435 |      2472 |     15200 | 
##                           |     0.020 |     0.079 |     0.315 |     0.423 |     0.163 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       507 |      2084 |      7786 |     11175 |      4435 |     25987 | 
##                           |     0.020 |     0.080 |     0.300 |     0.430 |     0.171 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |       808 |      3290 |     12572 |     17610 |      6907 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  12.12811     d.f. =  4     p =  0.01642358 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and HS_GEN_HEALTH 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       310 |      1231 |      4920 |      6237 |      2502 |     15200 | 
##                                  |     0.020 |     0.081 |     0.324 |     0.410 |     0.165 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       513 |      2145 |      8001 |     10847 |      4481 |     25987 | 
##                                  |     0.020 |     0.083 |     0.308 |     0.417 |     0.172 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |       823 |      3376 |     12921 |     17084 |      6983 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  12.74105     d.f. =  4     p =  0.01261291 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and HS_GEN_HEALTH 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       307 |      1246 |      4873 |      6267 |      2507 |     15200 | 
##                                     |     0.020 |     0.082 |     0.321 |     0.412 |     0.165 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       518 |      2138 |      7926 |     10907 |      4498 |     25987 | 
##                                     |     0.020 |     0.082 |     0.305 |     0.420 |     0.173 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |       825 |      3384 |     12799 |     17174 |      7005 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  12.55766     d.f. =  4     p =  0.01365213 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and SMK_CIG_STATUS 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38770 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      8093 |      4829 |       335 |      1076 |     14333 | 
##                      |     0.565 |     0.337 |     0.023 |     0.075 |     0.370 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |     13155 |      8273 |       655 |      2354 |     24437 | 
##                      |     0.538 |     0.339 |     0.027 |     0.096 |     0.630 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     21248 |     13102 |       990 |      3430 |     38770 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  61.79863     d.f. =  3     p =  2.426001e-13 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and SMK_CIG_STATUS 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      8960 |      4829 |       335 |      1076 |     15200 | 
##                           |     0.589 |     0.318 |     0.022 |     0.071 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |     14705 |      8273 |       655 |      2354 |     25987 | 
##                           |     0.566 |     0.318 |     0.025 |     0.091 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     23665 |     13102 |       990 |      3430 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  58.4398     d.f. =  3     p =  1.266198e-12 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and SMK_CIG_STATUS 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      8657 |      5082 |       345 |      1116 |     15200 | 
##                                  |     0.570 |     0.334 |     0.023 |     0.073 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |     14142 |      8719 |       675 |      2451 |     25987 | 
##                                  |     0.544 |     0.336 |     0.026 |     0.094 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     22799 |     13801 |      1020 |      3567 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  63.67693     d.f. =  3     p =  9.623397e-14 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and SMK_CIG_STATUS 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      8609 |      5105 |       351 |      1135 |     15200 | 
##                                     |     0.566 |     0.336 |     0.023 |     0.075 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |     13954 |      8787 |       714 |      2532 |     25987 | 
##                                     |     0.537 |     0.338 |     0.027 |     0.097 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     22563 |     13892 |      1065 |      3667 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  78.23742     d.f. =  3     p =  7.329201e-17 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ALC_CUR_FREQ 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39504 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       815 |       870 |      1979 |       963 |      1601 |      1657 |      3119 |      1711 |      1880 |     14595 | 
##                      |     0.056 |     0.060 |     0.136 |     0.066 |     0.110 |     0.114 |     0.214 |     0.117 |     0.129 |     0.369 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    2 |      1502 |      1721 |      5216 |      2075 |      3276 |      2651 |      4055 |      2391 |      2022 |     24909 | 
##                      |     0.060 |     0.069 |     0.209 |     0.083 |     0.132 |     0.106 |     0.163 |     0.096 |     0.081 |     0.631 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      2317 |      2591 |      7195 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     39504 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  749.4115     d.f. =  8     p =  1.635889e-156 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ALC_CUR_FREQ 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       815 |       870 |      2584 |       963 |      1601 |      1657 |      3119 |      1711 |      1880 |     15200 | 
##                           |     0.054 |     0.057 |     0.170 |     0.063 |     0.105 |     0.109 |     0.205 |     0.113 |     0.124 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         2 |      1502 |      1721 |      6294 |      2075 |      3276 |      2651 |      4055 |      2391 |      2022 |     25987 | 
##                           |     0.058 |     0.066 |     0.242 |     0.080 |     0.126 |     0.102 |     0.156 |     0.092 |     0.078 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      2317 |      2591 |      8878 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  708.6945     d.f. =  8     p =  9.610926e-148 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ALC_CUR_FREQ 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       915 |       905 |      2054 |       992 |      1694 |      1686 |      3232 |      1777 |      1945 |     15200 | 
##                                  |     0.060 |     0.060 |     0.135 |     0.065 |     0.111 |     0.111 |     0.213 |     0.117 |     0.128 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                2 |      1643 |      1809 |      5444 |      2183 |      3381 |      2729 |      4192 |      2494 |      2112 |     25987 | 
##                                  |     0.063 |     0.070 |     0.209 |     0.084 |     0.130 |     0.105 |     0.161 |     0.096 |     0.081 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      2558 |      2714 |      7498 |      3175 |      5075 |      4415 |      7424 |      4271 |      4057 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  774.2746     d.f. =  8     p =  7.198131e-162 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ALC_CUR_FREQ 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       862 |       911 |      2066 |      1010 |      1669 |      1727 |      3236 |      1783 |      1936 |     15200 | 
##                                     |     0.057 |     0.060 |     0.136 |     0.066 |     0.110 |     0.114 |     0.213 |     0.117 |     0.127 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      1583 |      1793 |      5479 |      2183 |      3409 |      2753 |      4194 |      2485 |      2108 |     25987 | 
##                                     |     0.061 |     0.069 |     0.211 |     0.084 |     0.131 |     0.106 |     0.161 |     0.096 |     0.081 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      2445 |      2704 |      7545 |      3193 |      5078 |      4480 |      7430 |      4268 |      4044 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  781.0256     d.f. =  8     p =  2.526662e-163 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  36482 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |     13353 |      1214 |        73 |     14640 | 
##                      |     0.912 |     0.083 |     0.005 |     0.401 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    2 |     18177 |      3325 |       340 |     21842 | 
##                      |     0.832 |     0.152 |     0.016 |     0.599 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     31530 |      4539 |       413 |     36482 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  489.7788     d.f. =  2     p =  4.424704e-107 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |     13913 |      1214 |        73 |     15200 | 
##                           |     0.915 |     0.080 |     0.005 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         2 |     22322 |      3325 |       340 |     25987 | 
##                           |     0.859 |     0.128 |     0.013 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  301.3859     d.f. =  2     p =  3.588183e-66 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |     13858 |      1261 |        81 |     15200 | 
##                                  |     0.912 |     0.083 |     0.005 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                2 |     21914 |      3644 |       429 |     25987 | 
##                                  |     0.843 |     0.140 |     0.017 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  412.5905     d.f. =  2     p =  2.553334e-90 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |     13861 |      1258 |        81 |     15200 | 
##                                     |     0.912 |     0.083 |     0.005 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   2 |     21655 |      3963 |       369 |     25987 | 
##                                     |     0.833 |     0.152 |     0.014 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  505.7176     d.f. =  2     p =  1.530445e-110 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39707 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |     13448 |       139 |      1056 |        17 |     14660 | 
##                      |     0.917 |     0.009 |     0.072 |     0.001 |     0.369 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |     23359 |       176 |      1104 |       408 |     25047 | 
##                      |     0.933 |     0.007 |     0.044 |     0.016 |     0.631 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     36807 |       315 |      2160 |       425 |     39707 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  339.9795     d.f. =  3     p =  2.204604e-73 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |     13988 |       139 |      1056 |        17 |     15200 | 
##                           |     0.920 |     0.009 |     0.069 |     0.001 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |     24299 |       176 |      1104 |       408 |     25987 | 
##                           |     0.935 |     0.007 |     0.042 |     0.016 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  340.1529     d.f. =  3     p =  2.021971e-73 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |     13961 |       140 |      1082 |        17 |     15200 | 
##                                  |     0.918 |     0.009 |     0.071 |     0.001 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |     24262 |       177 |      1135 |       413 |     25987 | 
##                                  |     0.934 |     0.007 |     0.044 |     0.016 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  344.8751     d.f. =  3     p =  1.920217e-74 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |     13928 |       143 |      1112 |        17 |     15200 | 
##                                     |     0.916 |     0.009 |     0.073 |     0.001 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |     24227 |       183 |      1153 |       424 |     25987 | 
##                                     |     0.932 |     0.007 |     0.044 |     0.016 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  360.835     d.f. =  3     p =  6.721412e-78 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      1377 |      2066 |     10192 |      1565 |     15200 | 
##                      |     0.091 |     0.136 |     0.671 |     0.103 |     0.369 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |      3073 |      3934 |     15245 |      3735 |     25987 | 
##                      |     0.118 |     0.151 |     0.587 |     0.144 |     0.631 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  316.7752     d.f. =  3     p =  2.327164e-68 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      1377 |      2066 |     10192 |      1565 |     15200 | 
##                           |     0.091 |     0.136 |     0.671 |     0.103 |     0.369 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |      3073 |      3934 |     15245 |      3735 |     25987 | 
##                           |     0.118 |     0.151 |     0.587 |     0.144 |     0.631 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  316.7752     d.f. =  3     p =  2.327164e-68 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      1377 |      2066 |     10192 |      1565 |     15200 | 
##                                  |     0.091 |     0.136 |     0.671 |     0.103 |     0.369 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |      3073 |      3934 |     15245 |      3735 |     25987 | 
##                                  |     0.118 |     0.151 |     0.587 |     0.144 |     0.631 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  316.7752     d.f. =  3     p =  2.327164e-68 
## 
## 
##  
## 
## Cross-tabulation between SDC_GENDER and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      1377 |      2066 |     10192 |      1565 |     15200 | 
##                                     |     0.091 |     0.136 |     0.671 |     0.103 |     0.369 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      3073 |      3934 |     15245 |      3735 |     25987 | 
##                                     |     0.118 |     0.151 |     0.587 |     0.144 |     0.631 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  316.7752     d.f. =  3     p =  2.327164e-68 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and HS_GEN_HEALTH 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39029 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    0 |       360 |      1317 |      3611 |      4566 |      1804 |     11658 | 
##                      |     0.031 |     0.113 |     0.310 |     0.392 |     0.155 |     0.299 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       397 |      1810 |      8416 |     11859 |      4889 |     27371 | 
##                      |     0.015 |     0.066 |     0.307 |     0.433 |     0.179 |     0.701 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |       757 |      3127 |     12027 |     16425 |      6693 |     39029 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  397.8757     d.f. =  4     p =  8.003618e-85 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and HS_GEN_HEALTH 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         0 |       360 |      1317 |      3611 |      4678 |      1804 |     11770 | 
##                           |     0.031 |     0.112 |     0.307 |     0.397 |     0.153 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       448 |      1973 |      8961 |     12932 |      5103 |     29417 | 
##                           |     0.015 |     0.067 |     0.305 |     0.440 |     0.173 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |       808 |      3290 |     12572 |     17610 |      6907 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  368.0409     d.f. =  4     p =  2.229239e-78 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and HS_GEN_HEALTH 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                0 |       393 |      1443 |      3825 |      4845 |      1900 |     12406 | 
##                                  |     0.032 |     0.116 |     0.308 |     0.391 |     0.153 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       430 |      1933 |      9096 |     12239 |      5083 |     28781 | 
##                                  |     0.015 |     0.067 |     0.316 |     0.425 |     0.177 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |       823 |      3376 |     12921 |     17084 |      6983 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  432.0271     d.f. =  4     p =  3.334229e-92 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and HS_GEN_HEALTH 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         4 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |       389 |      1432 |      3864 |      4797 |      1901 |     12383 | 
##                                     |     0.031 |     0.116 |     0.312 |     0.387 |     0.154 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       436 |      1952 |      8935 |     12377 |      5104 |     28804 | 
##                                     |     0.015 |     0.068 |     0.310 |     0.430 |     0.177 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |       825 |      3384 |     12799 |     17174 |      7005 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  421.9498     d.f. =  4     p =  5.023994e-90 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and SMK_CIG_STATUS 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  37994 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      5735 |      4272 |       280 |      1082 |     11369 | 
##                      |     0.504 |     0.376 |     0.025 |     0.095 |     0.299 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |     15102 |      8594 |       680 |      2249 |     26625 | 
##                      |     0.567 |     0.323 |     0.026 |     0.084 |     0.701 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     20837 |     12866 |       960 |      3331 |     37994 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  133.9416     d.f. =  3     p =  7.648224e-29 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and SMK_CIG_STATUS 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      6136 |      4272 |       280 |      1082 |     11770 | 
##                           |     0.521 |     0.363 |     0.024 |     0.092 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |     17529 |      8830 |       710 |      2348 |     29417 | 
##                           |     0.596 |     0.300 |     0.024 |     0.080 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     23665 |     13102 |       990 |      3430 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  200.3597     d.f. =  3     p =  3.527297e-43 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and SMK_CIG_STATUS 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      6341 |      4610 |       289 |      1166 |     12406 | 
##                                  |     0.511 |     0.372 |     0.023 |     0.094 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |     16458 |      9191 |       731 |      2401 |     28781 | 
##                                  |     0.572 |     0.319 |     0.025 |     0.083 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     22799 |     13801 |      1020 |      3567 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  141.0815     d.f. =  3     p =  2.209293e-30 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and SMK_CIG_STATUS 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      6244 |      4629 |       314 |      1196 |     12383 | 
##                                     |     0.504 |     0.374 |     0.025 |     0.097 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |     16319 |      9263 |       751 |      2471 |     28804 | 
##                                     |     0.567 |     0.322 |     0.026 |     0.086 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     22563 |     13892 |      1065 |      3667 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  142.9397     d.f. =  3     p =  8.781447e-31 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ALC_CUR_FREQ 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38729 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    0 |       776 |       816 |      2112 |       821 |      1281 |      1149 |      1945 |      1257 |      1419 |     11576 | 
##                      |     0.067 |     0.070 |     0.182 |     0.071 |     0.111 |     0.099 |     0.168 |     0.109 |     0.123 |     0.299 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      1422 |      1717 |      4924 |      2165 |      3526 |      3083 |      5128 |      2781 |      2407 |     27153 | 
##                      |     0.052 |     0.063 |     0.181 |     0.080 |     0.130 |     0.114 |     0.189 |     0.102 |     0.089 |     0.701 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      2198 |      2533 |      7036 |      2986 |      4807 |      4232 |      7073 |      4038 |      3826 |     38729 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  201.6318     d.f. =  8     p =  2.894945e-39 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ALC_CUR_FREQ 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         0 |       776 |       816 |      2306 |       821 |      1281 |      1149 |      1945 |      1257 |      1419 |     11770 | 
##                           |     0.066 |     0.069 |     0.196 |     0.070 |     0.109 |     0.098 |     0.165 |     0.107 |     0.121 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      1541 |      1775 |      6572 |      2217 |      3596 |      3159 |      5229 |      2845 |      2483 |     29417 | 
##                           |     0.052 |     0.060 |     0.223 |     0.075 |     0.122 |     0.107 |     0.178 |     0.097 |     0.084 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      2317 |      2591 |      8878 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  223.8068     d.f. =  8     p =  6.040035e-44 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ALC_CUR_FREQ 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                0 |       948 |       858 |      2263 |       888 |      1361 |      1203 |      2046 |      1332 |      1507 |     12406 | 
##                                  |     0.076 |     0.069 |     0.182 |     0.072 |     0.110 |     0.097 |     0.165 |     0.107 |     0.121 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      1610 |      1856 |      5235 |      2287 |      3714 |      3212 |      5378 |      2939 |      2550 |     28781 | 
##                                  |     0.056 |     0.064 |     0.182 |     0.079 |     0.129 |     0.112 |     0.187 |     0.102 |     0.089 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      2558 |      2714 |      7498 |      3175 |      5075 |      4415 |      7424 |      4271 |      4057 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  232.5835     d.f. =  8     p =  8.411726e-46 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ALC_CUR_FREQ 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |       874 |       870 |      2286 |       892 |      1360 |      1214 |      2050 |      1324 |      1513 |     12383 | 
##                                     |     0.071 |     0.070 |     0.185 |     0.072 |     0.110 |     0.098 |     0.166 |     0.107 |     0.122 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      1571 |      1834 |      5259 |      2301 |      3718 |      3266 |      5380 |      2944 |      2531 |     28804 | 
##                                     |     0.055 |     0.064 |     0.183 |     0.080 |     0.129 |     0.113 |     0.187 |     0.102 |     0.088 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      2445 |      2704 |      7545 |      3193 |      5078 |      4480 |      7430 |      4268 |      4044 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  222.4642     d.f. =  8     p =  1.160938e-43 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  35099 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    0 |      8748 |      1487 |       139 |     10374 | 
##                      |     0.843 |     0.143 |     0.013 |     0.296 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |     21663 |      2837 |       225 |     24725 | 
##                      |     0.876 |     0.115 |     0.009 |     0.704 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     30411 |      4324 |       364 |     35099 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  70.65945     d.f. =  2     p =  4.534134e-16 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         0 |     10144 |      1487 |       139 |     11770 | 
##                           |     0.862 |     0.126 |     0.012 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |     26091 |      3052 |       274 |     29417 | 
##                           |     0.887 |     0.104 |     0.009 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  50.15434     d.f. =  2     p =  1.285652e-11 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                0 |     10503 |      1702 |       201 |     12406 | 
##                                  |     0.847 |     0.137 |     0.016 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |     25269 |      3203 |       309 |     28781 | 
##                                  |     0.878 |     0.111 |     0.011 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  79.57838     d.f. =  2     p =  5.245348e-18 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   0 |     10400 |      1813 |       170 |     12383 | 
##                                     |     0.840 |     0.146 |     0.014 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |     25116 |      3408 |       280 |     28804 | 
##                                     |     0.872 |     0.118 |     0.010 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  76.99765     d.f. =  2     p =  1.906221e-17 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38194 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |     10309 |       103 |       852 |       108 |     11372 | 
##                      |     0.907 |     0.009 |     0.075 |     0.009 |     0.298 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |     25163 |       181 |      1175 |       303 |     26822 | 
##                      |     0.938 |     0.007 |     0.044 |     0.011 |     0.702 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     35472 |       284 |      2027 |       411 |     38194 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  162.4005     d.f. =  3     p =  5.559974e-35 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |     10707 |       103 |       852 |       108 |     11770 | 
##                           |     0.910 |     0.009 |     0.072 |     0.009 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |     27580 |       212 |      1308 |       317 |     29417 | 
##                           |     0.938 |     0.007 |     0.044 |     0.011 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  136.715     d.f. =  3     p =  1.930673e-29 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |     11230 |       116 |       947 |       113 |     12406 | 
##                                  |     0.905 |     0.009 |     0.076 |     0.009 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |     26993 |       201 |      1270 |       317 |     28781 | 
##                                  |     0.938 |     0.007 |     0.044 |     0.011 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  186.3606     d.f. =  3     p =  3.730229e-40 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |     11195 |       115 |       959 |       114 |     12383 | 
##                                     |     0.904 |     0.009 |     0.077 |     0.009 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |     26960 |       211 |      1306 |       327 |     28804 | 
##                                     |     0.936 |     0.007 |     0.045 |     0.011 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  179.7636     d.f. =  3     p =  9.919917e-39 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39260 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      1526 |      1631 |      7286 |      1327 |     11770 | 
##                      |     0.130 |     0.139 |     0.619 |     0.113 |     0.300 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      2882 |      4364 |     16418 |      3826 |     27490 | 
##                      |     0.105 |     0.159 |     0.597 |     0.139 |     0.700 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4408 |      5995 |     23704 |      5153 |     39260 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  117.5231     d.f. =  3     p =  2.635363e-25 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      1526 |      1631 |      7286 |      1327 |     11770 | 
##                           |     0.130 |     0.139 |     0.619 |     0.113 |     0.286 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      2924 |      4369 |     18151 |      3973 |     29417 | 
##                           |     0.099 |     0.149 |     0.617 |     0.135 |     0.714 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  109.5046     d.f. =  3     p =  1.402621e-23 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      1534 |      1633 |      7851 |      1388 |     12406 | 
##                                  |     0.124 |     0.132 |     0.633 |     0.112 |     0.301 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      2916 |      4367 |     17586 |      3912 |     28781 | 
##                                  |     0.101 |     0.152 |     0.611 |     0.136 |     0.699 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  109.6843     d.f. =  3     p =  1.283166e-23 
## 
## 
##  
## 
## Cross-tabulation between WRK_EMPLOYMENT and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      1544 |      1634 |      7833 |      1372 |     12383 | 
##                                     |     0.125 |     0.132 |     0.633 |     0.111 |     0.301 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      2906 |      4366 |     17604 |      3928 |     28804 | 
##                                     |     0.101 |     0.152 |     0.611 |     0.136 |     0.699 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  118.7115     d.f. =  3     p =  1.461925e-25 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and SMK_CIG_STATUS 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38508 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       319 |       267 |        22 |       159 |       767 | 
##                      |     0.416 |     0.348 |     0.029 |     0.207 |     0.020 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |      1391 |      1108 |       107 |       489 |      3095 | 
##                      |     0.449 |     0.358 |     0.035 |     0.158 |     0.080 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |      6195 |      4178 |       265 |      1268 |     11906 | 
##                      |     0.520 |     0.351 |     0.022 |     0.107 |     0.309 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    4 |      9223 |      5388 |       410 |      1113 |     16134 | 
##                      |     0.572 |     0.334 |     0.025 |     0.069 |     0.419 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    5 |      3983 |      2084 |       180 |       359 |      6606 | 
##                      |     0.603 |     0.315 |     0.027 |     0.054 |     0.172 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     21111 |     13025 |       984 |      3388 |     38508 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  679.2301     d.f. =  12     p =  1.228079e-137 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and SMK_CIG_STATUS 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       360 |       267 |        22 |       159 |       808 | 
##                           |     0.446 |     0.330 |     0.027 |     0.197 |     0.020 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |      1586 |      1108 |       107 |       489 |      3290 | 
##                           |     0.482 |     0.337 |     0.033 |     0.149 |     0.080 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |      6861 |      4178 |       265 |      1268 |     12572 | 
##                           |     0.546 |     0.332 |     0.021 |     0.101 |     0.305 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         4 |     10574 |      5465 |       416 |      1155 |     17610 | 
##                           |     0.600 |     0.310 |     0.024 |     0.066 |     0.428 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         5 |      4284 |      2084 |       180 |       359 |      6907 | 
##                           |     0.620 |     0.302 |     0.026 |     0.052 |     0.168 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     23665 |     13102 |       990 |      3430 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  661.2721     d.f. =  12     p =  8.526377e-134 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and SMK_CIG_STATUS 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       342 |       284 |        23 |       174 |       823 | 
##                                  |     0.416 |     0.345 |     0.028 |     0.211 |     0.020 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |      1550 |      1199 |       114 |       513 |      3376 | 
##                                  |     0.459 |     0.355 |     0.034 |     0.152 |     0.082 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |      6804 |      4491 |       272 |      1354 |     12921 | 
##                                  |     0.527 |     0.348 |     0.021 |     0.105 |     0.314 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                4 |      9859 |      5667 |       414 |      1144 |     17084 | 
##                                  |     0.577 |     0.332 |     0.024 |     0.067 |     0.415 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                5 |      4244 |      2160 |       197 |       382 |      6983 | 
##                                  |     0.608 |     0.309 |     0.028 |     0.055 |     0.170 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     22799 |     13801 |      1020 |      3567 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  722.7182     d.f. =  12     p =  6.029546e-147 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and SMK_CIG_STATUS 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       345 |       281 |        26 |       173 |       825 | 
##                                     |     0.418 |     0.341 |     0.032 |     0.210 |     0.020 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      1526 |      1199 |       116 |       543 |      3384 | 
##                                     |     0.451 |     0.354 |     0.034 |     0.160 |     0.082 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |      6657 |      4485 |       290 |      1367 |     12799 | 
##                                     |     0.520 |     0.350 |     0.023 |     0.107 |     0.311 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |      9792 |      5738 |       442 |      1202 |     17174 | 
##                                     |     0.570 |     0.334 |     0.026 |     0.070 |     0.417 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |      4243 |      2189 |       191 |       382 |      7005 | 
##                                     |     0.606 |     0.312 |     0.027 |     0.055 |     0.170 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     22563 |     13892 |      1065 |      3667 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  736.2341     d.f. =  12     p =  7.681881e-150 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ALC_CUR_FREQ 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39256 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |        75 |       121 |       189 |        60 |        84 |        55 |        94 |        43 |        54 |       775 | 
##                      |     0.097 |     0.156 |     0.244 |     0.077 |     0.108 |     0.071 |     0.121 |     0.055 |     0.070 |     0.020 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       253 |       314 |       766 |       268 |       339 |       280 |       401 |       268 |       257 |      3146 | 
##                      |     0.080 |     0.100 |     0.243 |     0.085 |     0.108 |     0.089 |     0.127 |     0.085 |     0.082 |     0.080 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    3 |       731 |       950 |      2645 |       961 |      1496 |      1249 |      1840 |      1115 |      1140 |     12127 | 
##                      |     0.060 |     0.078 |     0.218 |     0.079 |     0.123 |     0.103 |     0.152 |     0.092 |     0.094 |     0.309 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    4 |       859 |       881 |      2603 |      1238 |      2071 |      1876 |      3404 |      1882 |      1670 |     16484 | 
##                      |     0.052 |     0.053 |     0.158 |     0.075 |     0.126 |     0.114 |     0.207 |     0.114 |     0.101 |     0.420 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    5 |       342 |       299 |       947 |       492 |       869 |       825 |      1403 |       781 |       766 |      6724 | 
##                      |     0.051 |     0.044 |     0.141 |     0.073 |     0.129 |     0.123 |     0.209 |     0.116 |     0.114 |     0.171 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      2260 |      2565 |      7150 |      3019 |      4859 |      4285 |      7142 |      4089 |      3887 |     39256 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  986.5904     d.f. =  32     p =  1.143138e-186 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ALC_CUR_FREQ 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |        75 |       121 |       222 |        60 |        84 |        55 |        94 |        43 |        54 |       808 | 
##                           |     0.093 |     0.150 |     0.275 |     0.074 |     0.104 |     0.068 |     0.116 |     0.053 |     0.067 |     0.020 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       253 |       314 |       910 |       268 |       339 |       280 |       401 |       268 |       257 |      3290 | 
##                           |     0.077 |     0.095 |     0.277 |     0.081 |     0.103 |     0.085 |     0.122 |     0.081 |     0.078 |     0.080 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         3 |       731 |       950 |      3090 |       961 |      1496 |      1249 |      1840 |      1115 |      1140 |     12572 | 
##                           |     0.058 |     0.076 |     0.246 |     0.076 |     0.119 |     0.099 |     0.146 |     0.089 |     0.091 |     0.305 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         4 |       916 |       907 |      3526 |      1257 |      2089 |      1899 |      3436 |      1895 |      1685 |     17610 | 
##                           |     0.052 |     0.052 |     0.200 |     0.071 |     0.119 |     0.108 |     0.195 |     0.108 |     0.096 |     0.428 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         5 |       342 |       299 |      1130 |       492 |       869 |       825 |      1403 |       781 |       766 |      6907 | 
##                           |     0.050 |     0.043 |     0.164 |     0.071 |     0.126 |     0.119 |     0.203 |     0.113 |     0.111 |     0.168 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      2317 |      2591 |      8878 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  912.474     d.f. =  32     p =  4.41201e-171 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ALC_CUR_FREQ 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |        81 |       130 |       203 |        65 |        87 |        59 |        98 |        44 |        56 |       823 | 
##                                  |     0.098 |     0.158 |     0.247 |     0.079 |     0.106 |     0.072 |     0.119 |     0.053 |     0.068 |     0.020 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       283 |       320 |       824 |       293 |       351 |       292 |       435 |       304 |       274 |      3376 | 
##                                  |     0.084 |     0.095 |     0.244 |     0.087 |     0.104 |     0.086 |     0.129 |     0.090 |     0.081 |     0.082 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                3 |       858 |      1028 |      2796 |      1040 |      1571 |      1298 |      1940 |      1177 |      1213 |     12921 | 
##                                  |     0.066 |     0.080 |     0.216 |     0.080 |     0.122 |     0.100 |     0.150 |     0.091 |     0.094 |     0.314 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                4 |       941 |       916 |      2695 |      1264 |      2162 |      1921 |      3517 |      1951 |      1717 |     17084 | 
##                                  |     0.055 |     0.054 |     0.158 |     0.074 |     0.127 |     0.112 |     0.206 |     0.114 |     0.101 |     0.415 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                5 |       395 |       320 |       980 |       513 |       904 |       845 |      1434 |       795 |       797 |      6983 | 
##                                  |     0.057 |     0.046 |     0.140 |     0.073 |     0.129 |     0.121 |     0.205 |     0.114 |     0.114 |     0.170 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      2558 |      2714 |      7498 |      3175 |      5075 |      4415 |      7424 |      4271 |      4057 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1026.213     d.f. =  32     p =  5.131109e-195 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ALC_CUR_FREQ 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |        79 |       127 |       204 |        62 |        87 |        62 |       100 |        48 |        56 |       825 | 
##                                     |     0.096 |     0.154 |     0.247 |     0.075 |     0.105 |     0.075 |     0.121 |     0.058 |     0.068 |     0.020 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       285 |       339 |       830 |       292 |       357 |       297 |       422 |       291 |       271 |      3384 | 
##                                     |     0.084 |     0.100 |     0.245 |     0.086 |     0.105 |     0.088 |     0.125 |     0.086 |     0.080 |     0.082 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |       795 |      1006 |      2804 |      1019 |      1572 |      1310 |      1918 |      1180 |      1195 |     12799 | 
##                                     |     0.062 |     0.079 |     0.219 |     0.080 |     0.123 |     0.102 |     0.150 |     0.092 |     0.093 |     0.311 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |       919 |       914 |      2720 |      1294 |      2162 |      1954 |      3538 |      1944 |      1729 |     17174 | 
##                                     |     0.054 |     0.053 |     0.158 |     0.075 |     0.126 |     0.114 |     0.206 |     0.113 |     0.101 |     0.417 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |       367 |       318 |       987 |       526 |       900 |       857 |      1452 |       805 |       793 |      7005 | 
##                                     |     0.052 |     0.045 |     0.141 |     0.075 |     0.128 |     0.122 |     0.207 |     0.115 |     0.113 |     0.170 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      2445 |      2704 |      7545 |      3193 |      5078 |      4480 |      7430 |      4268 |      4044 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1051.614     d.f. =  32     p =  2.255941e-200 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  36185 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |       451 |       267 |        12 |       730 | 
##                      |     0.618 |     0.366 |     0.016 |     0.020 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    2 |      2202 |       740 |        47 |      2989 | 
##                      |     0.737 |     0.248 |     0.016 |     0.083 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    3 |      9585 |      1603 |       124 |     11312 | 
##                      |     0.847 |     0.142 |     0.011 |     0.313 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    4 |     13530 |      1385 |       133 |     15048 | 
##                      |     0.899 |     0.092 |     0.009 |     0.416 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    5 |      5583 |       480 |        43 |      6106 | 
##                      |     0.914 |     0.079 |     0.007 |     0.169 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     31351 |      4475 |       359 |     36185 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1139.762     d.f. =  8     p =  9.890398e-241 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |       529 |       267 |        12 |       808 | 
##                           |     0.655 |     0.330 |     0.015 |     0.020 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         2 |      2503 |       740 |        47 |      3290 | 
##                           |     0.761 |     0.225 |     0.014 |     0.080 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         3 |     10845 |      1603 |       124 |     12572 | 
##                           |     0.863 |     0.128 |     0.010 |     0.305 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         4 |     15974 |      1449 |       187 |     17610 | 
##                           |     0.907 |     0.082 |     0.011 |     0.428 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         5 |      6384 |       480 |        43 |      6907 | 
##                           |     0.924 |     0.069 |     0.006 |     0.168 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1163.713     d.f. =  8     p =  6.629579e-246 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |       520 |       288 |        15 |       823 | 
##                                  |     0.632 |     0.350 |     0.018 |     0.020 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                2 |      2516 |       799 |        61 |      3376 | 
##                                  |     0.745 |     0.237 |     0.018 |     0.082 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                3 |     10921 |      1803 |       197 |     12921 | 
##                                  |     0.845 |     0.140 |     0.015 |     0.314 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                4 |     15425 |      1488 |       171 |     17084 | 
##                                  |     0.903 |     0.087 |     0.010 |     0.415 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                5 |      6390 |       527 |        66 |      6983 | 
##                                  |     0.915 |     0.075 |     0.009 |     0.170 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1257.104     d.f. =  8     p =  4.388501e-266 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |       495 |       318 |        12 |       825 | 
##                                     |     0.600 |     0.385 |     0.015 |     0.020 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   2 |      2473 |       855 |        56 |      3384 | 
##                                     |     0.731 |     0.253 |     0.017 |     0.082 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   3 |     10787 |      1849 |       163 |     12799 | 
##                                     |     0.843 |     0.144 |     0.013 |     0.311 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   4 |     15391 |      1614 |       169 |     17174 | 
##                                     |     0.896 |     0.094 |     0.010 |     0.417 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   5 |      6370 |       585 |        50 |      7005 | 
##                                     |     0.909 |     0.084 |     0.007 |     0.170 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1345.131     d.f. =  8     p =  4.126292e-285 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39337 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       609 |        18 |       125 |        15 |       767 | 
##                      |     0.794 |     0.023 |     0.163 |     0.020 |     0.019 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |      2563 |        58 |       490 |        56 |      3167 | 
##                      |     0.809 |     0.018 |     0.155 |     0.018 |     0.081 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |     11009 |       146 |       872 |       167 |     12194 | 
##                      |     0.903 |     0.012 |     0.072 |     0.014 |     0.310 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    4 |     15807 |        65 |       478 |       127 |     16477 | 
##                      |     0.959 |     0.004 |     0.029 |     0.008 |     0.419 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    5 |      6529 |        18 |       129 |        56 |      6732 | 
##                      |     0.970 |     0.003 |     0.019 |     0.008 |     0.171 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     36517 |       305 |      2094 |       421 |     39337 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1491.438     d.f. =  12     p =  2.660341e-312 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       650 |        18 |       125 |        15 |       808 | 
##                           |     0.804 |     0.022 |     0.155 |     0.019 |     0.020 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |      2686 |        58 |       490 |        56 |      3290 | 
##                           |     0.816 |     0.018 |     0.149 |     0.017 |     0.080 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |     11387 |       146 |       872 |       167 |     12572 | 
##                           |     0.906 |     0.012 |     0.069 |     0.013 |     0.305 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         4 |     16860 |        75 |       544 |       131 |     17610 | 
##                           |     0.957 |     0.004 |     0.031 |     0.007 |     0.428 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         5 |      6704 |        18 |       129 |        56 |      6907 | 
##                           |     0.971 |     0.003 |     0.019 |     0.008 |     0.168 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1402.253     d.f. =  12     p =  4.544385e-293 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       661 |        18 |       129 |        15 |       823 | 
##                                  |     0.803 |     0.022 |     0.157 |     0.018 |     0.020 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |      2741 |        59 |       517 |        59 |      3376 | 
##                                  |     0.812 |     0.017 |     0.153 |     0.017 |     0.082 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |     11657 |       153 |       941 |       170 |     12921 | 
##                                  |     0.902 |     0.012 |     0.073 |     0.013 |     0.314 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                4 |     16396 |        67 |       493 |       128 |     17084 | 
##                                  |     0.960 |     0.004 |     0.029 |     0.007 |     0.415 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                5 |      6768 |        20 |       137 |        58 |      6983 | 
##                                  |     0.969 |     0.003 |     0.020 |     0.008 |     0.170 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1512.611     d.f. =  12     p =  7.207978e-317 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       653 |        19 |       137 |        16 |       825 | 
##                                     |     0.792 |     0.023 |     0.166 |     0.019 |     0.020 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      2725 |        63 |       536 |        60 |      3384 | 
##                                     |     0.805 |     0.019 |     0.158 |     0.018 |     0.082 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |     11526 |       156 |       941 |       176 |     12799 | 
##                                     |     0.901 |     0.012 |     0.074 |     0.014 |     0.311 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |     16459 |        68 |       516 |       131 |     17174 | 
##                                     |     0.958 |     0.004 |     0.030 |     0.008 |     0.417 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |      6792 |        20 |       135 |        58 |      7005 | 
##                                     |     0.970 |     0.003 |     0.019 |     0.008 |     0.170 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  1602.326     d.f. =  12     p =  0 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  40515 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |        73 |        43 |       638 |        54 |       808 | 
##                      |     0.090 |     0.053 |     0.790 |     0.067 |     0.020 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       264 |       315 |      2352 |       359 |      3290 | 
##                      |     0.080 |     0.096 |     0.715 |     0.109 |     0.081 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |      1298 |      1731 |      7951 |      1592 |     12572 | 
##                      |     0.103 |     0.138 |     0.632 |     0.127 |     0.310 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    4 |      1889 |      2866 |      9887 |      2296 |     16938 | 
##                      |     0.112 |     0.169 |     0.584 |     0.136 |     0.418 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    5 |       877 |      1045 |      4131 |       854 |      6907 | 
##                      |     0.127 |     0.151 |     0.598 |     0.124 |     0.170 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4401 |      6000 |     24959 |      5155 |     40515 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  394.7173     d.f. =  12     p =  4.970586e-77 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |        73 |        43 |       638 |        54 |       808 | 
##                           |     0.090 |     0.053 |     0.790 |     0.067 |     0.020 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       264 |       315 |      2352 |       359 |      3290 | 
##                           |     0.080 |     0.096 |     0.715 |     0.109 |     0.080 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |      1298 |      1731 |      7951 |      1592 |     12572 | 
##                           |     0.103 |     0.138 |     0.632 |     0.127 |     0.305 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         4 |      1938 |      2866 |     10365 |      2441 |     17610 | 
##                           |     0.110 |     0.163 |     0.589 |     0.139 |     0.428 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         5 |       877 |      1045 |      4131 |       854 |      6907 | 
##                           |     0.127 |     0.151 |     0.598 |     0.124 |     0.168 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  369.0326     d.f. =  12     p =  1.344163e-71 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |        75 |        43 |       648 |        57 |       823 | 
##                                  |     0.091 |     0.052 |     0.787 |     0.069 |     0.020 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       267 |       315 |      2413 |       381 |      3376 | 
##                                  |     0.079 |     0.093 |     0.715 |     0.113 |     0.082 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |      1326 |      1731 |      8192 |      1672 |     12921 | 
##                                  |     0.103 |     0.134 |     0.634 |     0.129 |     0.314 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                4 |      1903 |      2866 |      9992 |      2323 |     17084 | 
##                                  |     0.111 |     0.168 |     0.585 |     0.136 |     0.415 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                5 |       879 |      1045 |      4192 |       867 |      6983 | 
##                                  |     0.126 |     0.150 |     0.600 |     0.124 |     0.170 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  403.2071     d.f. =  12     p =  7.922401e-79 
## 
## 
##  
## 
## Cross-tabulation between HS_GEN_HEALTH and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |        75 |        43 |       651 |        56 |       825 | 
##                                     |     0.091 |     0.052 |     0.789 |     0.068 |     0.020 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       274 |       315 |      2419 |       376 |      3384 | 
##                                     |     0.081 |     0.093 |     0.715 |     0.111 |     0.082 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |      1318 |      1731 |      8109 |      1641 |     12799 | 
##                                     |     0.103 |     0.135 |     0.634 |     0.128 |     0.311 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |      1898 |      2866 |     10051 |      2359 |     17174 | 
##                                     |     0.111 |     0.167 |     0.585 |     0.137 |     0.417 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |       885 |      1045 |      4207 |       868 |      7005 | 
##                                     |     0.126 |     0.149 |     0.601 |     0.124 |     0.170 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  399.7851     d.f. =  12     p =  4.20252e-78 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ALC_CUR_FREQ 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38410 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      1691 |      1449 |      3975 |      1667 |      2678 |      2329 |      3658 |      1889 |      1698 |     21034 | 
##                      |     0.080 |     0.069 |     0.189 |     0.079 |     0.127 |     0.111 |     0.174 |     0.090 |     0.081 |     0.548 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       397 |       763 |      2235 |       978 |      1574 |      1358 |      2502 |      1606 |      1586 |     12999 | 
##                      |     0.031 |     0.059 |     0.172 |     0.075 |     0.121 |     0.104 |     0.192 |     0.124 |     0.122 |     0.338 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    2 |        22 |        37 |       136 |        67 |       116 |       121 |       211 |       135 |       135 |       980 | 
##                      |     0.022 |     0.038 |     0.139 |     0.068 |     0.118 |     0.123 |     0.215 |     0.138 |     0.138 |     0.026 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                    3 |       144 |       277 |       670 |       262 |       359 |       370 |       609 |       352 |       354 |      3397 | 
##                      |     0.042 |     0.082 |     0.197 |     0.077 |     0.106 |     0.109 |     0.179 |     0.104 |     0.104 |     0.088 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      2254 |      2526 |      7016 |      2974 |      4727 |      4178 |      6980 |      3982 |      3773 |     38410 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  744.2668     d.f. =  24     p =  1.185903e-141 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ALC_CUR_FREQ 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      1754 |      1514 |      5691 |      1731 |      2828 |      2459 |      3852 |      2009 |      1827 |     23665 | 
##                           |     0.074 |     0.064 |     0.240 |     0.073 |     0.120 |     0.104 |     0.163 |     0.085 |     0.077 |     0.575 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       397 |       763 |      2338 |       978 |      1574 |      1358 |      2502 |      1606 |      1586 |     13102 | 
##                           |     0.030 |     0.058 |     0.178 |     0.075 |     0.120 |     0.104 |     0.191 |     0.123 |     0.121 |     0.318 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         2 |        22 |        37 |       146 |        67 |       116 |       121 |       211 |       135 |       135 |       990 | 
##                           |     0.022 |     0.037 |     0.147 |     0.068 |     0.117 |     0.122 |     0.213 |     0.136 |     0.136 |     0.024 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                         3 |       144 |       277 |       703 |       262 |       359 |       370 |       609 |       352 |       354 |      3430 | 
##                           |     0.042 |     0.081 |     0.205 |     0.076 |     0.105 |     0.108 |     0.178 |     0.103 |     0.103 |     0.083 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      2317 |      2591 |      8878 |      3038 |      4877 |      4308 |      7174 |      4102 |      3902 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  917.7328     d.f. =  24     p =  2.539638e-178 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ALC_CUR_FREQ 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      1942 |      1577 |      4279 |      1798 |      2889 |      2484 |      3918 |      2057 |      1855 |     22799 | 
##                                  |     0.085 |     0.069 |     0.188 |     0.079 |     0.127 |     0.109 |     0.172 |     0.090 |     0.081 |     0.554 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       438 |       806 |      2377 |      1036 |      1692 |      1426 |      2648 |      1695 |      1683 |     13801 | 
##                                  |     0.032 |     0.058 |     0.172 |     0.075 |     0.123 |     0.103 |     0.192 |     0.123 |     0.122 |     0.335 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                2 |        23 |        41 |       139 |        68 |       118 |       126 |       219 |       139 |       147 |      1020 | 
##                                  |     0.023 |     0.040 |     0.136 |     0.067 |     0.116 |     0.124 |     0.215 |     0.136 |     0.144 |     0.025 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                3 |       155 |       290 |       703 |       273 |       376 |       379 |       639 |       380 |       372 |      3567 | 
##                                  |     0.043 |     0.081 |     0.197 |     0.077 |     0.105 |     0.106 |     0.179 |     0.107 |     0.104 |     0.087 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      2558 |      2714 |      7498 |      3175 |      5075 |      4415 |      7424 |      4271 |      4057 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  825.3224     d.f. =  24     p =  9.238488e-159 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ALC_CUR_FREQ 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         0 |         1 |         2 |         3 |         4 |         5 |         6 |         7 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      1824 |      1562 |      4264 |      1791 |      2863 |      2503 |      3894 |      2018 |      1844 |     22563 | 
##                                     |     0.081 |     0.069 |     0.189 |     0.079 |     0.127 |     0.111 |     0.173 |     0.089 |     0.082 |     0.548 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       426 |       801 |      2407 |      1054 |      1709 |      1444 |      2653 |      1711 |      1687 |     13892 | 
##                                     |     0.031 |     0.058 |     0.173 |     0.076 |     0.123 |     0.104 |     0.191 |     0.123 |     0.121 |     0.337 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |        28 |        40 |       140 |        73 |       124 |       130 |       230 |       153 |       147 |      1065 | 
##                                     |     0.026 |     0.038 |     0.131 |     0.069 |     0.116 |     0.122 |     0.216 |     0.144 |     0.138 |     0.026 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |       167 |       301 |       734 |       275 |       382 |       403 |       653 |       386 |       366 |      3667 | 
##                                     |     0.046 |     0.082 |     0.200 |     0.075 |     0.104 |     0.110 |     0.178 |     0.105 |     0.100 |     0.089 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      2445 |      2704 |      7545 |      3193 |      5078 |      4480 |      7430 |      4268 |      4044 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  791.9337     d.f. =  24     p =  1.044929e-151 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  34604 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    0 |     16796 |      2047 |       154 |     18997 | 
##                      |     0.884 |     0.108 |     0.008 |     0.549 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |     10007 |      1463 |       138 |     11608 | 
##                      |     0.862 |     0.126 |     0.012 |     0.335 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    2 |       752 |       132 |         9 |       893 | 
##                      |     0.842 |     0.148 |     0.010 |     0.026 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    3 |      2489 |       557 |        60 |      3106 | 
##                      |     0.801 |     0.179 |     0.019 |     0.090 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     30044 |      4199 |       361 |     34604 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  180.7127     d.f. =  6     p =  2.39458e-36 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         0 |     21072 |      2387 |       206 |     23665 | 
##                           |     0.890 |     0.101 |     0.009 |     0.575 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |     11501 |      1463 |       138 |     13102 | 
##                           |     0.878 |     0.112 |     0.011 |     0.318 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         2 |       849 |       132 |         9 |       990 | 
##                           |     0.858 |     0.133 |     0.009 |     0.024 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         3 |      2813 |       557 |        60 |      3430 | 
##                           |     0.820 |     0.162 |     0.017 |     0.083 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  149.7     d.f. =  6     p =  8.95382e-30 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                0 |     20112 |      2443 |       244 |     22799 | 
##                                  |     0.882 |     0.107 |     0.011 |     0.554 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |     11914 |      1699 |       188 |     13801 | 
##                                  |     0.863 |     0.123 |     0.014 |     0.335 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                2 |       871 |       138 |        11 |      1020 | 
##                                  |     0.854 |     0.135 |     0.011 |     0.025 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                3 |      2875 |       625 |        67 |      3567 | 
##                                  |     0.806 |     0.175 |     0.019 |     0.087 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  166.2883     d.f. =  6     p =  2.754478e-33 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   0 |     19846 |      2533 |       184 |     22563 | 
##                                     |     0.880 |     0.112 |     0.008 |     0.548 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |     11876 |      1838 |       178 |     13892 | 
##                                     |     0.855 |     0.132 |     0.013 |     0.337 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   2 |       897 |       158 |        10 |      1065 | 
##                                     |     0.842 |     0.148 |     0.009 |     0.026 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   3 |      2897 |       692 |        78 |      3667 | 
##                                     |     0.790 |     0.189 |     0.021 |     0.089 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  243.6633     d.f. =  6     p =  9.264327e-50 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  37712 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |     19376 |       144 |       951 |       206 |     20677 | 
##                      |     0.937 |     0.007 |     0.046 |     0.010 |     0.548 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |     11761 |       104 |       751 |       138 |     12754 | 
##                      |     0.922 |     0.008 |     0.059 |     0.011 |     0.338 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       909 |         3 |        42 |         9 |       963 | 
##                      |     0.944 |     0.003 |     0.044 |     0.009 |     0.026 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |      2968 |        39 |       265 |        46 |      3318 | 
##                      |     0.895 |     0.012 |     0.080 |     0.014 |     0.088 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     35014 |       290 |      2009 |       399 |     37712 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  96.26827     d.f. =  9     p =  8.925064e-17 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |     22162 |       169 |      1102 |       232 |     23665 | 
##                           |     0.936 |     0.007 |     0.047 |     0.010 |     0.575 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |     12109 |       104 |       751 |       138 |     13102 | 
##                           |     0.924 |     0.008 |     0.057 |     0.011 |     0.318 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       936 |         3 |        42 |         9 |       990 | 
##                           |     0.945 |     0.003 |     0.042 |     0.009 |     0.024 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |      3080 |        39 |       265 |        46 |      3430 | 
##                           |     0.898 |     0.011 |     0.077 |     0.013 |     0.083 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  83.17858     d.f. =  9     p =  3.766849e-14 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |     21354 |       155 |      1065 |       225 |     22799 | 
##                                  |     0.937 |     0.007 |     0.047 |     0.010 |     0.554 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |     12721 |       117 |       815 |       148 |     13801 | 
##                                  |     0.922 |     0.008 |     0.059 |     0.011 |     0.335 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       963 |         3 |        45 |         9 |      1020 | 
##                                  |     0.944 |     0.003 |     0.044 |     0.009 |     0.025 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |      3185 |        42 |       292 |        48 |      3567 | 
##                                  |     0.893 |     0.012 |     0.082 |     0.013 |     0.087 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  108.1071     d.f. =  9     p =  3.569365e-19 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |     21095 |       160 |      1083 |       225 |     22563 | 
##                                     |     0.935 |     0.007 |     0.048 |     0.010 |     0.548 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |     12789 |       117 |       833 |       153 |     13892 | 
##                                     |     0.921 |     0.008 |     0.060 |     0.011 |     0.337 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      1006 |         4 |        46 |         9 |      1065 | 
##                                     |     0.945 |     0.004 |     0.043 |     0.008 |     0.026 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |      3265 |        45 |       303 |        54 |      3667 | 
##                                     |     0.890 |     0.012 |     0.083 |     0.015 |     0.089 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  108.5351     d.f. =  9     p =  2.921067e-19 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38770 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      2364 |      3124 |     13147 |      2613 |     21248 | 
##                      |     0.111 |     0.147 |     0.619 |     0.123 |     0.548 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      1820 |      1754 |      7568 |      1960 |     13102 | 
##                      |     0.139 |     0.134 |     0.578 |     0.150 |     0.338 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |        56 |        89 |       698 |       147 |       990 | 
##                      |     0.057 |     0.090 |     0.705 |     0.148 |     0.026 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |       174 |       345 |      2522 |       389 |      3430 | 
##                      |     0.051 |     0.101 |     0.735 |     0.113 |     0.088 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4414 |      5312 |     23935 |      5109 |     38770 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  465.9426     d.f. =  9     p =  1.117682e-94 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      2400 |      3812 |     14649 |      2804 |     23665 | 
##                           |     0.101 |     0.161 |     0.619 |     0.118 |     0.575 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      1820 |      1754 |      7568 |      1960 |     13102 | 
##                           |     0.139 |     0.134 |     0.578 |     0.150 |     0.318 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |        56 |        89 |       698 |       147 |       990 | 
##                           |     0.057 |     0.090 |     0.705 |     0.148 |     0.024 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |       174 |       345 |      2522 |       389 |      3430 | 
##                           |     0.051 |     0.101 |     0.735 |     0.113 |     0.083 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  569.8574     d.f. =  9     p =  6.142164e-117 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      2387 |      3576 |     14144 |      2692 |     22799 | 
##                                  |     0.105 |     0.157 |     0.620 |     0.118 |     0.554 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      1833 |      1965 |      7944 |      2059 |     13801 | 
##                                  |     0.133 |     0.142 |     0.576 |     0.149 |     0.335 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |        56 |        92 |       723 |       149 |      1020 | 
##                                  |     0.055 |     0.090 |     0.709 |     0.146 |     0.025 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |       174 |       367 |      2626 |       400 |      3567 | 
##                                  |     0.049 |     0.103 |     0.736 |     0.112 |     0.087 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  520.0016     d.f. =  9     p =  2.990348e-106 
## 
## 
##  
## 
## Cross-tabulation between SMK_CIG_STATUS and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      2382 |      3526 |     13954 |      2701 |     22563 | 
##                                     |     0.106 |     0.156 |     0.618 |     0.120 |     0.548 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      1837 |      1977 |      8047 |      2031 |     13892 | 
##                                     |     0.132 |     0.142 |     0.579 |     0.146 |     0.337 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |        57 |       105 |       745 |       158 |      1065 | 
##                                     |     0.054 |     0.099 |     0.700 |     0.148 |     0.026 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |       174 |       392 |      2691 |       410 |      3667 | 
##                                     |     0.047 |     0.107 |     0.734 |     0.112 |     0.089 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  486.4315     d.f. =  9     p =  4.616837e-99 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DEP_EVER 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  35352 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|
##                   -7 |      1700 |       287 |        38 |      2025 | 
##                      |     0.840 |     0.142 |     0.019 |     0.057 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    0 |      1889 |       399 |        38 |      2326 | 
##                      |     0.812 |     0.172 |     0.016 |     0.066 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    1 |      5416 |       919 |        81 |      6416 | 
##                      |     0.844 |     0.143 |     0.013 |     0.181 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    2 |      2335 |       340 |        23 |      2698 | 
##                      |     0.865 |     0.126 |     0.009 |     0.076 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    3 |      3837 |       500 |        33 |      4370 | 
##                      |     0.878 |     0.114 |     0.008 |     0.124 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    4 |      3394 |       439 |        39 |      3872 | 
##                      |     0.877 |     0.113 |     0.010 |     0.110 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    5 |      5680 |       704 |        51 |      6435 | 
##                      |     0.883 |     0.109 |     0.008 |     0.182 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    6 |      3274 |       373 |        26 |      3673 | 
##                      |     0.891 |     0.102 |     0.007 |     0.104 | 
## ---------------------|-----------|-----------|-----------|-----------|
##                    7 |      3107 |       399 |        31 |      3537 | 
##                      |     0.878 |     0.113 |     0.009 |     0.100 | 
## ---------------------|-----------|-----------|-----------|-----------|
##         Column Total |     30632 |      4360 |       360 |     35352 | 
## ---------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  161.2761     d.f. =  16     p =  4.587603e-26 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DEP_EVER 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|
##                        -7 |      1992 |       287 |        38 |      2317 | 
##                           |     0.860 |     0.124 |     0.016 |     0.056 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         0 |      2154 |       399 |        38 |      2591 | 
##                           |     0.831 |     0.154 |     0.015 |     0.063 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         1 |      7646 |      1098 |       134 |      8878 | 
##                           |     0.861 |     0.124 |     0.015 |     0.216 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         2 |      2675 |       340 |        23 |      3038 | 
##                           |     0.881 |     0.112 |     0.008 |     0.074 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         3 |      4344 |       500 |        33 |      4877 | 
##                           |     0.891 |     0.103 |     0.007 |     0.118 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         4 |      3830 |       439 |        39 |      4308 | 
##                           |     0.889 |     0.102 |     0.009 |     0.105 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         5 |      6419 |       704 |        51 |      7174 | 
##                           |     0.895 |     0.098 |     0.007 |     0.174 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         6 |      3703 |       373 |        26 |      4102 | 
##                           |     0.903 |     0.091 |     0.006 |     0.100 | 
## --------------------------|-----------|-----------|-----------|-----------|
##                         7 |      3472 |       399 |        31 |      3902 | 
##                           |     0.890 |     0.102 |     0.008 |     0.095 | 
## --------------------------|-----------|-----------|-----------|-----------|
##              Column Total |     36235 |      4539 |       413 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  170.2487     d.f. =  16     p =  7.510807e-28 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DEP_EVER 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                               -7 |      2148 |       344 |        66 |      2558 | 
##                                  |     0.840 |     0.134 |     0.026 |     0.062 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                0 |      2203 |       462 |        49 |      2714 | 
##                                  |     0.812 |     0.170 |     0.018 |     0.066 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                1 |      6331 |      1062 |       105 |      7498 | 
##                                  |     0.844 |     0.142 |     0.014 |     0.182 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                2 |      2740 |       378 |        57 |      3175 | 
##                                  |     0.863 |     0.119 |     0.018 |     0.077 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                3 |      4475 |       559 |        41 |      5075 | 
##                                  |     0.882 |     0.110 |     0.008 |     0.123 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                4 |      3889 |       480 |        46 |      4415 | 
##                                  |     0.881 |     0.109 |     0.010 |     0.107 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                5 |      6588 |       765 |        71 |      7424 | 
##                                  |     0.887 |     0.103 |     0.010 |     0.180 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                6 |      3824 |       413 |        34 |      4271 | 
##                                  |     0.895 |     0.097 |     0.008 |     0.104 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                                7 |      3574 |       442 |        41 |      4057 | 
##                                  |     0.881 |     0.109 |     0.010 |     0.099 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
##                     Column Total |     35772 |      4905 |       510 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  244.3736     d.f. =  16     p =  7.363602e-43 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DEP_EVER 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         0 |         1 |         2 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                  -7 |      2057 |       341 |        47 |      2445 | 
##                                     |     0.841 |     0.139 |     0.019 |     0.059 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   0 |      2184 |       477 |        43 |      2704 | 
##                                     |     0.808 |     0.176 |     0.016 |     0.066 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   1 |      6327 |      1109 |       109 |      7545 | 
##                                     |     0.839 |     0.147 |     0.014 |     0.183 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   2 |      2746 |       413 |        34 |      3193 | 
##                                     |     0.860 |     0.129 |     0.011 |     0.078 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   3 |      4450 |       587 |        41 |      5078 | 
##                                     |     0.876 |     0.116 |     0.008 |     0.123 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   4 |      3895 |       538 |        47 |      4480 | 
##                                     |     0.869 |     0.120 |     0.010 |     0.109 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   5 |      6537 |       834 |        59 |      7430 | 
##                                     |     0.880 |     0.112 |     0.008 |     0.180 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   6 |      3791 |       443 |        34 |      4268 | 
##                                     |     0.888 |     0.104 |     0.008 |     0.104 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                                   7 |      3529 |       479 |        36 |      4044 | 
##                                     |     0.873 |     0.118 |     0.009 |     0.098 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
##                        Column Total |     35516 |      5221 |       450 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  187.4895     d.f. =  16     p =  2.640468e-31 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DIAB_TYPE 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  38448 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                   -7 |      1913 |        23 |       201 |        45 |      2182 | 
##                      |     0.877 |     0.011 |     0.092 |     0.021 |     0.057 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      2235 |        30 |       209 |        41 |      2515 | 
##                      |     0.889 |     0.012 |     0.083 |     0.016 |     0.065 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      6370 |        67 |       462 |       100 |      6999 | 
##                      |     0.910 |     0.010 |     0.066 |     0.014 |     0.182 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |      2746 |        17 |       142 |        30 |      2935 | 
##                      |     0.936 |     0.006 |     0.048 |     0.010 |     0.076 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |      4453 |        40 |       233 |        53 |      4779 | 
##                      |     0.932 |     0.008 |     0.049 |     0.011 |     0.124 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    4 |      3967 |        28 |       175 |        32 |      4202 | 
##                      |     0.944 |     0.007 |     0.042 |     0.008 |     0.109 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    5 |      6651 |        43 |       277 |        51 |      7022 | 
##                      |     0.947 |     0.006 |     0.039 |     0.007 |     0.183 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    6 |      3788 |        18 |       166 |        28 |      4000 | 
##                      |     0.947 |     0.004 |     0.042 |     0.007 |     0.104 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    7 |      3577 |        28 |       176 |        33 |      3814 | 
##                      |     0.938 |     0.007 |     0.046 |     0.009 |     0.099 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     35700 |       294 |      2041 |       413 |     38448 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  272.9416     d.f. =  24     p =  4.487085e-44 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DIAB_TYPE 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                        -7 |      2048 |        23 |       201 |        45 |      2317 | 
##                           |     0.884 |     0.010 |     0.087 |     0.019 |     0.056 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      2311 |        30 |       209 |        41 |      2591 | 
##                           |     0.892 |     0.012 |     0.081 |     0.016 |     0.063 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      8097 |        88 |       581 |       112 |      8878 | 
##                           |     0.912 |     0.010 |     0.065 |     0.013 |     0.216 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |      2849 |        17 |       142 |        30 |      3038 | 
##                           |     0.938 |     0.006 |     0.047 |     0.010 |     0.074 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |      4551 |        40 |       233 |        53 |      4877 | 
##                           |     0.933 |     0.008 |     0.048 |     0.011 |     0.118 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         4 |      4073 |        28 |       175 |        32 |      4308 | 
##                           |     0.945 |     0.006 |     0.041 |     0.007 |     0.105 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         5 |      6803 |        43 |       277 |        51 |      7174 | 
##                           |     0.948 |     0.006 |     0.039 |     0.007 |     0.174 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         6 |      3890 |        18 |       166 |        28 |      4102 | 
##                           |     0.948 |     0.004 |     0.040 |     0.007 |     0.100 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         7 |      3665 |        28 |       176 |        33 |      3902 | 
##                           |     0.939 |     0.007 |     0.045 |     0.008 |     0.095 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  266.4402     d.f. =  24     p =  8.901444e-43 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DIAB_TYPE 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                               -7 |      2240 |        26 |       245 |        47 |      2558 | 
##                                  |     0.876 |     0.010 |     0.096 |     0.018 |     0.062 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      2411 |        31 |       228 |        44 |      2714 | 
##                                  |     0.888 |     0.011 |     0.084 |     0.016 |     0.066 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      6816 |        69 |       510 |       103 |      7498 | 
##                                  |     0.909 |     0.009 |     0.068 |     0.014 |     0.182 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |      2971 |        20 |       149 |        35 |      3175 | 
##                                  |     0.936 |     0.006 |     0.047 |     0.011 |     0.077 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |      4735 |        41 |       245 |        54 |      5075 | 
##                                  |     0.933 |     0.008 |     0.048 |     0.011 |     0.123 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                4 |      4173 |        30 |       180 |        32 |      4415 | 
##                                  |     0.945 |     0.007 |     0.041 |     0.007 |     0.107 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                5 |      7028 |        50 |       293 |        53 |      7424 | 
##                                  |     0.947 |     0.007 |     0.039 |     0.007 |     0.180 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                6 |      4044 |        19 |       179 |        29 |      4271 | 
##                                  |     0.947 |     0.004 |     0.042 |     0.007 |     0.104 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                7 |      3805 |        31 |       188 |        33 |      4057 | 
##                                  |     0.938 |     0.008 |     0.046 |     0.008 |     0.099 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  311.7154     d.f. =  24     p =  7.282467e-52 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and DIS_DIAB_TYPE 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                  -7 |      2129 |        27 |       239 |        50 |      2445 | 
##                                     |     0.871 |     0.011 |     0.098 |     0.020 |     0.059 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      2395 |        34 |       232 |        43 |      2704 | 
##                                     |     0.886 |     0.013 |     0.086 |     0.016 |     0.066 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      6849 |        76 |       513 |       107 |      7545 | 
##                                     |     0.908 |     0.010 |     0.068 |     0.014 |     0.183 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |      2984 |        19 |       160 |        30 |      3193 | 
##                                     |     0.935 |     0.006 |     0.050 |     0.009 |     0.078 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |      4723 |        44 |       255 |        56 |      5078 | 
##                                     |     0.930 |     0.009 |     0.050 |     0.011 |     0.123 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |      4218 |        32 |       196 |        34 |      4480 | 
##                                     |     0.942 |     0.007 |     0.044 |     0.008 |     0.109 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |      7038 |        44 |       294 |        54 |      7430 | 
##                                     |     0.947 |     0.006 |     0.040 |     0.007 |     0.180 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   6 |      4028 |        18 |       188 |        34 |      4268 | 
##                                     |     0.944 |     0.004 |     0.044 |     0.008 |     0.104 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   7 |      3791 |        32 |       188 |        33 |      4044 | 
##                                     |     0.937 |     0.008 |     0.046 |     0.008 |     0.098 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  317.8302     d.f. =  24     p =  4.233082e-53 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39504 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                   -7 |       158 |       272 |      1676 |       211 |      2317 | 
##                      |     0.068 |     0.117 |     0.723 |     0.091 |     0.059 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |       315 |       432 |      1528 |       316 |      2591 | 
##                      |     0.122 |     0.167 |     0.590 |     0.122 |     0.066 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       629 |       950 |      4534 |      1082 |      7195 | 
##                      |     0.087 |     0.132 |     0.630 |     0.150 |     0.182 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       275 |       444 |      1872 |       447 |      3038 | 
##                      |     0.091 |     0.146 |     0.616 |     0.147 |     0.077 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |       473 |       818 |      2883 |       703 |      4877 | 
##                      |     0.097 |     0.168 |     0.591 |     0.144 |     0.123 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    4 |       463 |       589 |      2656 |       600 |      4308 | 
##                      |     0.107 |     0.137 |     0.617 |     0.139 |     0.109 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    5 |       902 |      1206 |      4080 |       986 |      7174 | 
##                      |     0.126 |     0.168 |     0.569 |     0.137 |     0.182 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    6 |       586 |       678 |      2371 |       467 |      4102 | 
##                      |     0.143 |     0.165 |     0.578 |     0.114 |     0.104 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    7 |       604 |       579 |      2385 |       334 |      3902 | 
##                      |     0.155 |     0.148 |     0.611 |     0.086 |     0.099 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4405 |      5968 |     23985 |      5146 |     39504 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  513.1458     d.f. =  24     p =  3.096828e-93 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                        -7 |       158 |       272 |      1676 |       211 |      2317 | 
##                           |     0.068 |     0.117 |     0.723 |     0.091 |     0.056 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |       315 |       432 |      1528 |       316 |      2591 | 
##                           |     0.122 |     0.167 |     0.590 |     0.122 |     0.063 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       674 |       982 |      5986 |      1236 |      8878 | 
##                           |     0.076 |     0.111 |     0.674 |     0.139 |     0.216 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       275 |       444 |      1872 |       447 |      3038 | 
##                           |     0.091 |     0.146 |     0.616 |     0.147 |     0.074 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |       473 |       818 |      2883 |       703 |      4877 | 
##                           |     0.097 |     0.168 |     0.591 |     0.144 |     0.118 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         4 |       463 |       589 |      2656 |       600 |      4308 | 
##                           |     0.107 |     0.137 |     0.617 |     0.139 |     0.105 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         5 |       902 |      1206 |      4080 |       986 |      7174 | 
##                           |     0.126 |     0.168 |     0.569 |     0.137 |     0.174 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         6 |       586 |       678 |      2371 |       467 |      4102 | 
##                           |     0.143 |     0.165 |     0.578 |     0.114 |     0.100 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         7 |       604 |       579 |      2385 |       334 |      3902 | 
##                           |     0.155 |     0.148 |     0.611 |     0.086 |     0.095 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  690.9361     d.f. =  24     p =  1.997459e-130 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                               -7 |       165 |       273 |      1904 |       216 |      2558 | 
##                                  |     0.065 |     0.107 |     0.744 |     0.084 |     0.062 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |       319 |       435 |      1638 |       322 |      2714 | 
##                                  |     0.118 |     0.160 |     0.604 |     0.119 |     0.066 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       636 |       954 |      4789 |      1119 |      7498 | 
##                                  |     0.085 |     0.127 |     0.639 |     0.149 |     0.182 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       276 |       447 |      1995 |       457 |      3175 | 
##                                  |     0.087 |     0.141 |     0.628 |     0.144 |     0.077 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |       477 |       824 |      3048 |       726 |      5075 | 
##                                  |     0.094 |     0.162 |     0.601 |     0.143 |     0.123 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                4 |       464 |       592 |      2749 |       610 |      4415 | 
##                                  |     0.105 |     0.134 |     0.623 |     0.138 |     0.107 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                5 |       913 |      1214 |      4291 |      1006 |      7424 | 
##                                  |     0.123 |     0.164 |     0.578 |     0.136 |     0.180 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                6 |       590 |       681 |      2501 |       499 |      4271 | 
##                                  |     0.138 |     0.159 |     0.586 |     0.117 |     0.104 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                7 |       610 |       580 |      2522 |       345 |      4057 | 
##                                  |     0.150 |     0.143 |     0.622 |     0.085 |     0.099 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  562.1215     d.f. =  24     p =  1.948869e-103 
## 
## 
##  
## 
## Cross-tabulation between ALC_CUR_FREQ and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                  -7 |       159 |       274 |      1793 |       219 |      2445 | 
##                                     |     0.065 |     0.112 |     0.733 |     0.090 |     0.059 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |       318 |       434 |      1627 |       325 |      2704 | 
##                                     |     0.118 |     0.161 |     0.602 |     0.120 |     0.066 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       634 |       956 |      4835 |      1120 |      7545 | 
##                                     |     0.084 |     0.127 |     0.641 |     0.148 |     0.183 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       280 |       448 |      1999 |       466 |      3193 | 
##                                     |     0.088 |     0.140 |     0.626 |     0.146 |     0.078 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |       480 |       822 |      3054 |       722 |      5078 | 
##                                     |     0.095 |     0.162 |     0.601 |     0.142 |     0.123 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   4 |       468 |       593 |      2802 |       617 |      4480 | 
##                                     |     0.104 |     0.132 |     0.625 |     0.138 |     0.109 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   5 |       908 |      1209 |      4304 |      1009 |      7430 | 
##                                     |     0.122 |     0.163 |     0.579 |     0.136 |     0.180 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   6 |       594 |       681 |      2510 |       483 |      4268 | 
##                                     |     0.139 |     0.160 |     0.588 |     0.113 |     0.104 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   7 |       609 |       583 |      2513 |       339 |      4044 | 
##                                     |     0.151 |     0.144 |     0.621 |     0.084 |     0.098 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  535.5776     d.f. =  24     p =  6.660611e-98 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and DIS_DIAB_TYPE 
##  For Orginal data
```

```
## Warning in chisq.test(t, correct = FALSE, ...): Chi-squared approximation may
## be incorrect
```

```
## 
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  35781 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |     29007 |       226 |      1543 |       279 |     31055 | 
##                      |     0.934 |     0.007 |     0.050 |     0.009 |     0.868 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |      3932 |        57 |       380 |        70 |      4439 | 
##                      |     0.886 |     0.013 |     0.086 |     0.016 |     0.124 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       252 |         3 |        21 |        11 |       287 | 
##                      |     0.878 |     0.010 |     0.073 |     0.038 |     0.008 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |     33191 |       286 |      1944 |       360 |     35781 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  160.6447     d.f. =  6     p =  4.324187e-32 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and DIS_DIAB_TYPE 
##  For Median Imputation
```

```
## Warning in chisq.test(t, correct = FALSE, ...): Chi-squared approximation may
## be incorrect
```

```
## 
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |     33877 |       255 |      1759 |       344 |     36235 | 
##                           |     0.935 |     0.007 |     0.049 |     0.009 |     0.880 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |      4032 |        57 |       380 |        70 |      4539 | 
##                           |     0.888 |     0.013 |     0.084 |     0.015 |     0.110 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       378 |         3 |        21 |        11 |       413 | 
##                           |     0.915 |     0.007 |     0.051 |     0.027 |     0.010 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |     38287 |       315 |      2160 |       425 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  145.2906     d.f. =  6     p =  7.654143e-29 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and DIS_DIAB_TYPE 
##  For KNN Imputation
```

```
## Warning in chisq.test(t, correct = FALSE, ...): Chi-squared approximation may
## be incorrect
```

```
## 
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |     33403 |       251 |      1777 |       341 |     35772 | 
##                                  |     0.934 |     0.007 |     0.050 |     0.010 |     0.869 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |      4353 |        62 |       415 |        75 |      4905 | 
##                                  |     0.887 |     0.013 |     0.085 |     0.015 |     0.119 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       467 |         4 |        25 |        14 |       510 | 
##                                  |     0.916 |     0.008 |     0.049 |     0.027 |     0.012 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |     38223 |       317 |      2217 |       430 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  153.7964     d.f. =  6     p =  1.217958e-30 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and DIS_DIAB_TYPE 
##  For MICE Imputation
```

```
## Warning in chisq.test(t, correct = FALSE, ...): Chi-squared approximation may
## be incorrect
```

```
## 
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |        -7 |         1 |         2 |         3 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |     33131 |       262 |      1784 |       339 |     35516 | 
##                                     |     0.933 |     0.007 |     0.050 |     0.010 |     0.862 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |      4625 |        61 |       446 |        89 |      5221 | 
##                                     |     0.886 |     0.012 |     0.085 |     0.017 |     0.127 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       399 |         3 |        35 |        13 |       450 | 
##                                     |     0.887 |     0.007 |     0.078 |     0.029 |     0.011 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |     38155 |       326 |      2265 |       441 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  167.1681     d.f. =  6     p =  1.792698e-33 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  36482 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    0 |      2935 |      4607 |     20470 |      3518 |     31530 | 
##                      |     0.093 |     0.146 |     0.649 |     0.112 |     0.864 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |       478 |       728 |      2891 |       442 |      4539 | 
##                      |     0.105 |     0.160 |     0.637 |     0.097 |     0.124 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |         0 |         0 |       413 |         0 |       413 | 
##                      |     0.000 |     0.000 |     1.000 |     0.000 |     0.011 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      3413 |      5335 |     23774 |      3960 |     36482 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  243.4442     d.f. =  6     p =  1.03182e-49 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         0 |      3972 |      5272 |     22133 |      4858 |     36235 | 
##                           |     0.110 |     0.145 |     0.611 |     0.134 |     0.880 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |       478 |       728 |      2891 |       442 |      4539 | 
##                           |     0.105 |     0.160 |     0.637 |     0.097 |     0.110 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |         0 |         0 |       413 |         0 |       413 | 
##                           |     0.000 |     0.000 |     1.000 |     0.000 |     0.010 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  311.7957     d.f. =  6     p =  2.424689e-64 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                0 |      3886 |      5215 |     21885 |      4786 |     35772 | 
##                                  |     0.109 |     0.146 |     0.612 |     0.134 |     0.869 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |       562 |       785 |      3047 |       511 |      4905 | 
##                                  |     0.115 |     0.160 |     0.621 |     0.104 |     0.119 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |         2 |         0 |       505 |         3 |       510 | 
##                                  |     0.004 |     0.000 |     0.990 |     0.006 |     0.012 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  341.0792     d.f. =  6     p =  1.268522e-70 
## 
## 
##  
## 
## Cross-tabulation between DIS_DEP_EVER and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   0 |      3801 |      5151 |     21883 |      4681 |     35516 | 
##                                     |     0.107 |     0.145 |     0.616 |     0.132 |     0.862 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |       648 |       849 |      3105 |       619 |      5221 | 
##                                     |     0.124 |     0.163 |     0.595 |     0.119 |     0.127 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |         1 |         0 |       449 |         0 |       450 | 
##                                     |     0.002 |     0.000 |     0.998 |     0.000 |     0.011 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  310.0074     d.f. =  6     p =  5.86137e-64 
## 
## 
##  
## 
## Cross-tabulation between DIS_DIAB_TYPE and ADM_STUDY_ID 
##  For Orginal data
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  39707 
## 
##  
##                      | data[[var_names[j]]] 
## data[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                   -7 |      4036 |      5529 |     22424 |      4818 |     36807 | 
##                      |     0.110 |     0.150 |     0.609 |     0.131 |     0.927 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    1 |        30 |        40 |       197 |        48 |       315 | 
##                      |     0.095 |     0.127 |     0.625 |     0.152 |     0.008 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    2 |       188 |       333 |      1324 |       315 |      2160 | 
##                      |     0.087 |     0.154 |     0.613 |     0.146 |     0.054 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##                    3 |        78 |        74 |       213 |        60 |       425 | 
##                      |     0.184 |     0.174 |     0.501 |     0.141 |     0.011 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
##         Column Total |      4332 |      5976 |     24158 |      5241 |     39707 | 
## ---------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  47.84937     d.f. =  9     p =  2.725043e-07 
## 
## 
##  
## 
## Cross-tabulation between DIS_DIAB_TYPE and ADM_STUDY_ID 
##  For Median Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                           | data_mean[[var_names[j]]] 
## data_mean[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                        -7 |      4154 |      5553 |     23703 |      4877 |     38287 | 
##                           |     0.108 |     0.145 |     0.619 |     0.127 |     0.930 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         1 |        30 |        40 |       197 |        48 |       315 | 
##                           |     0.095 |     0.127 |     0.625 |     0.152 |     0.008 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         2 |       188 |       333 |      1324 |       315 |      2160 | 
##                           |     0.087 |     0.154 |     0.613 |     0.146 |     0.052 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##                         3 |        78 |        74 |       213 |        60 |       425 | 
##                           |     0.184 |     0.174 |     0.501 |     0.141 |     0.010 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
##              Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## --------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  52.98209     d.f. =  9     p =  2.94585e-08 
## 
## 
##  
## 
## Cross-tabulation between DIS_DIAB_TYPE and ADM_STUDY_ID 
##  For KNN Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                  | imputed_data_KNN[[var_names[j]]] 
## imputed_data_KNN[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                               -7 |      4151 |      5553 |     23643 |      4876 |     38223 | 
##                                  |     0.109 |     0.145 |     0.619 |     0.128 |     0.928 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                1 |        31 |        40 |       198 |        48 |       317 | 
##                                  |     0.098 |     0.126 |     0.625 |     0.151 |     0.008 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                2 |       189 |       333 |      1379 |       316 |      2217 | 
##                                  |     0.085 |     0.150 |     0.622 |     0.143 |     0.054 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                3 |        79 |        74 |       217 |        60 |       430 | 
##                                  |     0.184 |     0.172 |     0.505 |     0.140 |     0.010 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
##                     Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ---------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  51.48747     d.f. =  9     p =  5.649627e-08 
## 
## 
##  
## 
## Cross-tabulation between DIS_DIAB_TYPE and ADM_STUDY_ID 
##  For MICE Imputation
##  
##    Cell Contents
## |-------------------------|
## |                       N |
## |           N / Row Total |
## |-------------------------|
## 
##  
## Total Observations in Table:  41187 
## 
##  
##                                     | imputed_data_mice_c[[var_names[j]]] 
## imputed_data_mice_c[[var_names[i]]] |         1 |         2 |         3 |         5 | Row Total | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                  -7 |      4139 |      5552 |     23595 |      4869 |     38155 | 
##                                     |     0.108 |     0.146 |     0.618 |     0.128 |     0.926 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   1 |        30 |        41 |       206 |        49 |       326 | 
##                                     |     0.092 |     0.126 |     0.632 |     0.150 |     0.008 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   2 |       198 |       333 |      1413 |       321 |      2265 | 
##                                     |     0.087 |     0.147 |     0.624 |     0.142 |     0.055 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                                   3 |        83 |        74 |       223 |        61 |       441 | 
##                                     |     0.188 |     0.168 |     0.506 |     0.138 |     0.011 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
##                        Column Total |      4450 |      6000 |     25437 |      5300 |     41187 | 
## ------------------------------------|-----------|-----------|-----------|-----------|-----------|
## 
##  
## Statistics for All Table Factors
## 
## 
## Pearson's Chi-squared test 
## ------------------------------------------------------------
## Chi^2 =  52.46714     d.f. =  9     p =  3.687879e-08 
## 
## 
## 
```
- Visual comparisons of distributions before and after imputation.


``` r
# variables<-data %>%
#   select(where(is.numeric)) %>%
#   names()
variables<-c("PM_BMI_SR",  "PA_TOTAL_SHORT" , "PA_TOTAL_SIT_TIME" )
  # Load the ggplot2 package

# Loop through each variable

 data_rename <- data %>%
  rename_with(~ paste0(. , "_ori"), -ID)
 data_mean_rename <- data_mean %>%
  rename_with(~ paste0(. , "_mean"), -ID)
 imputed_data_KNN_rename <- imputed_data_KNN %>%
  rename_with(~ paste0(. , "_KNN"), -ID)
 imputed_data_mice_c_rename <- imputed_data_mice_c %>%
  rename_with(~ paste0(. , "_mice"), -ID)
# 
# # Load the ggplot2 package
# library(ggplot2)

# List of variables to plot
# variables <- c("PA_TOTAL_SHORT", "SDC_GENDER")

# Loop through each variable
combined_data <- data_rename %>%
  full_join(data_mean_rename, by = "ID") %>%
  full_join(imputed_data_KNN_rename, by = "ID") %>%
  full_join(imputed_data_mice_c_rename, by = "ID")
# for (var in variables) {
#   # Create the density plot
#   density_imp <- ggplot(combined_data) +
#     geom_density(aes(x = .combined_data[[paste0(var, "_ori")]], colour = "Original")) +
#     geom_density(aes(x = .combined_data[[paste0(var, "_mean")]], colour = "Mean Imputation")) +
#     geom_density(aes(x = .combined_data[[paste0(var, "_KNN")]], colour = "KNN Imputation")) +
#     geom_density(aes(x = .combined_data[[paste0(var, "_mice")]], colour = "MICE Imputation")) +
#     labs(
#       title = paste("Density Plot for", var),
#       x = var,
#       y = "Density",
#       colour = "Imputation Method"
#     ) 
# 
#   # Display the plot
#   print(density_imp)
# }

density_bmi <- ggplot(combined_data) +
                geom_density(aes(PM_BMI_SR_ori, colour= "Original")) +
                geom_density(aes(PM_BMI_SR_mean, colour= "Mean Imputation")) +
                geom_density(aes(PM_BMI_SR_KNN, colour= "KNN Imputation")) +
                geom_density(aes(PM_BMI_SR_mice, colour= "MICE Imputation"))+
  labs(
    title = "Density Plot for BMI",  # Dynamic title using the variable name
    # subtitle = "Comparison of Imputation Methods",  # Optional subtitle
    # caption = "Data source: Your Dataset",  # Optional caption
    x = "BMI",  # X-axis label
    y = "Density",  # Y-axis label
    colour = "Imputation Method"  # Legend title
  )+
  theme(
  plot.title = element_text(size = 16, face = "bold", hjust = 0.5),  # Center and bold the title
  plot.subtitle = element_text(size = 12, hjust = 0.5),  # Center the subtitle
  plot.caption = element_text(size = 10, face = "italic")  # Italicize the caption
)
        
plot(density_bmi)
```

```
## Warning: Removed 11976 rows containing non-finite outside the scale range
## (`stat_density()`).
```

![](Missing-Data_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

``` r
density_short <- ggplot(combined_data) +
                geom_density(aes(PA_TOTAL_SHORT_ori, colour= "Original")) +
                geom_density(aes(PA_TOTAL_SHORT_mean, colour= "Mean Imputation")) +
                geom_density(aes(PA_TOTAL_SHORT_KNN, colour= "KNN Imputation")) +
                geom_density(aes(PA_TOTAL_SHORT_mice, colour= "MICE Imputation"))+
    labs(
    title = "Density Plot for Physical Activity",  # Dynamic title using the variable name
    # subtitle = "Comparison of Imputation Methods",  # Optional subtitle
    # caption = "Data source: Your Dataset",  # Optional caption
    x = "Physical Activity",  # X-axis label
    y = "Density",  # Y-axis label
    colour = "Imputation Method"  # Legend title
  )+
  theme(
  plot.title = element_text(size = 16, face = "bold", hjust = 0.5),  # Center and bold the title
  plot.subtitle = element_text(size = 12, hjust = 0.5),  # Center the subtitle
  plot.caption = element_text(size = 10, face = "italic")  # Italicize the caption
)
plot(density_short)
```

```
## Warning: Removed 6763 rows containing non-finite outside the scale range
## (`stat_density()`).
```

![](Missing-Data_files/figure-html/unnamed-chunk-16-2.png)<!-- -->

``` r
density_sit <- ggplot(combined_data) +
                geom_density(aes(PA_TOTAL_SIT_TIME_ori, colour= "Original")) +
                geom_density(aes(PA_TOTAL_SIT_TIME_mean, colour= "Mean Imputation")) +
                geom_density(aes(PA_TOTAL_SIT_TIME_KNN, colour= "KNN Imputation")) +
                geom_density(aes(PA_TOTAL_SIT_TIME_mice, colour= "MICE Imputation")) +
      labs(
    title = "Density Plot for sitting time",  # Dynamic title using the variable name
    # subtitle = "Comparison of Imputation Methods",  # Optional subtitle
    # caption = "Data source: Your Dataset",  # Optional caption
    x = "Sitting time",  # X-axis label
    y = "Density",  # Y-axis label
    colour = "Imputation Method"  # Legend title
  )+
  theme(
  plot.title = element_text(size = 16, face = "bold", hjust = 0.5),  # Center and bold the title
  plot.subtitle = element_text(size = 12, hjust = 0.5),  # Center the subtitle
  plot.caption = element_text(size = 10, face = "italic")  # Italicize the caption
)
plot(density_sit)
```

```
## Warning: Removed 11272 rows containing non-finite outside the scale range
## (`stat_density()`).
```

![](Missing-Data_files/figure-html/unnamed-chunk-16-3.png)<!-- -->

  
4. **Analysis of Imputed Data**
   - Conduct a simple statistical analysis on the imputed datasets to illustrate the downstream effects of different imputation methods.

``` r
data_ori<-data %>%
  mutate(source="Original")
data_mean_source<-data_mean %>%
  mutate(source="Meean")
imputed_data_KNN_source<-imputed_data_KNN%>%
  select(-c(ID_imp , PM_BMI_SR_imp, PA_TOTAL_SHORT_imp, PA_TOTAL_SIT_TIME_imp, SDC_EB_ABORIGINAL_imp, SDC_AGE_CALC_imp, SDC_GENDER_imp, WRK_EMPLOYMENT_imp, HS_GEN_HEALTH_imp, NUT_VEG_QTY_imp, NUT_FRUITS_QTY_imp, SMK_CIG_STATUS_imp, ALC_CUR_FREQ_imp, DIS_DEP_EVER_imp, DIS_DIAB_TYPE_imp, ADM_STUDY_ID_imp)) %>%
  mutate(source="KNN")
imputed_data_mice_c_source<-imputed_data_mice_c %>%
  mutate(source="MICE")
combine_long<-rbind(data_ori,data_mean_source, imputed_data_KNN_source, imputed_data_mice_c_source )
```

``` r
median_table <- combine_long %>%
   group_by(source) %>%
   summarize(
    BMI = median(PM_BMI_SR, na.rm = TRUE),
    SHORT = mean(PA_TOTAL_SHORT, na.rm = TRUE),
    sit_time = median(PA_TOTAL_SIT_TIME, na.rm = TRUE)
  )
print(median_table)
```

```
## # A tibble: 4 × 4
##   source     BMI SHORT sit_time
##   <chr>    <dbl> <dbl>    <dbl>
## 1 KNN       26.6 2479.    2520 
## 2 MICE      26.6 2588.    2520 
## 3 Meean     27.5 2574.    2661.
## 4 Original  26.6 2574.    2520
```

   
   - Discuss how the choice of imputation method impacts the analysis results.

``` r
 library(broom)
 model_original <- data %>% 
   with(lm(PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT +
                  PA_TOTAL_SIT_TIME + SDC_EB_ABORIGINAL +
                  SDC_AGE_CALC + SDC_GENDER+ 
                  WRK_EMPLOYMENT + HS_GEN_HEALTH +
                  NUT_VEG_QTY + NUT_FRUITS_QTY +
                  SMK_CIG_STATUS + ALC_CUR_FREQ +
                  DIS_DEP_EVER + DIS_DIAB_TYPE +
                  ADM_STUDY_ID))
summary(model_original)
```

```
## 
## Call:
## lm(formula = PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT + PA_TOTAL_SIT_TIME + 
##     SDC_EB_ABORIGINAL + SDC_AGE_CALC + SDC_GENDER + WRK_EMPLOYMENT + 
##     HS_GEN_HEALTH + NUT_VEG_QTY + NUT_FRUITS_QTY + SMK_CIG_STATUS + 
##     ALC_CUR_FREQ + DIS_DEP_EVER + DIS_DIAB_TYPE + ADM_STUDY_ID)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -20.415  -3.685  -0.764   2.735  39.744 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)         2.739e+01  5.115e-01  53.556  < 2e-16 ***
## PA_TOTAL_SHORT     -1.028e-04  1.691e-05  -6.077 1.25e-09 ***
## PA_TOTAL_SIT_TIME   1.756e-04  3.650e-05   4.811 1.51e-06 ***
## SDC_EB_ABORIGINAL1  4.410e-01  2.300e-01   1.917 0.055192 .  
## SDC_AGE_CALC        3.431e-02  4.436e-03   7.734 1.09e-14 ***
## SDC_GENDER2        -1.214e+00  8.885e-02 -13.663  < 2e-16 ***
## WRK_EMPLOYMENT1     1.948e-02  1.023e-01   0.190 0.848981    
## HS_GEN_HEALTH2      1.825e-01  3.694e-01   0.494 0.621381    
## HS_GEN_HEALTH3     -9.134e-01  3.459e-01  -2.640 0.008287 ** 
## HS_GEN_HEALTH4     -3.066e+00  3.459e-01  -8.863  < 2e-16 ***
## HS_GEN_HEALTH5     -3.874e+00  3.559e-01 -10.886  < 2e-16 ***
## NUT_VEG_QTY         1.075e-02  2.958e-02   0.364 0.716225    
## NUT_FRUITS_QTY     -6.525e-02  3.467e-02  -1.882 0.059848 .  
## SMK_CIG_STATUS1     3.433e-01  9.244e-02   3.714 0.000205 ***
## SMK_CIG_STATUS2     7.677e-01  2.711e-01   2.832 0.004634 ** 
## SMK_CIG_STATUS3     2.488e-01  1.688e-01   1.474 0.140400    
## ALC_CUR_FREQ0       4.072e-01  2.531e-01   1.609 0.107708    
## ALC_CUR_FREQ1       1.616e-01  2.153e-01   0.751 0.452805    
## ALC_CUR_FREQ2       2.668e-01  2.415e-01   1.105 0.269231    
## ALC_CUR_FREQ3       1.563e-01  2.233e-01   0.700 0.483945    
## ALC_CUR_FREQ4      -5.889e-01  2.273e-01  -2.591 0.009589 ** 
## ALC_CUR_FREQ5      -2.988e-01  2.137e-01  -1.398 0.162192    
## ALC_CUR_FREQ6      -5.661e-01  2.305e-01  -2.456 0.014067 *  
## ALC_CUR_FREQ7      -4.715e-01  2.315e-01  -2.037 0.041662 *  
## DIS_DEP_EVER1       2.395e-01  1.378e-01   1.738 0.082200 .  
## DIS_DEP_EVER2       7.387e-01  5.110e-01   1.446 0.148307    
## DIS_DIAB_TYPE1      6.261e-01  5.107e-01   1.226 0.220219    
## DIS_DIAB_TYPE2      1.270e+00  1.997e-01   6.362 2.03e-10 ***
## DIS_DIAB_TYPE3      1.679e+00  4.442e-01   3.781 0.000157 ***
## ADM_STUDY_ID2       1.966e+00  1.617e-01  12.157  < 2e-16 ***
## ADM_STUDY_ID3       7.469e-01  1.366e-01   5.469 4.58e-08 ***
## ADM_STUDY_ID5       2.826e+00  2.030e-01  13.921  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.684 on 18666 degrees of freedom
##   (22489 observations deleted due to missingness)
## Multiple R-squared:  0.1024,	Adjusted R-squared:  0.1009 
## F-statistic: 68.67 on 31 and 18666 DF,  p-value: < 2.2e-16
```

``` r
  model_mean <- data_mean %>% 
   with(lm(PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT +
                  PA_TOTAL_SIT_TIME + SDC_EB_ABORIGINAL +
                  SDC_AGE_CALC + SDC_GENDER+ 
                  WRK_EMPLOYMENT + HS_GEN_HEALTH +
                  NUT_VEG_QTY + NUT_FRUITS_QTY +
                  SMK_CIG_STATUS + ALC_CUR_FREQ +
                  DIS_DEP_EVER + DIS_DIAB_TYPE +
                  ADM_STUDY_ID))
 summary(model_mean)
```

```
## 
## Call:
## lm(formula = PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT + PA_TOTAL_SIT_TIME + 
##     SDC_EB_ABORIGINAL + SDC_AGE_CALC + SDC_GENDER + WRK_EMPLOYMENT + 
##     HS_GEN_HEALTH + NUT_VEG_QTY + NUT_FRUITS_QTY + SMK_CIG_STATUS + 
##     ALC_CUR_FREQ + DIS_DEP_EVER + DIS_DIAB_TYPE + ADM_STUDY_ID)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -19.432  -2.744  -0.363   1.703  40.735 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)         2.816e+01  2.872e-01  98.077  < 2e-16 ***
## PA_TOTAL_SHORT     -7.199e-05  1.065e-05  -6.759 1.41e-11 ***
## PA_TOTAL_SIT_TIME   1.261e-04  2.481e-05   5.080 3.80e-07 ***
## SDC_EB_ABORIGINAL1  2.843e-01  1.353e-01   2.101 0.035668 *  
## SDC_AGE_CALC        2.173e-02  2.565e-03   8.468  < 2e-16 ***
## SDC_GENDER2        -8.850e-01  5.364e-02 -16.499  < 2e-16 ***
## WRK_EMPLOYMENT1    -1.221e-02  5.896e-02  -0.207 0.835958    
## HS_GEN_HEALTH2     -2.515e-01  1.968e-01  -1.278 0.201400    
## HS_GEN_HEALTH3     -9.802e-01  1.834e-01  -5.345 9.07e-08 ***
## HS_GEN_HEALTH4     -2.522e+00  1.833e-01 -13.761  < 2e-16 ***
## HS_GEN_HEALTH5     -3.038e+00  1.901e-01 -15.985  < 2e-16 ***
## NUT_VEG_QTY         1.806e-02  1.729e-02   1.045 0.296172    
## NUT_FRUITS_QTY     -5.177e-02  2.026e-02  -2.555 0.010612 *  
## SMK_CIG_STATUS1     2.328e-01  5.560e-02   4.186 2.84e-05 ***
## SMK_CIG_STATUS2     3.144e-01  1.630e-01   1.929 0.053771 .  
## SMK_CIG_STATUS3     2.049e-02  9.312e-02   0.220 0.825810    
## ALC_CUR_FREQ0       2.751e-01  1.436e-01   1.916 0.055425 .  
## ALC_CUR_FREQ1       1.308e-01  1.171e-01   1.117 0.264102    
## ALC_CUR_FREQ2       1.445e-01  1.387e-01   1.042 0.297472    
## ALC_CUR_FREQ3       4.597e-03  1.271e-01   0.036 0.971141    
## ALC_CUR_FREQ4      -4.623e-01  1.298e-01  -3.563 0.000367 ***
## ALC_CUR_FREQ5      -3.469e-01  1.210e-01  -2.868 0.004135 ** 
## ALC_CUR_FREQ6      -3.818e-01  1.315e-01  -2.903 0.003701 ** 
## ALC_CUR_FREQ7      -2.629e-01  1.331e-01  -1.975 0.048292 *  
## DIS_DEP_EVER1       1.065e-01  8.036e-02   1.325 0.185251    
## DIS_DEP_EVER2       3.920e-01  2.490e-01   1.575 0.115378    
## DIS_DIAB_TYPE1      8.212e-01  2.837e-01   2.895 0.003800 ** 
## DIS_DIAB_TYPE2      1.013e+00  1.136e-01   8.921  < 2e-16 ***
## DIS_DIAB_TYPE3      1.074e+00  2.451e-01   4.382 1.18e-05 ***
## ADM_STUDY_ID2       1.221e+00  9.969e-02  12.244  < 2e-16 ***
## ADM_STUDY_ID3       3.109e-01  8.384e-02   3.708 0.000209 ***
## ADM_STUDY_ID5       1.700e+00  1.031e-01  16.490  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.002 on 41155 degrees of freedom
## Multiple R-squared:  0.06947,	Adjusted R-squared:  0.06877 
## F-statistic: 99.12 on 31 and 41155 DF,  p-value: < 2.2e-16
```

``` r
model_KNN <- imputed_data_KNN %>% 
   with(lm(PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT +
                  PA_TOTAL_SIT_TIME + SDC_EB_ABORIGINAL +
                  SDC_AGE_CALC + SDC_GENDER+ 
                  WRK_EMPLOYMENT + HS_GEN_HEALTH +
                  NUT_VEG_QTY + NUT_FRUITS_QTY +
                  SMK_CIG_STATUS + ALC_CUR_FREQ +
                  DIS_DEP_EVER + DIS_DIAB_TYPE +
                  ADM_STUDY_ID))
#model for KNNN imputation
 summary(model_KNN)
```

```
## 
## Call:
## lm(formula = PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT + PA_TOTAL_SIT_TIME + 
##     SDC_EB_ABORIGINAL + SDC_AGE_CALC + SDC_GENDER + WRK_EMPLOYMENT + 
##     HS_GEN_HEALTH + NUT_VEG_QTY + NUT_FRUITS_QTY + SMK_CIG_STATUS + 
##     ALC_CUR_FREQ + DIS_DEP_EVER + DIS_DIAB_TYPE + ADM_STUDY_ID)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -19.949  -3.513  -0.710   2.667  41.391 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)         2.816e+01  3.110e-01  90.544  < 2e-16 ***
## PA_TOTAL_SHORT     -8.685e-05  1.127e-05  -7.705 1.34e-14 ***
## PA_TOTAL_SIT_TIME   1.301e-04  2.505e-05   5.194 2.07e-07 ***
## SDC_EB_ABORIGINAL1  2.568e-01  1.417e-01   1.813 0.069870 .  
## SDC_AGE_CALC        2.806e-02  2.829e-03   9.916  < 2e-16 ***
## SDC_GENDER2        -1.111e+00  5.933e-02 -18.719  < 2e-16 ***
## WRK_EMPLOYMENT1    -6.744e-02  6.402e-02  -1.053 0.292129    
## HS_GEN_HEALTH2     -4.274e-02  2.147e-01  -0.199 0.842239    
## HS_GEN_HEALTH3     -8.354e-01  2.002e-01  -4.173 3.02e-05 ***
## HS_GEN_HEALTH4     -2.885e+00  2.006e-01 -14.380  < 2e-16 ***
## HS_GEN_HEALTH5     -3.628e+00  2.078e-01 -17.457  < 2e-16 ***
## NUT_VEG_QTY         3.273e-02  1.884e-02   1.737 0.082365 .  
## NUT_FRUITS_QTY     -9.409e-03  2.185e-02  -0.431 0.666743    
## SMK_CIG_STATUS1     3.362e-01  6.055e-02   5.553 2.83e-08 ***
## SMK_CIG_STATUS2     3.271e-01  1.771e-01   1.847 0.064779 .  
## SMK_CIG_STATUS3     3.464e-02  1.011e-01   0.343 0.731955    
## ALC_CUR_FREQ0       2.832e-01  1.526e-01   1.856 0.063478 .  
## ALC_CUR_FREQ1       1.330e-01  1.271e-01   1.046 0.295420    
## ALC_CUR_FREQ2       3.123e-01  1.473e-01   2.119 0.034074 *  
## ALC_CUR_FREQ3       4.205e-02  1.348e-01   0.312 0.755126    
## ALC_CUR_FREQ4      -5.670e-01  1.382e-01  -4.103 4.08e-05 ***
## ALC_CUR_FREQ5      -5.587e-01  1.283e-01  -4.355 1.34e-05 ***
## ALC_CUR_FREQ6      -4.983e-01  1.398e-01  -3.564 0.000366 ***
## ALC_CUR_FREQ7      -4.600e-01  1.416e-01  -3.248 0.001162 ** 
## DIS_DEP_EVER1       1.360e-01  8.582e-02   1.585 0.113033    
## DIS_DEP_EVER2       9.404e-02  2.475e-01   0.380 0.704002    
## DIS_DIAB_TYPE1      8.470e-01  3.116e-01   2.719 0.006559 ** 
## DIS_DIAB_TYPE2      1.128e+00  1.238e-01   9.114  < 2e-16 ***
## DIS_DIAB_TYPE3      1.666e+00  2.684e-01   6.206 5.49e-10 ***
## ADM_STUDY_ID2       1.524e+00  1.097e-01  13.893  < 2e-16 ***
## ADM_STUDY_ID3      -6.900e-02  9.241e-02  -0.747 0.455260    
## ADM_STUDY_ID5       2.385e+00  1.136e-01  20.998  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.51 on 41155 degrees of freedom
## Multiple R-squared:  0.1003,	Adjusted R-squared:  0.0996 
## F-statistic:   148 on 31 and 41155 DF,  p-value: < 2.2e-16
```

``` r
 model_mice <- imputed_data_mice_c %>% 
   with(lm(PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT +
                  PA_TOTAL_SIT_TIME + SDC_EB_ABORIGINAL +
                  SDC_AGE_CALC + SDC_GENDER+ 
                  WRK_EMPLOYMENT + HS_GEN_HEALTH +
                  NUT_VEG_QTY + NUT_FRUITS_QTY +
                  SMK_CIG_STATUS + ALC_CUR_FREQ +
                  DIS_DEP_EVER + DIS_DIAB_TYPE +
                  ADM_STUDY_ID))
#model for KNNN imputation
 summary(model_mice)
```

```
## 
## Call:
## lm(formula = PM_BMI_SR ~ PA_TOTAL_SHORT + PA_TOTAL_SHORT + PA_TOTAL_SIT_TIME + 
##     SDC_EB_ABORIGINAL + SDC_AGE_CALC + SDC_GENDER + WRK_EMPLOYMENT + 
##     HS_GEN_HEALTH + NUT_VEG_QTY + NUT_FRUITS_QTY + SMK_CIG_STATUS + 
##     ALC_CUR_FREQ + DIS_DEP_EVER + DIS_DIAB_TYPE + ADM_STUDY_ID)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -21.174  -3.782  -0.810   2.833  41.317 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)         2.825e+01  3.331e-01  84.824  < 2e-16 ***
## PA_TOTAL_SHORT     -8.629e-05  1.152e-05  -7.489 7.10e-14 ***
## PA_TOTAL_SIT_TIME   1.355e-04  2.499e-05   5.422 5.94e-08 ***
## SDC_EB_ABORIGINAL1  5.612e-01  1.512e-01   3.712 0.000206 ***
## SDC_AGE_CALC        3.221e-02  3.030e-03  10.629  < 2e-16 ***
## SDC_GENDER2        -1.209e+00  6.314e-02 -19.154  < 2e-16 ***
## WRK_EMPLOYMENT1    -4.064e-02  6.849e-02  -0.593 0.552949    
## HS_GEN_HEALTH2     -4.471e-01  2.279e-01  -1.961 0.049830 *  
## HS_GEN_HEALTH3     -1.468e+00  2.128e-01  -6.898 5.34e-12 ***
## HS_GEN_HEALTH4     -3.592e+00  2.132e-01 -16.844  < 2e-16 ***
## HS_GEN_HEALTH5     -4.355e+00  2.209e-01 -19.713  < 2e-16 ***
## NUT_VEG_QTY         3.269e-02  1.970e-02   1.659 0.097110 .  
## NUT_FRUITS_QTY     -6.779e-02  2.307e-02  -2.938 0.003300 ** 
## SMK_CIG_STATUS1     2.919e-01  6.435e-02   4.536 5.74e-06 ***
## SMK_CIG_STATUS2     5.102e-01  1.844e-01   2.766 0.005672 ** 
## SMK_CIG_STATUS3    -7.783e-02  1.064e-01  -0.731 0.464689    
## ALC_CUR_FREQ0       2.258e-01  1.641e-01   1.376 0.168908    
## ALC_CUR_FREQ1       7.947e-02  1.371e-01   0.579 0.562266    
## ALC_CUR_FREQ2       8.622e-02  1.583e-01   0.545 0.585928    
## ALC_CUR_FREQ3       9.775e-03  1.452e-01   0.067 0.946346    
## ALC_CUR_FREQ4      -6.336e-01  1.484e-01  -4.270 1.96e-05 ***
## ALC_CUR_FREQ5      -5.496e-01  1.384e-01  -3.972 7.14e-05 ***
## ALC_CUR_FREQ6      -5.467e-01  1.505e-01  -3.634 0.000280 ***
## ALC_CUR_FREQ7      -3.817e-01  1.524e-01  -2.504 0.012273 *  
## DIS_DEP_EVER1       2.938e-01  8.903e-02   3.300 0.000968 ***
## DIS_DEP_EVER2       2.218e-02  2.796e-01   0.079 0.936780    
## DIS_DIAB_TYPE1      7.653e-01  3.266e-01   2.343 0.019126 *  
## DIS_DIAB_TYPE2      1.566e+00  1.304e-01  12.009  < 2e-16 ***
## DIS_DIAB_TYPE3      1.659e+00  2.818e-01   5.887 3.96e-09 ***
## ADM_STUDY_ID2       1.795e+00  1.166e-01  15.392  < 2e-16 ***
## ADM_STUDY_ID3       6.633e-01  9.820e-02   6.755 1.44e-11 ***
## ADM_STUDY_ID5       3.537e+00  1.207e-01  29.298  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.855 on 41155 degrees of freedom
## Multiple R-squared:  0.1094,	Adjusted R-squared:  0.1087 
## F-statistic: 163.1 on 31 and 41155 DF,  p-value: < 2.2e-16
```

Original Dataset (No Imputation)

Observations Deleted: 22,489 observations were deleted due to missingness, reducing the sample size to 18,666.
Residual Standard Error: 5.684
R-squared: 0.1024
Key Findings:
Significant predictors include PA_TOTAL_SHORT, PA_TOTAL_SIT_TIME, SDC_AGE_CALC, SDC_GENDER, HS_GEN_HEALTH, SMK_CIG_STATUS, ALC_CUR_FREQ, DIS_DIAB_TYPE, and ADM_STUDY_ID at 5 percent level of significant. 
The effect sizes and significance levels are based on the complete cases, which may introduce bias if the missing data are not MCAR.

Mean Imputation

Observations Deleted: None (all missing values were imputed).
Residual Standard Error: 5.002
R-squared: 0.06947
Key Findings:
The residual standard error is lower, and the R-squared is slightly lower compared to the original dataset.
Some predictors that were significant in the original dataset (e.g., SDC_EB_ABORIGINAL, NUT_FRUITS_QTY) became less significant or insignificant.
The effect sizes for some predictors (e.g., SDC_GENDER, HS_GEN_HEALTH, DIS_DIAB_TYPE) are smaller than those in the original dataset.
Mean imputation tends to reduce variability and may underestimate the true effect sizes.

KNN Imputation

Observations Deleted: None (all missing values were imputed).
Residual Standard Error: 5.51
R-squared: 0.1003
Key Findings:
The residual standard error and R-squared are closer to the original dataset compared to mean imputation.
Some predictors (e.g., SDC_EB_ABORIGINAL, NUT_VEG_QTY, NUT_FRUITS_QTY) show different significance levels compared to the original dataset.
The effect sizes for some predictors (e.g., SDC_GENDER, HS_GEN_HEALTH, DIS_DIAB_TYPE) are closer to the original dataset compared to mean imputation.
KNN imputation preserves more of the data structure and variability than mean imputation.

MICE Imputation

Observations Deleted: None (all missing values were imputed).
Residual Standard Error: 5.855
R-squared: 0.1094
Key Findings:
The residual standard error is slightly higher, and the R-squared is slightly higher compared to the original dataset.
Some predictors (e.g., SDC_EB_ABORIGINAL, NUT_FRUITS_QTY, DIS_DEP_EVER) show different significance levels compared to the original dataset.
The effect sizes for some predictors (e.g., SDC_GENDER, HS_GEN_HEALTH, DIS_DIAB_TYPE) are closer to the original dataset compared to mean and KNN imputation.
MICE imputation accounts for the uncertainty in imputed values and typically produces more reliable estimates compared to mean and KNN imputation.

5. **Interpretation and Reporting**
   - Provide a detailed comparison of the methods, discussing their strengths, weaknesses, and suitability for the dataset.
   # Mean/Median/Mode Imputation

Method: Replace missing values with the mean, median, or mode of the observed data.
Impact:
Advantages:
Simple and easy to implement.
Preserves the sample size.
Disadvantages:
Reduces variability in the data, leading to underestimation of variance.
Can distort relationships between variables (e.g., correlations, regression coefficients).
Ignores the uncertainty of the imputed values.
Use Case: Suitable for preliminary analysis or when the proportion of missing data is very small.

# k-Nearest Neighbors (KNN) Imputation

Method: Replace missing values with the average (or weighted average) of the k-nearest neighbors in the feature space.
Advantages:
Captures local patterns in the data.
Preserves relationships between variables better than mean imputation.
Disadvantages:
Computationally expensive for large datasets.
Sensitive to the choice of k and the distance metric.
May introduce bias if the data has a complex structure.
Use Case: Useful for datasets with complex relationships and moderate missingness.

# Multiple Imputation by Chained Equations (MICE)

Method: Generate multiple imputed datasets by modeling each variable with missing data conditional on other variables.
Impact:
Advantages:
Accounts for uncertainty in the imputed values by generating multiple datasets.
Preserves relationships between variables and the variability of the data.
Flexible and can handle different types of variables (continuous, categorical).
Disadvantages:
Computationally intensive.
Requires careful specification of the imputation model.
Use Case: Ideal for datasets with complex missing data mechanisms and when unbiased estimates of uncertainty are needed.

   - Reflect on the challenges of handling missing data in health research.

Bias: The analysis may produce biased estimates if missingness is not random (MAR or MNAR).
Reduced Statistical Power: Missing data reduces the adequate sample size, leading to less precise estimates and lower power to detect significant effects.
Loss of Generalizability: If the missing data pattern is related to specific subgroups, the results may not be generalizable to the entire population.
Challenge: Ensuring that the analysis remains valid and generalizable despite missing data.

## References
