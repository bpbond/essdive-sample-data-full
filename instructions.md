# Instructions

## SCOPE
- The Sample Data - Full Reporting Format is intended for data-generated in a laboratory from physical samples. This can include a set of individual samples or a time series of measurements on a single sample.
- This reporting format (RF) provides guidance on file structure and contents for data and metadata. It includes a term guide, templates, examples, and several controlled vocabularies.
- To be compliant with this RF, you must also adhere to the requirements in the [CSV](https://github.com/ess-dive-workspace/essdive-csv-structure), [File Level Metadata](https://github.com/ess-dive-workspace/essdive-file-level-metadata), [Location Metadata](https://github.com/ess-dive-workspace/essdive-location-metadata/tree/release-v2.0.0), and [Sample ID and Metadata](https://github.com/ess-dive-workspace/essdive-sample-id-metadata/tree/release-v2.0) Reporting Formats, as detailed below. 
- A simpler version of this reporting format ([Sample Data - Lite](https://github.com/ess-dive-workspace/essdive-sample-data-lite/tree/release-v1.0.0)) is also available for laboratory-generated sample data. 
    - This Full version supports more detailed metadata and provides flexibility to describe more approaches. For example, sample tracking, named locations, non-point locations, and complex / detailed methods are supported. 
    - The Lite version supports less detailed metadata and only common approaches. For example, point locations in only WGS84 datum and high-level methods are supported; sample tracking is not supported.

## CHECKLIST FOR SUBMISSION
- [Data file(s)](#data-files) (as many as needed)
- [Methods and attributes file](#methods-and-attributes-file) (one)
- [Data dictionary file(s)](#data-dictionary-files) (as many as needed)
- [File level metadata file](#file-level-metadata-file) (one)
- [Location metadata file](#locations-file) (one)
- [Sample ID and metadata file](#sample-id-and-metadata-file) (one)

## DATA FILES
- **Purpose:** provides measurement data for the sample(s).
- **Format:** comma-separated value (.csv)
- Use the template and term guide to structure data files.
    - Required terms include:
        - `sample_name`
        - `common_method_id`
        - `{measurement_column_name}`
    - Conditionally required terms include:
        - `time_elapsed`
             - Condition: Required for time series measurements on a single sample
    - Optional terms include:
        - `treatment_id`
        - `datetime_measured`**
        - `{measurement_column_name}_method_id`
        - `{measurement_column_name}_flag`
        - `common_flag`
        - `notes`
- ** `datetime_measured` is an optional term in the data file, while `datetime_collected` is a required term in the Sample ID and Metadata file for the corresponding `sample_name`. See term guide for details.
- Include as many measurement columns as desired. Each `{measurement_column_name}` must be defined in the data dictionary.
- Method IDs, treatment IDs, and flags must be defined in the Methods and Attributes File. 
- If multiple method IDs or flags are provided in a single cell, they should be separated by a semicolon and space. 
- If data files contain time series measurements on a single sample, each file can only contain a time series for one sample. The column required for a time series (`time_elapsed`) cannot have repeated values. 

## METHODS AND ATTRIBUTES FILE
- **Purpose:** lists and describes `attr_id` (attribute ID), which includes IDs used in the `*_method_id`, `*_flag`, and `treatment_id` data file columns.
- **Format:** comma-separated value (.csv)
- Use the template and term guide to generate a methods and attributes file. Name the file “`sample_attr.csv`” or with the suffix “`_sample_attr.csv`”. 
    - Required terms include:
        - `attr_id`
        - `attr_type`
        - `attr_description`
    - Optional terms include:
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
- The `attr_id` must be unique within the file.
- The optional terms you choose to populate should be determined by the `attr_type` for which you are providing information. For example, `treatment_id` is unlikely to have `analysis_detection_limit`, `analysis_precision`, `instrument_precision`, etc. populated.
- The division of what is considered `method_id` versus `flag` versus `treatment_id`information is dependent upon the data and the research purpose(s). For example, a user might choose to put all methods information together in a `method_id` and not use the other `attr_type` options. A user might choose to use one `method_id` for an overall summary of the method and then further contextualize that information with a separate `method_id` for each instrument that was used.

## FILES GOVERNED BY OTHER REPORTING FORMATS
### DATA DICTIONARY FILES
- **Purpose:** lists and describes `column_or_row_name` to provide metadata for each column header.
- **Format:** comma-separated value (.csv)
- **Governed by:** File Level Metadata (FLMD) Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Full Reporting Format.
- Use the Sample Data - Full Reporting Format template to structure data dictionary (DD) files. Name the file “`dd.csv`” or with the suffix “`_dd.csv`”. See the term guide for term descriptions and requirements. _Extension (new) or modified terms that build on the dd structure governed by the FLMD Reporting Format are marked with a plus below._
     - Required terms include:
          - `column_or_row_name`
          - `unit`+
          - `definition`+
          - `measured_variable`+
    - Optional terms include:
      - `material_measured`+
      - `column_or_row_long_name`
      - `data_type`+
      - `missing_value_code`+
      - `unit_basis`+
      - `representation_temporal`+
      - `statistic_measurement`+
      - `statistic_measurement_number`+
      - `statistic_spatial`+
      - `statistic_spatial_number`+
      - `statistic_temporal`+
      - `statistic_temporal_number`+
      - `statistic_detail`+
      - `notes`+
- The data dictionary template includes definitions for the data file's required and optional terms. These definitions must be used as-is in the `definition` column when you create the data dictionaries for your data package.
- Column names (`column_or_row_name`) defined in the DD cannot be repeated in the same DD.
    - If column headers have different metadata across data files (e.g., a different unit or definition) but the column name does not change, the data files must use separate DD files, i.e., there must be a specific DD file per data file.
- If your dataset contains other data dictionaries, the data dictionaries associated with these Sample Data - Full Reporting Format files must be separate.

### FILE LEVEL METADATA FILE
- **Purpose:** lists and describes `file_name` to provide metadata for each file.
- **Format:** comma-separated value (.csv)
- **Governed by:** FLMD Reporting Format available at https://github.com/ess-dive-workspace/essdive-file-level-metadata, with required modifications detailed in this Sample Data - Full Reporting Format (see details below).
- Use the Sample Data - Full Reporting Format template to structure file level metadata (FLMD) file. Name the file “`flmd.csv`” or with the suffix “`_flmd.csv`”. See the term guide for term descriptions and requirements. _Extension (new) or modified terms that build on the FLMD structure governed by the FLMD Reporting Format are marked with a plus below._
    - Required terms include:
        - `file_name`
        - `file_description`
        - `standard`+
        - `data_dictionary_file_name`+
    - Optional terms include:
        - `file_version`
        - `data_orientation`
        - `header_rows`
        - `column_or_row_name_position`
        - `notes`
- The data, methods and attributes, and data dictionary files listed in the FLMD should have “ESS-DIVE Sample Data - Full Reporting Format v1” listed in the `standard` column.
- If you include the optional terms `data_orientation`, `header_rows`, or `column_or_row_name_position`, the reported values should be “horizontal”, “1”, and “1”, respectively, for the files following this RF.

### LOCATIONS FILE
- **Purpose:** lists and describes `location_id` to provide metadata for each location.
- **Format:** comma-separated value (.csv)
- **Governed by:** Location Metadata Reporting Format available at https://github.com/ess-dive-workspace/essdive-location-metadata/tree/release-v2.0.0
- Additional requirements:
     - There must be a `location_id` entry (row) for every `Location ID` entered on the Sample ID and Metadata RF.

### SAMPLE ID AND METADATA FILE
- **Purpose:** lists and describes `sample_name` to provide metadata for each sample.
- **Format:** comma-separated value (.csv)
- **Governed by:** Sample ID and Metadata Reporting Format available at https://github.com/ess-dive-workspace/essdive-sample-id-metadata/tree/release-v2.0
- Additional requirements:
    - There must be a `Sample Name` entry (row) for every `sample_name` that is included in the data file(s).
    - `Location ID` must be provided for each sample and a corresponding entry for that `location_id` must be provided in the Location Metadata RF.
    - If you are acquiring IGSNs (International Generic Sample Number), you must enter the `Latitude` and `Longitude` (WGS84 datum) in both this Sample ID and Metadata RF and the Locations RF. If you are not acquiring IGSNs, you do not need to enter the `Latitude` and `Longitude` terms in the Sample ID and Metadata RF. The `latitude` and `longitude` terms in the Location Metadata RF will be the primary source of location information, even if `Latitude` and `Longitude` are provided on the Sample ID and Metadata RF.
    - `Collection method description` is required. `Collection method description` should only describe the methods used in the field to collect the sample. Any laboratory methods should be included in the methods attribute file.
 
## ADDITIONAL CONSIDERATIONS
- You are encouraged to include raw data files, instrument specification PDFs from manufacturers, code used for data collection or data processing, and/or links to relevant content (i.e., GitHub, Zenodo). The RF does not provide specific guidance on formats of these additional files.
- If your data type cannot use a standard data csv structure (e.g., individual spectra files per sample), populate the methods and attributes file as you would for any other data type and populate a data file template that contains the required columns. This will allow for normal mapping to the other file types for data users; however, ESS-DIVE’s internal tools may not be able to use this information. In place of the column of data, the column should point to the file or folder of data. An example is below:
<img width="463" height="69" alt="Screenshot 2026-06-02 at 9 48 20 AM" src="https://github.com/user-attachments/assets/977ebaed-a7fd-44b0-bd2e-6f1d0f4d232c" />

