# SLAM-Analysis-Tools
The repository contains instructions for Localization and Map Analysis.

Download & Install [EVO](https://github.com/MichaelGrupp/evo):
```
git clone https://github.com/MichaelGrupp/evo.git
cd ~/evo
pip2 install --editable . --upgrade --no-binary evo
```
Download the `bagmerge.py` file from this repository and put that inside `~/evo/test/data` directory. Merge 2 rosbag files:
```
cd ~/evo/test/data
python bagmerge.py gt_odometry.bag odometry.bag -o odometry_analysis.bag
```
## Trajectory Analysis and Plot:
```
cd ~/evo/test/data
evo_traj bag odometry_analysis.bag /odom --ref /gt_odom -va --plot --plot_mode=xyz
```
## Absolute Position Error (APE) Analysis, Plot and Save:
```
cd ~/evo/test/data
mkdir results
evo_ape bag odometry_analysis.bag /odom /gt_odom -va --plot --plot_mode=xyz --save_results results/odometry_analysis.zip
```
## Relative Position Error (RPE) Analysis, Plot and Save:
```
cd ~/evo/test/data
mkdir results
evo_rpe bag odometry_analysis.bag /odom /gt_odom -va --plot --plot_mode=xyz --save_results results/odometry_analysis.zip
```
## Post Result Analysis and Plot:
```
cd ~/evo/test/data
mkdir results
evo_res results/odometry_analysis.zip -p --save_table results/table.csv
```
