# Point registration via efficient convex relaxation
Implementation of the SIGGRAPH 2016 paper "Point registration via efficient convex relaxation"
Haggai Maron, Nadav Dym, Itay Kezurer, Shahar Kovalsky,Yaron Lipman 

Abstract
-------------
Point cloud registration is a fundamental task in computer graphics, and more specifically, in rigid and non-rigid shape matching.The rigid shape matching problem can be formulated as the problem of simultaneously aligning and labelling two point clouds in 3D so that they are as similar as possible. We name this problem the Procrustes matching (PM) problem. The non-rigid shape matching problem can be formulated as a higher dimensional PM problem using the functional maps method. High dimensional PM problems are difficult non-convex problems which currently can only be solved locally using iterative closest point (ICP) algorithms or similar methods. Good initialization is crucial for obtaining a good solution.

We introduce a novel and efficient convex SDP (semidefinite programming) relaxation for the PM problem. The algorithm is guaranteed to return a correct global solution of the problem when matching two isometric shapes which are either asymmetric or bilaterally symmetric.

We show our algorithm gives state of the art results on popular shape matching datasets. We also show that our algorithm gives
state of the art results for anatomical classification of shapes. Finally we demonstrate the power of our method in aligning shape collections.

Prerequisites:
--------------
1.) Yalmip
2.) Mosek
3.) Graph toolbox
4.) ANN libray - supplied - make sure you compile it.
5.) This code was tested on matlab 2015a on linux only.

Note: At the beginning of each of the files mentioned below you need to fill in the path of the prerequisites - just replace the addpath command to the corrrect one on your machine.

Quick start:
------------
1.) Run testPMSDP_synthetic - this file generates a synthetic point cloud registration problem, solves it, and compares the results to the ground truth.

2.) Run testPMSDP_scape - this file runs PM SDP on the scape dataset and saves the results. Two mehses are supplied with the code as an example. 
Download the full scape dataset (http://robotics.stanford.edu/~drago/Projects/scape/scape.html) in order to get all the meshes. 
These meshes need to be preprocessed before PM-SDP can use them. The preprocessing code as well as the shapes are in the /shapes directory. 
The function "preprocessMeshesInFolder" runs preprocessing on all meshes in a folder and saves a .mat file containig data for each mesh. 
Two example meshes and their mat files are supplied as an example.
The function "runAllScape" runs on all the scape dataset.

2.) Run testPMSDP_faust - this file runs PM SDP on the FAUST dataset and saves the results.
We use the preprocessed pointcloud of [Chen and Koltun, 2015] so their code/pointclouds are needed (can be downloaded from: web.stanford.edu/~cqf/convex).
You should download their code and the FAUST dataset, and add the data in the "training" folder to you matlab path.
The biggest difference between running on SCAPE and FAUST is way we generate the Laplacian: 
for SCAPE we simply use the cot Laplacian, while for FAUST we build the laplacian using the geodesics matrix (see constructLaplacianFromGeoMat.m).

3.) Run testPMSDP_scapeRawScans - this file runs PM SDP on the SCAPE raw scans dataset and saves the results.
A prerequisite is to preprocess this dataset using Chen and Koltun's preprocessing code and put the point clouds and geodesic matrices in the matlab path. 
Also note that the regular SCAPE dataset is needed for error validation. The file outputs a .cor file that can be used for error evaluation using Kim et al. 2011 code 
(https://www.cs.princeton.edu/~vk/projects/CorrsBlended/doc_data.php)

Disclaimer:
-----------------
The code is provided as-is for academic use only and without any guarantees. Please contact the authors to report any bugs.


Contact:
---------
haggaimaron@gmail.com
