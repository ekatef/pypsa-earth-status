# PyPSA-Earth-Status: A package for validating any PyPSA network on Earth :D

## Development Status: **under development**

[![Test workflows](https://github.com/pypsa-meets-earth/pypsa-earth-status/actions/workflows/test.yaml/badge.svg)](https://github.com/pypsa-meets-earth/pypsa-earth/actions/workflows/test.yaml)
![Size](https://img.shields.io/github/repo-size/pypsa-meets-earth/pypsa-earth-status)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Discord](https://img.shields.io/discord/911692131440148490?logo=discord)](https://discord.gg/AnuJBk23FU)
[![Google Drive](https://img.shields.io/badge/Google%20Drive-4285F4?style=flat&logo=googledrive&logoColor=white)](https://drive.google.com/drive/folders/13Z8Y9zgsh5IZaDNkkRyo1wkoMgbdUxT5?usp=sharing)


**PyPSA-Earth-Status: A package for validating any PyPSA network on Earth**

PyPSA-Earth-Status is a GitHub repository designed to validate PyPSA networks against real-world energy system data. It provides automated procedures to compare user-provided PyPSA networks with state-of-the-art statistics from authoritative databases such as IRENA, IEA, and others.

By streamlining the validation process, PyPSA-Earth-Status helps modelers enhance the credibility, transparency, and quality of their modeling results -- saving time and allowing them to focus on what matters most: developing better energy system models.

🔍 Automated validation covers:

- **Installed capacities**: `p_nom` of generators and storage units
- **Optimized capacities**: `p_nom_opt` of generators and storage units
- **Transmission capacities**: `s_nom` of power lines
- **Demand**: comparison with real-world consumption data

💡 Energy modelers often face the challenge of validating their models to ensure accuracy and reliability. This collaborative project aims to make that process faster, easier, and more consistent across the community.

🤝 We warmly welcome contributions to expand the capabilities of PyPSA-Earth-Status and to build a shared foundation for model validation in open energy system research worldwide.

## Features
- Automated validation of PyPSA networks against real-world data
- Creation of reference statistics from leading databases:
  - Demand data from Our World in Data
  - Installed capacities from IRENA and IEA
  - Cross-border line capacities from [Global Transmission Database](https://zenodo.org/records/15527469)
- Comparison of network data with reference statistics
- Generation of tables and visualizations for easy interpretation of results

... and more features with your help!

## Installation

To install PyPSA-Earth-Status, simply clone the repository:

```bash
    git clone https://github.com/pypsa-meets-earth/pypsa-earth-status --recurse-submodules
```

The Python dependencies required to run the scripts are a proven subset of those used by PyPSA-Earth.
We recommend using the PyPSA-Earth environment, which provides OS-specific lock files for Conda.

For Linux, create the environment as follows:

```bash
    cd pypsa-earth-status
    conda env create -f workflows/pypsa-earth/envs/linux-64.lock.yaml
```

For other operating systems, use the corresponding lock file for your platform.
You can find all available lock files in: `workflows/pypsa-earth/envs/`. For example:
- `win-64.lock.yaml` for Windows,
- `osx-arm64.lock.yaml` for macOS platform arm64 (M1/M2)
- `osx-64.lock.yaml` for macOS platform x86_64 (Intel)

## Tutorial

To validate a first PyPSA network, you can run the following command in your terminal from the `pypsa-earth-status` folder:

```bash
    conda activate pypsa-earth
    snakemake -j 1 visualize_data
```

This command will:
1. Create the sample network scigrid_de from PyPSA
2. Save it as `resources/example_DE.nc` with minimal changes
3. Execute the typical validation procedure to produre tables and visualizations in the folder `results/` for easy inspection

## Execute your first custom validation

If you want to validate your own PyPSA network, you can:

1. Open the file `config.yaml` in the `pypsa-earth-status` folder
2. Specify the path to the network you want to validate in the field `network_path` under `network_validation`
3. Adapt the list of countries you want to validate in the field `countries` under `network_validation` using 2-letter code naming convention; please keep at least two neighbouring countries in the list, e.g. ['DE', 'FR'] for the tutorial case for Germany.
4. Execute:
    ```bash
        snakemake -j 1 visualize_data
    ```
5. Check the results in the `results/` folder
