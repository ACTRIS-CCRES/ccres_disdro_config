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
