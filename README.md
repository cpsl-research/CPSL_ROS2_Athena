# CPSL_ROS2_Athena
A collection of ROS2 packages for the athena demo

## Software Notes

The following code was used to implement a set of nodes for the Athena demo applicatoin. The specific software versions used are as follows:

- Gazebo Version (if simulating): GZ Harmonic
- ROS Version: ROS2 Jazzy
- Ubuntu Version: Ubuntu 24.04
- Python Version: Python 3.12

## Installation
In order for the code to work properly, the following steps are required
1. Install the virtual environment for CPSL_ROS2_Athena using Poetry
2. Install the ROS2 nodes as required



### 1. Clone CPSL_ROS2_PC_Processing
```
git clone https://github.com/cpsl-research/CPSL_ROS2_Athena
```
Initialize the submodules
```
cd CPSL_ROS2_Athena
git submodule update --init
```
### 2. Install CPSL_ROS2_Athena using Poetry

#### Installing Poetry 1.8.4:
 
1. Check to see if Python Poetry is installed. If the below command is successful, poetry is installed move on to setting up the conda environment

```
    poetry --version
```
2. If Python Poetry is not installed, follow the [Poetry Install Instructions](https://python-poetry.org/docs/#installing-with-the-official-installer). On linux, Poetry can be installed using the following command:
```
curl -sSL https://install.python-poetry.org | python3 - --version 1.8.4
```

If you are using poetry over an ssh connection or get an error in the following steps, try running the following command first and then continuing with the remainder fo the installation.
```
export PYTHON_KEYRING_BACKEND=keyring.backends.null.Keyring
```
#### Installing CPSL_ROS2_PC_Processing

To install the package using poetry, use the following steps
1. Configure poetry projects to be able to use the system packages
```
poetry config virtualenvs.options.system-site-packages true
```

2. Install the virtual environment
```
cd CPSL_ROS2_Athena
poetry install --extras "submodules"
```

#### Updating CPSL_ROS2_Athena
If the pyproject.toml file is updated, the poetry installation must also be updated. Use the following commands to update the version of poetry
```
poetry lock --no-update
poetry install
```

### 3. Building ROS2 nodes
To build the ROS2 nodes, complete the following steps:
1. go into the CPSL_ROS2_PC_Processing directory
```
cd CPSL_ROS2_PC_Processing
```
2. activate the poetry shell
```
poetry shell
```
3. install the package
```
python -m colcon build --symlink-install
```
4. Once complete source the setup.bash file
```
source install/setup.bash
```

## Tutorials

### 1. Running the ROS2 nodes on a UGV
To run the ROS2 nodes for the CPSL_ROS2_PC_Processing packages, complete the following steps:
1. go into the CPSL_ROS2_PC_Processing directory
```
cd CPSL_ROS2_PCProcessing
```
2. activate the poetry shell
```
poetry shell
```
4. Source the setup.bash file
```
source install/setup.bash
```
5. Finally, launch the ugv_gnn_bringup file
```
ros2 launch pc_processing ugv_gnn_bringup.launch.py
```

When launching, the following parameters can also be set by using the `parameter:=value` notation after the name of the launch file:
| **Parameter** | **Default** | **Description** |
|----------------|--------------|------------------------------------------------------|
|`namespace`|''|The robot's namespace|
|`param_file`| 'ugv_gnn.yaml'|YAML file with parameters for the nodes in the configs directory|
|`model_state_dict`| 'Sage_10fp_20fh_0_50_th_5mRng_0_2_res.pth'|.pth config file in the model_state_dicts folder|
|`scan_enable`| 'false'|If enabled, additionally publish a /LaserScan message on the radar_combined/scan topic|


### Using .env for Project Directories

In order to use any datasets in your computer's directory, you must first create a .env file and mark where the dataset files can be found.

1. Create a .env file in your project's root directory. This will file will not be uploaded to GitHub when you commit your changes.
2. Inside the .env file, add these variables
```
DATASET_DIRECTORY=/data/radnav/rad_nav_datasets/
MODEL_DATASET_DIRECTORY=/data/radnav/
MAP_DIRECTORY=/data/radnav/maps/
CONFIG_DIRECTORY=/home/USERNAME/Documents/odometry/submodules/mmwave_radar_processing/configs/
MOVIE_TEMP_DIRECTORY=/home/USERNAME/Downloads/radnav_temp_dir
RADCLOUD_MODEL_STATE_DICT_PATH=/home/USERNAME/Documents/odometry/submodules/radcloud/working_dir/RadCloud_40_chirps_10e.pth
RADARHD_MODEL_STATE_DICT_PATH=/data/RadarHD/radarhd_dict.pt_gen
```
3. Replace the example text with the path to your directory

## Loading the radarHD model

```
https://drive.google.com/file/d/1JorZEkDCIcQDSaMAabvkQX4scvwj0wzn/view?usp=sharing
```