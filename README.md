# Configuration files for CCRES disdro processing

## Naming of files

TOML configuration for the [ccres_disdro_processinf](https://github.com/ACTRIS-CCRES/ccres_disdrometer_processing) are store in the `conf_stations` directory.

Files have to be names `conf_[station]_[radar-disdro].toml` where:
- `station` is the station name of the station in cloudnet vocabulary. A list of stations can be found with the command below:

    ```bash
    curl https://cloudnet.fmi.fi/api/sites | jq '.[] | select(.actrisId != null)'
    ```

- `radar-disdro` is the name of the radar and disdrometer in cloudnet vocabulary.

    - to get the list of available name for radar

        ```bash
        curl https://cloudnet.fmi.fi/api/instruments | jq ' .[] | select(.type == "radar")'
        ```

    - to get the list of available name for radar

        ```bash
        curl https://cloudnet.fmi.fi/api/instruments | jq ' .[] | select(.type == "disdrometer")'
        ```

## Content of the files

Every parameter of the processing is read in the station file : the package holds no default value, and each command stops with the list of the missing, unknown or invalid keys. Besides `[location]`, `[methods]`, `[instrument_parameters]`, `[thresholds]` and `[nc_meta]`, each file holds the sections `[disdrometer_interval]`, `[disdrometer_axis_check]`, `[radar_alignment]`, `[saturation]` and `[gate_check]` (with its selection levels `[gate_check.levels.<name>]`, from the most lenient to the most demanding). `[instrument_parameters]` gives `DD_TIMESTAMP_CONVENTION` (`"end"`, or `"start"` when the disdrometer time marks the start of its measurement interval) and `KW_SQR`, the |K|² the radar uses to compute Ze (0.93 in X band, 0.88 in Ka band, 0.74 in W band). The sections are described in the documentation of ccres_disdrometer_processing.

These sections need ccres_disdrometer_processing 1.3.0 or later, which also rejects the keys of older files (`REFRACTION_INDEX`, `RADAR_FREQUENCIES`, `COMPUTE_MIE_METHOD`, `PR_SAMPLING`).
