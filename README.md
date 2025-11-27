# Capstone-Assignment-20.1-Initial-Report-and-EDA

Jupyter NoteBook link - 

### Problem statement:
Goal is to Predict the SSD rated life consumed based on the SSD drive log page/system data collected through NetApp Autosupport feature. 

### Data:
Dataset is from NetApp ASUP. The dataset contains 49,424 observations and 30 columns spanning device-level metadata, configuration information, and SSD health indicators. 
The schema is cleanly structured: 14 numeric columns, 15 categorical identifiers,

### Data Analysis and Findings:
Correlation and redundancy analysis identified several groups of variables that convey similar information. For example, the time-related fields dt and asup_id are nearly perfectly correlated, so only one should be retained for modeling. Metrics such as average_erase_block_count, max_erase_block_count, and rated_life_used exhibit highly similar patterns, all reflecting device wear and degradation. Likewise, host_write_block_count and total_nand_write_block_count are closely linked, both summarizing cumulative write activity. A strong correlation also exists between available_spares_percentage and dvc_glist_ct. These relationships reveal that the dataset contains fewer independent signals than its raw number of columns suggests, making feature selection or dimensionality reduction essential for effective modeling. Principal Component Analysis (PCA) confirms this, showing that the first five components account for over 80% of the total variance, with the most influential components driven by wear and workload metrics.

Multivariate analysis using parallel-coordinate plots was applied to all categorical variables. For categories such as sys_model, dvc_label, dvc_primary_port, and rg_type, the plot lines largely overlapped, indicating these groupings do not significantly affect the distribution of the main numeric features. This suggests that configuration-level categories have little impact on device health or workload metrics, and neither system nor RAID type produces distinct multivariate profiles. Additionally, disk_type contains only a single category and thus does not contribute any variation. Overall, the dataset’s diversity is primarily shaped by wear, workload, and defect metrics, rather than by categorical attributes. Further exploration with techniques like Andrews curves, grouped boxplots, or PCA scatterplots could provide additional insight, but current evidence points to a small set of degradation and usage factors as the main drivers of data structure.

### Summary:
The dataset is large, well-organized, and consistent. Many features are redundant due to multicollinearity, especially among wear indicators, workload counters, and spare-related metrics. Categorical variables offer limited explanatory value beyond identifying individual systems, and high-cardinality identifiers are not useful for analysis. Exploratory Data Analysis strongly indicates that meaningful modeling should concentrate on a streamlined set of numeric features related to wear, defects, and workload, while removing redundant variables and disregarding identifier-like categorical fields.








