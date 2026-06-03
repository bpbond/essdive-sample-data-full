# Instructions

## SCOPE
- The Sample Data - Full Reporting Format is intended for data-generated in a laboratory from physical samples This can include a set of individual samples or a time series of measurements on a single sample.
- This reporting format (RF) provides guidance on file structure and contents for data and metadata. It includes a term guide, templates, examples, and several controlled vocabularies.
- To be compliant with this RF, you must also adhere to the requirements in the [CSV](https://github.com/ess-dive-workspace/essdive-csv-structure), [File Level Metadata](https://github.com/ess-dive-workspace/essdive-file-level-metadata), [Location Metadata](https://github.com/ess-dive-workspace/essdive-location-metadata/tree/release-v2.0.0), and [Sample ID and Metadata](https://github.com/ess-dive-workspace/essdive-sample-id-metadata/tree/release-v2.0) Reporting Formats, as detailed below. 
- A simpler version of this reporting format ([Sample Data - Lite](https://github.com/ess-dive-workspace/essdive-sample-data-lite/tree/release-v1.0.0)) is also available for laboratory-generated sample data. 
    - The Full version supports more detailed metadata and provides flexibility to describe more approaches. For example, sample tracking, named locations, non-point locations, and complex / detailed methods are supported. 
    - The Lite version supports less detailed metadata and only common approaches. For example, point locations in only WGS84 datum and high-level methods are supported;  sample tracking is not supported.

## CHECKLIST FOR SUBMISSION
- [Data file(s)](#data-files) (as many as needed)
- [Methods and attributes file](#methods-and-attributes-file) (one)
- [Data dictionary file(s)](#data-dictionary-files) (as many as needed)
- [File level metadata file](#file-level-metadata-file) (one)
- [Location metadata file](#locations-file) (one)
- [Sample ID and metadata file](#sample-id-and-metadata-file) (one)

## DATA FILES
- **Purpose:** provides measurement data for each sample.
- **Format:** comma-separated value (.csv)
- Use the template and term guide to structure data files.
    - Required fields include:
        - `sample_name`
        - `{measurement_column_name}`
        - `{measurement_column_name}_method_id`
    - Conditionally required fields include:
        - `time_elapsed`
             - Condition: Required for time series measurements on a single sample
    - Optional fields include:
        - `treatment_id`
        - `datetime_measured`**
        - `{measurement_column_name}_flag`
        - `notes`
- Include as many measurement columns/rows as desired. Each `{measurement_column_name}` must be defined in the data dictionary using the RF-specified fields.
- Method IDs, treatment IDs, and flags must be defined in the Methods and Attributes File. 
- If multiple method IDs or flags are provided in a single cell, they should be separated by a semicolon and space. 
- If data files contain time series measurements on a single sample, one sample is allowed per file and `time_elapsed` cannot have repeated values. 
- ** The related datetime of sample collection is reported as a required term in the Sample ID and Metadata file for the corresponding `sample_name`.

## METHODS AND ATTRIBUTES FILE
- **Purpose:** lists and describes `attr_id` (attribute ID), which include IDs used in the `*_method_id`, `*_flag`, and `treatment_id` data file columns.
- **Format:** comma-separated value (.csv)
- Use the template and term guide to generate a methods and attributes file. Name the file “`sample_attr.csv`” or with the suffix “`_sample_attr.csv`”. 
    - Required fields include:
        - `attr_id`
        - `attr_type`
        - `attr_description`
    - Optional fields include:
        - `analysis_detection_limit`
        - `analysis_precision`
        - `instrument_precision`
        - `lower_bound`
        - `upper_bound`
        - `method_instrument`
        - `method_reference`
        - `method_hold_time`
        - `method_temp`
        - `method_light`
        - `method_atmosphere`
        - `method_moisture`
        - `method_medium`
        - `method_time`
        - `method_lab_contact`
        - `method_instrument_operator`
        - `method_lab`
- The combination of `attr_id` and `attr_type` columns must be unique within the file.

## FILES GOVERNED BY OTHER REPORTING FORMATS
### DATA DICTIONARY FILES
- **Purpose:** lists and describes `column_or_row_name` to provide metadata for each column/row header.
- **Format:** comma-separated value (.csv)
- **Governed by:** File Level Metadata (FLMD) Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Full Reporting Format.
- Use the Sample Data - Full Reporting Format template to structure data dictionary (dd) files. The template includes original FLMD Reporting Format terms and extensions that build upon it. Use the Sample Data - Full Reporting Format term guide for descriptions and requirements; original FLMD terms that are not extended have links to the FLMD term guide. Extensions are marked with an asterisk below.
     - Required fields include:
          - `column_or_row_name`
          - `unit`*
          - `definition`*
          - `measured_variable`*
    - Optional fields include:
      - `column_or_row_long_name`
      - `data_type`*
      - `missing_value_code`*
      - `unit_basis`*
      - `statistic_measurement`*
      - `statistic_spatial`*
      - `statistic_temporal`*
      - `representation_temporal`*
      - `notes`*
- The data dictionary template includes definitions for the data file's required and optional terms. These definitions must be used as-is in the `definition` column when you create the data dictionaries for your data package.
- Column/row headers defined in the dd cannot be repeated in the same dd. If column/row headers have different metadata across data files, the data files must use separate dd files.
- If your dataset contains other data dictionaries, the data dictionaries associated with these Sample Data - Full Reporting Format files must be separate. 

### FILE LEVEL METADATA FILE
- **Purpose:** lists and describes `file_name` to provide metadata for each file.
- **Format:** comma-separated value (.csv)
- **Governed by:** FLMD Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Full Reporting Format.
- Use the Lite Sample Data Reporting Format template to structure FLMD files. The template includes original FLMD Reporting Format terms and extensions that build upon it. Use the Lite Sample Data Reporting Format term guide for descriptions and requirements; original FLMD terms that are not extended have links to the FLMD term guide. Extensions are marked with an asterisk below.
    - Required fields include:
        - `file_name`
        - `file_description`
        - `standard`*
        - `data_dictionary_file_name`*
    - Optional fields include:
        - `file_version`
        - `data_orientation` =  horizontal
        - `header_rows` = 1
        - `column_or_row_name_position` = 1
        - `notes`
- The data, methods and attributes, and data dictionary files listed in the FLMD should have “ESS-DIVE Sample Data - Full Reporting Format v1” listed in the `standard` column.
- If you include the optional fields `data_orientation`, `header_rows`, or `column_or_row_name_position`, report the values above for the files following this RF.

### LOCATIONS FILE
- **Purpose:** lists and describes location_id to provide metadata for each location.
- **Format:** comma-separated value (.csv)
- **Governed by:** Location Metadata Reporting Format available at https://github.com/ess-dive-workspace/essdive-location-metadata/tree/release-v2.0.0
- Additional requirements:
     - There must be a `location_id` entry (row) for every `Location ID` entered on the Sample ID and Metadata RF.
     - The `latitude` and `longitude` terms in the Location Metadata RF will be the primary source of location information if `Latitude` and `Longitude` are provided on the Sample ID and Metadata RF.

### SAMPLE ID AND METADATA FILE
- **Purpose:** lists and describes sample_name to provide metadata for each sample.
- **Format:** comma-separated value (.csv)
- **Governed by:** Sample ID and Metadata Reporting Format available at https://github.com/ess-dive-workspace/essdive-sample-id-metadata/tree/release-v2.0
- Additional requirements:
    - There must be a `Sample Name` entry (row) for every `sample_name` that is included in the data file(s).
    - `Location ID` must be provided for each sample and a corresponding entry for that location id must be provided in the Location Metadata RF.
    - If you are acquiring IGSN (International Generic Sample Number), you must enter the `Latitude` and `Longitude` (WGS84 datum) in both this Sample ID and Metadata RF and the Locations RF. If you are not acquiring IGSNs, you do not need to enter the `Latitude` and `Longitude` terms in the Sample ID and Metadata RF.
    - `Collection method description` is required. Any sample methods information must also be included in the methods information captured in the data file and methods and attributes file.
 
## ADDITIONAL CONSIDERATIONS
- You are encouraged to include raw data files, instrument specification PDFs from manufacturers, code used for data collection or data processing, and/or links to relevant content (i.e., GitHub, Zenodo). The RF does not provide specific guidance on formats of these additional files.
- If your data type cannot use a standard data csv structure (e.g., individual spectra files per sample), populate the methods and attributes file as you would for any other data type and populate a data file template that contains the required columns. This will allow for normal mapping to the other file types for data users; however, ESS-DIVE’s internal tools may not be able to use this information. In place of the column of data, the column should point to the file or folder of data. An example is below:
<img width="463" height="69" alt="Screenshot 2026-06-02 at 9 48 20 AM" src="https://github.com/user-attachments/assets/977ebaed-a7fd-44b0-bd2e-6f1d0f4d232c" />

