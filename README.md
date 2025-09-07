# Balancing Profitability and Resilience to Earthquake-Induced Isolation: A Multi-Objective Optimization for Drone Depot Location

**Authors:** Yusuke Takahashi, Hiroki Takahashi

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)


## 1. Setup and Installation

### 1.1. Clone Repository

```bash
git clone git@github.com:h-takahashi-lab/drone_risk_profit_tradeoff.git
cd drone_risk_profit_tradeoff
```

# Balancing Profitability and Resilience to Earthquake-Induced Isolation: A Multi-Objective Optimization for Drone Depot Location

**Authors:** Yusuke Takahashi, Hiroki Takahashi

[![License: CC BY-NC 4.0](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc/4.0/)


## Abstract

Drone delivery networks possess a unique dual-use potential, enhancing commercial profitability during normal operations while providing critical logistics support for disaster resilience. While existing models often address these objectives separately or rely on abstract risk metrics, this study develops a multi-objective optimization model to strategically locate drone depots that explicitly accounts for the risk of community isolation following earthquakes. Our mixed-integer linear programming model quantifies the resilience objective by integrating a physics-based risk assessment that connects seismic shaking and topography to landslide probability and road failure, ultimately estimating community isolation risk. Applying the model to a case study in Japan, we derive a Pareto frontier demonstrating that a significant reduction in expected isolated population is achievable with only a minor sacrifice in profit. Furthermore, our sensitivity analysis reveals that increasing the number of depots qualitatively shifts the optimal deployment strategy from a general compromise to a specialized approach, balancing profit-focused and resilience-focused depots. This framework provides a quantitative tool for public and private decision-makers to design economically viable and socially robust dual-use logistics networks.


## 1. Setup and Installation

### 1.1. Clone Repository

```bash
git clone git@github.com:h-takahashi-lab/drone_risk_profit_tradeoff.git
cd drone_risk_profit_tradeoff
```

### 1.2. Install Dependencies

It is recommended to create a Python virtual environment before installing dependencies.

```bash
# Example using venv on macOS/Linux
python3 -m venv venv
source venv/bin/activate

# Install required packages
pip install -r requirements.txt
```

## 2. Data Preparation

The analysis code requires several external datasets to run. These datasets are not included in this repository (`data/` folder is ignored by `.gitignore`) and must be downloaded manually from their respective sources.

### Expected Directory Structure

After downloading and extracting all necessary data, your `data/` directory should have the following structure. The filenames listed below are examples provided in the project description and may vary based on specific downloads.

```text
repository_root/
├── data/
│   ├── agricultural_settlements/
│   │   └── MA0001_2015_2015_08/     
│   ├── DEM250/
│   │   └── G04-d-11_5339-jgd_GML/   
│   │   └── G04-d-11_5340-jgd_GML/   
│   │   └── G04-d-11_5439-jgd_GML/   
│   │   └── G04-d-11_5440-jgd_GML/   
│   │   └── G04-d-11_5540-jgd_GML/   
│   │   └── G04-d-11_5541-jgd_GML/   
│   ├── jshis_pgv/
│   │   └── P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5339/ 
│   │   └── P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5340/ 
│   │   └── P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5439/ 
│   │   └── P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5440/ 
│   │   └── P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5540/ 
│   ├── mesh/
│   │   └── SDDSWS5339/             
│   │   └── SDDSWS5340/    
│   │   └── SDDSWS5439/    
│   │   └── SDDSWS5440/    
│   │   └── SDDSWS5540/    
│   └── population/
│       └── tblT001140S5339/         
│       └── tblT001140S5340/         
│       └── tblT001140S5439/         
│       └── tblT001140S5440/         
│       └── tblT001140S5540/         
├── notebooks/
│   ├── prepare_data.ipynb
│   ├── run_optimization.ipynb
│   ├── visualize_data.ipynb
│   ├── visualize_results.ipynb
└── README.md
```


### Data Sources and Placement Instructions 

1.  **Agricultural Settlements Data (農業集落データ)**
    * **Source:** Ministry of Agriculture, Forestry and Fisheries, Japan (農林水産省) - [e.g., Agricultural Census](https://www.maff.go.jp/j/tokei/)
    * **Instructions:** Download the agricultural settlement boundary data. Unzip if necessary, and place the relevant files/folders (e.g., `MA0001_2015_2015_08`) into the `data/agricultural_settlements/` directory.

2.  **Digital Elevation Model (DEM) (数値標高モデル)**
    * **Source:** National Land Numerical Information database (国土数値情報ダウンロードサービス) - [GSI Japan](https://nlftp.mlit.go.jp/ksj/gml/datalist/KsjTmplt-G04-d.html)
    * **Instructions:** Download elevation and slope angle mesh data. Unzip if necessary, and place the relevant files/folders (e.g., `G04-d-11_5339-jgd_GML`) into the `data/DEM250/` directory.

3.  **Seismic Hazard Data (PGV) (地震ハザードデータ)**
    * **Source:** Japan Seismic Hazard Information Station (J-SHIS) - [NIED](https://www.j-shis.bosai.go.jp/download)
    * **Instructions:** Download probabilistic seismic hazard map data (e.g., PGV with 50-year exceedance probability). Unzip if necessary, and place relevant files/folders (e.g., `P-Y2020-MAP-AVR-TTL_MTTL-SHAPE-5339`) into the `data/jshis_pgv/` directory.

4.  **Standard Regional Mesh Data (標準地域メッシュ境界)**
    * **Source:** Statistics Bureau of Japan (e-Stat) - [Portal Site of Official Statistics of Japan](https://www.e-stat.go.jp/gis/statmap-search?type=1)
    * **Instructions:** Download the standard regional mesh **boundary data (Shapefile)**. Unzip if necessary, and place the relevant files/folders (e.g., `SDDSWS5339`) into the `data/mesh/` directory.

5.  **Population Data (人口統計データ)**
    * **Source:** Statistics Bureau of Japan (e-Stat) - [Portal Site of Official Statistics of Japan](https://www.e-stat.go.jp/gis/statmap-search?type=1)
    * **Instructions:** Download the corresponding **statistical data** for the mesh (e.g., 2020 Population Census). Unzip if necessary, and place the relevant files/folders (e.g., `tblT001140S5339`) into the `data/population/` directory.


## 3. Usage: Running the Analysis

The core analysis is contained within the Jupyter Notebooks located in the `notebooks/` directory.

**Execution Order:**
It is recommended to run the notebooks in the following order: prepare_data.ipynb,run_optimization.ipynb, visualize_data.ipynb, visualize_results.ipynb.

**Note on Language:** Please be aware that the comments and markdown text within the Jupyter Notebooks (`.ipynb` files) currently contain explanations primarily in Japanese. We plan to translate these in a future commit to improve accessibility for English-speaking users.


## 4. Citation

This research is currently being prepared for submission to a peer-reviewed journal. If you wish to use or reference this work before publication, please cite this repository directly or contact the corresponding author.

A formal citation and BibTeX entry will be provided here upon acceptance of the paper.



## 5. License

This project is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)**. See the `LICENSE` file for details.

You are free to share and adapt this material for non-commercial purposes, provided you give appropriate credit.

