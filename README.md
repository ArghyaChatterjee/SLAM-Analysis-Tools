# SLAM-Analysis-Tools
The repository contains instructions for Localization and Map Analysis.

# Localization Analysis
## [EVO](https://github.com/MichaelGrupp/evo) Download and Install:
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
evo_ape bag odometry_analysis.bag /gt_odom /odom -va --plot --plot_mode=xyz --save_results results/odometry_analysis.zip
```
## Relative Position Error (RPE) Analysis, Plot and Save:
```
cd ~/evo/test/data
mkdir results
evo_rpe bag odometry_analysis.bag /gt_odom /odom -va --plot --plot_mode=xyz --save_results results/odometry_analysis.zip
```
## Post Result Analysis and Plot:
```
cd ~/evo/test/data
mkdir results
evo_res results/odometry_analysis.zip -p --save_table results/table.csv
```
## Rosbag to Text File Conversion (Optional):
```
rostopic echo -b odometry_analysis.bag -p /odom > odom.txt
```
# Map Analysis
## CloudCompare Download and Install
Run the following command inside terminal:
```
sudo snap install cloudcompare
```
## Convert PCD files to PLY
You need to download pcl-tools to convert .pcd files to .ply files.
```
sudo apt install pcl-tools
```
Now, go to the directory where the map and reference ground truth map is located. Then run in the terminal:
```
pcl_pcd2ply map.pcd map.ply
pcl_pcd2ply gt_map.pcd gt_map.ply
```
## Compare with CloudCompare
Run Cloud compare by typing the following command inside terminal:
```
cloudcompare.CloudCompare
```
Open the two ply files. Just drag and drop them inside Cloud Compare one by one. Select both of them one by one (hold ctrl key) to activate distance compare button on top. 

## Follow Instructions from Cloud Compare
Follow [these instructions](https://www.cloudcompare.org/doc/wiki/index.php?title=Cloud-to-Cloud_Distance) to compute point to point distance. Remember that the compared is 'map.ply and the reference is 'gt_map.ply'. After you have imported 2 pointcloud, click on compute to compute the distance.

## Visualize Error
You can see the Mean Distance and Standard Deviation on the bottom console. Select `map.ply` from 'DB Tree' (upper left pane) and activate the colour bar from 'Properties' (lower left pane), change the background (Display--> Display Settings--> Colors and Materials--> Colors--> Background) and hide the `gt_map.ply` from 'DB Tree'. Hide the centre '+' sign from Display--> Toggle Viewer Based Perspective.

