# Term Guide
The  Sample Data - Full Reporting Format terms are defined below, including  whether that term is required, a brief definition, formatting requirements, an example, and additional guidance. Additional required terms are included in the [Location Metadata Reporting Format](https://github.com/ess-dive-workspace/essdive-location-metadata/blob/release-v2.0.0/term_guide.md) and [Sample ID and Metadata Reporting Format](https://github.com/ess-dive-workspace/essdive-sample-id-metadata/blob/release-v2.0/guide.md).

A single asterisk (*) below marks terms that are required. Two asterisks (**) mark fields that are conditionally required.

### Terms of the reporting format:
[**Sample Data File**](#sample-data-file)
- [sample_name](#sample_name)*
- [{measurement_column_name}](#measurement_column_name)*
- [{measurement_column_name}_method_id](#measurement_column_name_method_id)*
- [time_elapsed](#time_elapsed)**
- [treatment_id](#treatment_id)
- [datetime_measured](#datetime_measured)
- [{measurement_column_name}_flag](#measurement_column_name_flag)
- [notes](#notes)
 
[**Methods and Attributes File**](#methods-and-attributes-file)
- [attr_id](#attr_id)*
- [attr_type](#attr_type)*
- [attr_description](#attr_description)*
- [analysis_detection_limit](#analysis_detection_limit)
- [analysis_precision](#analysis_precision)
- [instrument_precision](#instrument_precision)
- [lower_bound](#lower_bound)
- [upper_bound](#upper_bound)
- [method_instrument](#method_instrument)
- [method_reference](#method_reference)
- [method_hold_time](#method_hold_time)
- [method_temp](#method_temp)
- [method_light](#method_light)
- [method_atmosphere](#method_atmosphere)
- [method_moisture](#method_moisture)
- [method_medium](#method_medium)
- [method_time](#method_time)
- [method_lab_contact](#method_lab_contact)
- [method_instrument_operator](#method_instrument_operator)
- [method_lab](#method_lab)
 
[**File Level Metadata File**](#file-level-metadata-file)
- [file_name](#file_name)*
- [file_description](#file_description)*
- [standard](#standard)*
- [data_dictionary_file_name](#data_dictionary_file_name)*
- [file_version](#file_version)
- [data_orientation](#data_orientation)
- [header_rows](#header_rows)
- [column_or_row_name_position](#column_or_row_name_position)
- [notes](#notes-1)

[**Data Dictionary File**](#data-dictionary-file)
- [column_or_row_name](#column_or_row_name)*
- [unit](#unit)*
- [definition](#definition)*
- [measured_variable](#measured_variable)*
- [column_or_row_long_name](#column_or_row_long_name)
- [data_type](#data_type)
- [missing_value_code](#missing_value_code)
- [unit_basis](#unit_basis)
- [statistic_measurement](#statistic_measurement)
- [statistic_spatial](#statistic_spatial)
- [statistic_temporal](#statistic_temporal)
- [representation_temporal](#representation_temporal)
- [notes](#notes-2)

[**Location Metadata Reporting Format Term Guide**](https://github.com/ess-dive-workspace/essdive-location-metadata/blob/release-v2.0.0/term_guide.md)

[**Sample Metadata and ID Reporting Format Term Guide**](https://github.com/ess-dive-workspace/essdive-sample-id-metadata/blob/release-v2.0/guide.md)

---
## Sample Data File
### sample_name
|term|`sample_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|Collector's project-specific sample name, which must be unique for each sample within the dataset that you are submitting.|
|example|CM_023|
|additional guidance|Sample names must be unique within the dataset and ideally are unique across a project.|

### {measurement_column_name}
|term|`{measurement_column_name}`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; only UTF-8 characters are permitted|
|unit|N/A|
|definition|User-defined measurement column name. Strongly recommend to use only letters, numbers, underscores, and hyphens.|
|example|temp_soil_2|
|additional guidance|`{measurement_column_name}` is considered arbitrary. They are not parsed for information on type of variable, unit, statistic, or temporal representation. Each `{measurement_column_name}` must be defined in the data dictionary file using the required fields that include `measured_variable` and `unit`. Optional fields, such as `statistic_*`, `representation_temporal`, and `unit_basis`, should be used to fully describe the measurement characteristics. |

### {measurement_column_name}_method_id
|term|`{measurement_column_name}_method_id`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; only UTF-8 characters are permitted; semicolon whitespace delimiter|
|unit|N/A|
|definition|User-defined identifier that indicates what methods were used for the individual measurement in the corresponding measurement_column_name. Strongly recommended to use only letters, numbers, underscores, and hyphens. |
|example|temp_soil_2_method_id|
|additional guidance|Column header for associated `{measurement_column_name}` will be appended with “_method_id” for a method_id column. The method ID must be defined within the methods and attributes file. <br><br>If more than one method_id is populated in a single cell, they should be separated by a semicolon and space.|

### time_elapsed
|term|`time_elapsed`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Required conditionally for time series measurements on a single sample|
|format|numeric|
|unit|second|
|definition|Cumulative time elapsed, to known specificity, between the first measurement and the current measurement, on a single sample.|
|example|30|
|additional guidance|Used to indicate the passage of time when taking multiple measurements through time on a single sample.|

### treatment_id
|term|`treatment_id`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|Optional|
|format|text; only UTF-8 characters are permitted |
|unit|N/A|
|definition|User-defined identifier that indicates what treatment was used for manipulation experiments, if applicable. Strongly recommended that only letters, numbers, hyphens, and underscores are used.|
|example|treatment_wet_01|
|additional guidance|Treatment IDs should be defined within the methods and attributes file. <br><br> It is recommended that if there is no treatment but the column is present, the `treatment_id` should be “N/A”. It is recommended that if there is a control treatment, the `treatment_id` should be “control”.|

### datetime_measured
|term|`datetime_measured`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|datetime, ISO 8601:2019|
|unit|N/A|
|definition|Date and time of measurement, to known specificity.|
|example|2026-03-12T13:50-06:00|
|additional guidance|Dates must be reported in the ISO 8601:2019 standard (YYYY-MM-DD) and completed to known precision (e.g. YYYY-MM, YYYY). Times must be reported with a date in either Coordinated Universal Time (UTC) (YYYY-MM-DDThh:mm:ssZ) or Local Standard Time with the UTC offset (YYYY-MM-DDThh:mm±hh:mm). It is strongly recommended not to change UTC offset in the middle of a time series (i.e., do not switch from Standard Time to Daylight Savings Time). Complete times to known precision (e.g. YYYY-MM-DDThh). Use of "T" and either “Z” or “±” characters are required. <br><br> YYYY = 4-digit year, MM = 2-digit month, DD = 2-digit day of month, hh = 2-digit hour ranging from 00-23, mm = 2-digit minute, ss = 2-digit second.|

### {measurement_column_name}_flag
|term|`{measurement_column_name}_flag`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|text; only UTF-8 characters are permitted|
|unit|N/A|
|definition|User-defined identifier that indicates a flag for the individual measurement in the corresponding measurement_column_name. Strongly recommend to use only letters, numbers, underscores, and hyphens.|
|example|temp_soil_2_flag|
|additional guidance|Column header for associated `{measurement_column_name}` will be appended with “_flag” for a flag column. Flag codes must be defined in the methods and attributes file|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Free text notes field.|
|example|Storm event occurred during sampling.|
|additional guidance|N/A|

---

## Methods and Attributes File
###  attr_id
|term|`attr_id`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; only UTF-8 characters are permitted|
|unit|N/A|
|definition|Attribute identifier associated with either a method ID, flag, treatment ID, or sensor ID. Strongly recommend to use only letters, numbers, underscores, and hyphens.|
|example|soil_method_012|
|additional guidance|N/A|

###  attr_type
|term|`attr_type`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#attr-type)|
|unit|N/A|
|definition|Attribute identifier type|
|example|method_id|
|additional guidance|N/A|

###  attr_description
|term|`attr_description`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|Description of the attribute identifier provided within the attr_id field|
|example|N/A|
|additional guidance|N/A|

###  analysis_detection_limit
|term|`analysis_detection_limit`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|See associated measurement column unit|
|definition|Detection limit associated with the analysis (i.e., the lowest / smallest quantity that can be measured), in the units of the reported measurement|
|example|0.05|
|additional guidance|N/A|

###  analysis_precision
|term|`analysis_precision`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|See associated measurement column unit|
|definition|Precision associated with the analysis (i.e., how close repeated measures are to each other), in the units of the reported measurement|
|example|0.02|
|additional guidance|N/A|

###  instrument_precision
|term|`instrument_precision`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|See associated measurement column unit|
|definition|Precision of the instrument/sensor (i.e., the smallest difference between measurements that the instrument can resolve), in the units of the reported measurement|
|example|0.02|
|additional guidance|N/A|

### lower_bound
|term|`lower_bound`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|See associated measurement column unit|
|definition|Lower bound of expected data values, in the units of the reported measurement|
|example|5|
|additional guidance|Bounds can support programmatic removal of flagged values. The lower bound may describe what is physically possible for the measurement type or what is expected for the particular system.|

### upper_bound
|term|`upper_bound`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|See associated measurement column unit|
|definition|Upper bound of expected data values, in the units of the reported measurement|
|example|8|
|additional guidance|Bounds can support programmatic removal of flagged values. The upper bound may describe what is physically possible for the measurement type or what is expected for the particular system.|

###  method_instrument
|term|`method_instrument`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Instrument specifications (e.g., type; model; manufacturer; manufacturing location)|
|example|WestCo SmartChem 200 Discrete Analyzer|
|additional guidance|N/A|

###  method_reference
|term|`method_reference`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Citation or link to published method description|
|example|https://www.epa.gov/sites/production/files/2015-08/documents/method_353-2_1993.pdf|
|additional guidance|It is recommended to list the full citation in the dataset related references when uploading data.|

###  method_hold_time
|term|`method_hold_time`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Hold time for the method, including the units. Use the [unit term controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#unit).|
|example|24 hour|
|additional guidance|Maximum duration of time a sample could be held for a designated analysis before no longer considered viable.|

###  method_temp
|term|`method_temp`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Temperature at which method was carried out. If a temperature numeric value is entered, include units following the [unit term controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#unit).|
|example|72 degree Celsius|
|additional guidance|Format can be numeric or descriptive. If numeric, use the unit term controlled vocabulary. Some descriptive examples include "ambient", "unknown", "iced", and "heated".|

###  method_light
|term|`method_light`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Light conditions for the method|
|example|dark|
|additional guidance|N/A|

###  method_atmosphere
|term|`method_atmosphere`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Atmosphere for the method|
|example|anoxic|
|additional guidance|N/A|

###  method_moisture
|term|`method_moisture`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Moisture conditions of sample exposed to method|
|example|field moist|
|additional guidance|N/A|

###  method_medium
|term|`method_medium`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Medium used for the method (e.g. extractions; dilutions; nutrient media for incubations).|
|example|2x dilution in Milli-Q water|
|additional guidance|Most applicable to report for methods involving manipulations of the initial sample medium.|

###  method_time
|term|`method_time`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Time span for method (e.g. incubation time; storage time; extraction time)|
|example|2 hour incubation|
|additional guidance|N/A|

###  method_lab_contact
|term|`method_lab_contact`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Contact details for the laboratory where the method was performed|
|example|Lawrence Berkeley National Laboratory, Berkeley CA|
|additional guidance|Contact details for the laboratory where the method was performed (e.g. name of contact person; email; website; postal address; phone number).|

###  method_instrument_operator
|term|`method_instrument_operator`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Name of the instrument operator|
|example|Jane Doe; Jane.Doe@JaneDoe.Jane; 000-000-0000|
|additional guidance|Contact details for the operator of the instrument (e.g. name of person; email; phone number; ORCID).|

###  method_lab
|term|`method_lab`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Name of the laboratory where the method was performed|
|example|UC Davis Analytical Lab|
|additional guidance|It may be appropriate to list more than one laboratory but it must be clear what was done where.|

---

## File Level Metadata File
### file_name
|term|`file_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|N/A|
|definition|Provide the name of the associated file. File names should be unique and be as descriptive as possible about the file contents. Use only letters (e.g. CamelCase), numbers, and underscores. Do not include spaces. Hyphens allowed but not preferred. Use "\*" wildcard when the FLMD applies to multiple files. For example - the same FLMD applies to all soil core files in this data package - "soil_cores_*.csv"|
|example|measurements.csv|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-name).|

### file_description
|term|`file_description`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement| required|
|format|N/A|
|definition|A brief description (minimum of 10 characters) of the file and what distinguishes this file from other files in the data package. Include information about the type of data (images, observations, experimental, etc.) |
|example|Geochemistry data measurements, including anions and cations, for 2025-06-08 to 2026-01-02.|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-description).|

### standard
|term|`standard`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/RF_FLMD_Standard_Terms.csv)|
|definition|Identify if an ESS-DIVE Reporting Format or any other data or metadata standard was applied to the data file. Standard names for the ESS-DIVE reporting formats are available in the [Standard FLMD Term List](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/RF_FLMD_Standard_Terms.csv).| 
|example|ESS-DIVE Sample Data - Full Reporting Format v1|
|additional guidance|For any files following the Sample Data - Full reporting format, including data, methods and attributes, and data dictionary, provide "ESS-DIVE Sample Data - Full Reporting Format v1" in the `standard` field.|

### data_dictionary_file_name
|term|`standard`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|text; contains “_dd.csv"|
|definition|The file name of the data dictionary that corresponds to the provided “file_name” entry. The file name must end with “_dd.csv”.| 
|example|measurements_dd.csv|
|additional guidance|N/A|

### file_version
|term|`file_version`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|definition|This is the version of the data file being described in the FLMD. The data file version is assigned by the data provider and not by the system. This would change if the data file is updated after the data package is published. Changes should be explained in the Notes field.| 
|example|version 1|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#file-version).|

### data_orientation
|term|`data_orientation`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|horizontal or vertical|
|definition|Describe how the data are organized within the data matrix. Choose between "horizontal" (i.e., data are organized in rows with column headers) or "vertical" (i.e., data are organized in columns with row headers).| 
|example|horizontal|
|additional guidance|For files following the Sample Data - Lite reporting format, the `data_orientation` value should be "horizontal".| 

### header_rows
|term|`header_rows`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|N/A|
|definition|Provide the total number of header rows before the start of the first data row, including the column header or row name. Do not include commented-out (i.e., column/rows that begin with a hash (#)) in the header_rows count. This field is marked as optional, but is required if any data files have more than one header row.|
|example|1|
|additional guidance|For files following the Sample Data - Full reporting format, the `header_rows` value should be 1.|

### column_or_row_name_position
|term|`column_or_row_name_position`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|numeric|
|unit|N/A|
|definition|Provide the row or column number that contains the header names. This field is not required if there are no rows or columns before the row/column names. If not included, it will be assumed that header names are in row 1 (horizontal orientation) or column 1 (vertical orientation). Do not include commented-out (i.e., column/rows that begin with a hash (#)) in the column_or_row_name_position count. |
|example|1|
|additional guidance|For files following the Sample Data - Full reporting format, the `column_or_row_name_position` value should be 1.|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|definition|Information provided would be data file specific. Details may include details on data file versioning, reporting format, software requirements, data quality, etc.| 
|example||
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/flmd_quick_guide.md#notes).| 

---

## Data Dictionary File
### column_or_row_name
|term|`column_or_row_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|Column or row name from the data file. Provide entries for each column or row name from the data matrix in the data file.|
|example|temp_soil_2|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/CSV_dd/csv_dd_quick_guide.md#column-or-row-name).|

### unit
|term|`unit`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#unit)|
|unit|N/A|
|definition|Unit of measurement.|
|example|degree Celsius|
|additional guidance|Insert "N/A" when units aren't applicable.|

### definition
|term|`definition`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|free text|
|unit|N/A|
|definition|A description of the column/row header.|
|example|Soil temperature replicate 2 at location loc_25d|
|additional guidance|Definitions for reporting format terms must be used as is from the provided data dictionary template. For user-defined `{measurement_column_name}`, the measurement characteristics must be defined in the required fields that include `measured_variable` and `unit`. Optional fields, such as `statistic_*`, `representation_temporal`, and `unit_basis`, should be used to fully describe the measurement characteristics. The measurement characteristics can be repeated in the definition; however downstream resources will primarily utilize the other specific data dictionary fields.|

### measured_variable
|term|`measured_variable`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|required|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#measured_variable)|
|unit|N/A|
|definition|The variable or property being measured. This field is only used for `{measurement_column_name}` column headers / rows.|
|example|temperature|
|additional guidance|N/A|

### column_or_row_long_name
|term|`column_or_row_long_name`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|recommended|
|format|free text|
|unit|N/A|
|definition|Longer human-readable column or row name. Sometimes this may be identical to Definition or even Column_or_Row_Name.|
|example|temperature_soil_2|
|additional guidance|This term is from the File Level Metadata reporting format, more details can be reviewed [here](https://github.com/ess-dive-workspace/essdive-file-level-metadata/blob/main/CSV_dd/csv_dd_quick_guide.md#column-or-row-long-name)|

### data_type
|term|`data_type`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#data_type)|
|unit|N/A|
|definition|Data type for each column|
|example|text|
|additional guidance|N/A|

### missing_value_code
|term|`missing_value_code`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|The missing value code used for missing measurements. Only one code allowed.|
|example|-9999|
|additional guidance|Based on the CSV Reporting Format guidelines, for columns containing numeric data, ESS-DIVE recommends using "-9999" as the missing value code. For columns containing character data, ESS-DIVE recommends using "N/A" as the missing value code. If you would like to use a different missing value code, specify the used missing value code within this field. If a missing value code is not applicable for a column, leave this entry blank or use a generic missing value code.|

### unit_basis
|term|`unit_basis`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Basis for how the measurement values are quantified (e.g., “as nitrate” vs. “as nitrogen”; “per kg dry sediment”; “relative to Vienna Pee Dee Belemnite”). Provide if relevant.|
|example|as carbon|
|additional guidance|This information is important for the correct interpretation of the measurement value.|

### statistic_measurement
|term|`statistic_measurement`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistic description, if applicable. This term is only used for `{measurement_column_name}` headers / rows if the measured value represents repeated observations of the same scientifically-equivalent spatial location and/or temporal period (e.g., replicates), or for general uncertainty in the measurement itself.|
|example|mean|
|additional guidance|A measurement statistic typically describes variation or uncertainty in the measurement. This can be obtained / reported by an instrument or calculated via replicates. Replicates include multiple measures on the same physical sample and/or samples collected at different locations and times that are not indistinguishable for the scientific purpose. Use the spatial and / or temporal statistical descriptions, if the variability is due to multiple scientifically important locations or time periods.|

### statistic_spatial
|term|`statistic_spatial`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistical description, if applicable. This term is only used for `{measurement_column_name}` headers / rows if the measured value represents a combination of individual observations from separate locations to represent a larger location.|
|example|mean|
|additional guidance|The spatial statistic should be used to describe measurement values that are a combination of separate spatial locations.|

### statistic_temporal
|term|`statistic_temporal`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#statistic)|
|unit|N/A|
|definition|Statistic description, if applicable. This term is only used for `{measurement_column_name}` headers / rows if the measured value represents a combination of individual observations at different times to represent a larger time period. In most cases, a corresponding representation_temporal should be specified.|
|example|mean|
|additional guidance|The temporal statistic should be used when the measurement value is a combination of individual measurements made at separate times.|

### representation_temporal
|term|`representation_temporal`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|[Controlled vocabulary](https://github.com/ess-dive-workspace/essdive-sample-data-full/blob/release-v1.0.0/controlled_vocabulary.md#representation_temporal)|
|unit|N/A|
|definition|Temporal representativeness of the measurement, if applicable. This field is only used for data dictionary rows where the `column_or_row_name` entry is a measured variable. In many cases, a corresponding `statistic_temporal` should be specified. The temporal representation will be considered instantaneous if no value is provided and `datetime_measured` is reported (instead of `datetime_measured_start` and `datetime_measured_end`).|
|example|month|
|additional guidance|The temporal representation should be used when the measurement value is not an instantaneous observation and/or represents a non-instantaneous time period. <br><br> If `datetime_measured_start` and `datetime_measured_end` are reported and a temporal representation is applicable, the temporal representation should match the temporal difference.|

### notes
|term|`notes`|
|:----------------------------------------------------|:----------------------------------------------------|
|requirement|optional|
|format|free text|
|unit|N/A|
|definition|Free text notes field|
|example||
|additional guidance|N/A|
