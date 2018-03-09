# Auto Complete Graph (ACG).


Using emergency maps to help robots save you in emergencies

## Description

The goal of this program is described [in this blog post](https://malcolmmielle.wordpress.com/2017/08/07/using-emergency-maps-to-help-robots-save-you-in-emergencies/) and can be summarized by this sentence:

> a method to integrate an emergency map into a robot map, so that the robot can plan its way toward places it has not yet explored.

![Result example](https://raw.githubusercontent.com/MalcolmMielle/Auto-Complete-Graph/SSRR2017/Images/result.png)

## Paper

The auto complete graph method is presented in [this article](https://www.arxiv.org/abs/1702.05087) on arxiv and on [IEEE Xplore](http://ieeexplore.ieee.org/abstract/document/8088137/?reload=true). The paper was awarded `Best Student Paper Award` at `SSRR2018` so hopefully you'll enjoy reading it :).

```
@INPROCEEDINGS{8088137,
author={M. Mielle and M. Magnusson and H. Andreasson and A. J. Lilienthal},
booktitle={2017 IEEE International Symposium on Safety, Security and Rescue Robotics (SSRR)},
title={SLAM auto-complete: Completing a robot map using an emergency map},
year={2017},
volume={},
number={},
pages={35-40},
keywords={SLAM (robots);graph theory;mobile robots;rescue robots;robot vision;SLAM auto-complete;aerial images;emergency map;graph-based SLAM;rescue missions;robot mapping;Buildings;Covariance matrices;Navigation;Simultaneous localization and mapping;Strain;Uncertainty},
doi={10.1109/SSRR.2017.8088137},
ISSN={},
month={Oct},}
```


## Run the code example

This should all be soon ros parameters but for now here is how you can test the code:

* Use `roslaunch ndt_feature gustav_radar_tf.launch` to create the ndt_graph that is going to be processed by the ACG. Modify the file so that it reads your bag file. Use this [bag file](http://aass.oru.se/Research/mro/data/tutorials/mapping.bag) if your only testing the algorithm.

* The parameters for ACG are loaded from a file. The file is determined by a string in `acg_node_review.cpp` named `parameters_for_ACG`. An example of parameter file is present in `ACG_params/param.txt`

* Use `rosrun auto_complete_graph acg_node_review` to run the algorithm.

* In Rviz, one can give an approximation of the position of the prior compared to robot map using the Publish point button. Only two links are needed to initialize.

### How to use your own prior

The class `PriorLoaderInterface.hpp` is used to load prior image and detected corners. Just inherit from this class to create your own prior loader. See an example in the class `basementFull.hpp`. This only argument needed for PriorLoaderInterface is the name of the file image where the prior is.

## Dependencies

* [BetterGraph](https://github.com/MalcolmMielle/BetterGraph)
* [VoDiGrEx](https://github.com/MalcolmMielle/VoDiGrEx)
* [G2O](https://github.com/RainerKuemmerle/g2o) but please use my fork for now. G2O code base changed in the meantime.
* [perception_oru](https://github.com/OrebroUniversity/perception_oru) Since the code here getting old and the new version is not available yet, I think this commit 5d6a7f6b6c9e04b4eaadce802c04c6ad8cf23084 should be where they are synchronised
* [ndt_feature](https://github.com/MalcolmMielle/ndt_feature_graph)
* [occupancy_grid_utils](https://github.com/clearpathrobotics/occupancy_grid_utils)
* [grid_map](https://github.com/ethz-asl/grid_map)
* OpenCV
* Eigen
* Boost

