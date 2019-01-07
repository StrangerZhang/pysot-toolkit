# pysot-toolkit
The purpose of this repo is to provide evaluation API of Current Single Object Tracking Dataset, including

- [x] [VOT2016](http://www.votchallenge.net/vot2016/dataset.html)
- [x] [VOT2018](http://www.votchallenge.net/vot2018/dataset.html)
- [x] [VOT2018-LT](http://www.votchallenge.net/vot2018/dataset.html)
- [x] [OTB100(OTB2015)](http://cvlab.hanyang.ac.kr/tracker_benchmark/datasets.html)
- [x] [UAV123](https://ivul.kaust.edu.sa/Pages/Dataset-UAV123.aspx)
- [x] [NFS](http://ci2cv.net/nfs/index.html)
- [x] [LaSOT](https://cis.temple.edu/lasot/)
- [ ] [TrackingNet (Evaluation on Server)](https://tracking-net.org)
- [ ] [GOT-10k (Evaluation on Server)](http://got-10k.aitestunion.com)

## Install 


```bash
git clone https://github.com/StrangerZhang/pysot-toolkit
pip install -r requirements.txt
cd pysot/utils/
python setup.py build_ext --inplace
# if you need to draw graph, you need latex installed on your system
```

## Download Dataset

Download json files used in our toolkit [baidu pan](https://pan.baidu.com/s/1js0Qhykqqur7_lNRtle1tA)

1. Put CVRP13.json, OTB100.json, OTB50.json in OTB100 dataset directory (you need to copy Jogging to Jogging-1 and Jogging-2, and copy Skating2 to Skating2-1 and Skating2-2 or using softlink)

   The directory should have the below format

   | -- OTB100/

   ​	| -- Basketball

   ​	| 	......

   ​	| -- Woman

   ​	| -- OTB100.json

   ​	| -- OTB50.json

   ​	| -- CVPR13.json

2. Put all other jsons in the dataset directory like in step 1

## Usage

### 1. Evaluation on VOT2018(VOT2016)
```bash
cd /path/to/pysot-toolkit
python bin/eval.py \
	--dataset_dir /path/to/dataset/root \		# dataset path
	--dataset VOT2018 \				# dataset name(VOT2018, VOT2016)
	--tracker_result_dir /path/to/tracker/dir \	# tracker dir
	--trackers ECO UPDT SiamRPNpp 			# tracker names 

# you will see
------------------------------------------------------------
|Tracker Name| Accuracy | Robustness | Lost Number |  EAO  |
------------------------------------------------------------
| SiamRPNpp  |  0.600   |   0.234    |    50.0     | 0.415 |
|    UPDT    |  0.536   |   0.184    |    39.2     | 0.378 |
|    ECO     |  0.484   |   0.276    |    59.0     | 0.280 |
------------------------------------------------------------
```
### 2. Evaluation on OTB100(UAV123, NFS, LaSOT)

converted *.txt tracking results will be released soon 

```bash
cd /path/to/pysot-toolkit
python bin/eval.py \
	--dataset_dir /path/to/dataset/root \		# dataset path
	--dataset OTB100 \				# dataset name(OTB100, UAV123, NFS, LaSOT)
	--tracker_result_dir /path/to/tracker/dir \	# tracker dir
	--trackers SiamRPN++ C-COT DaSiamRPN ECO  \	# tracker names 
	--num 4 \				  	# evaluation thread
	--show_video_level \ 	  			# wether to show video results
	--vis 					  	# draw graph

# you will see (Normalized Precision not used in OTB evaluation)
-----------------------------------------------------
|Tracker name| Success | Norm Precision | Precision |
-----------------------------------------------------
| SiamRPN++  |  0.696  |     0.000      |   0.914   |
|    ECO     |  0.691  |     0.000      |   0.910   |
|   C-COT    |  0.671  |     0.000      |   0.898   |
| DaSiamRPN  |  0.658  |     0.000      |   0.880   |
-----------------------------------------------------

-----------------------------------------------------------------------------------------
|    Tracker name     |      SiamRPN++      |      DaSiamRPN      |         ECO         |
-----------------------------------------------------------------------------------------
|     Video name      | success | precision | success | precision | success | precision |
-----------------------------------------------------------------------------------------
|     Basketball      |  0.423  |   0.555   |  0.677  |   0.865   |  0.653  |   0.800   |
|        Biker        |  0.728  |   0.932   |  0.319  |   0.448   |  0.506  |   0.832   |
|        Bird1        |  0.207  |   0.360   |  0.274  |   0.508   |  0.192  |   0.302   |
|        Bird2        |  0.629  |   0.742   |  0.604  |   0.697   |  0.775  |   0.882   |
|      BlurBody       |  0.823  |   0.879   |  0.759  |   0.767   |  0.713  |   0.894   |
|      BlurCar1       |  0.803  |   0.917   |  0.837  |   0.895   |  0.851  |   0.934   |
|      BlurCar2       |  0.864  |   0.926   |  0.794  |   0.872   |  0.883  |   0.931   |
|      BlurCar3       |  0.867  |   0.937   |  0.802  |   0.901   |  0.839  |   0.931   |
|      BlurCar4       |  0.883  |   0.918   |  0.842  |   0.869   |  0.876  |   0.893   |
|      BlurFace       |  0.776  |   0.836   |  0.753  |   0.819   |  0.834  |   0.889   |
|       BlurOwl       |  0.804  |   0.889   |  0.757  |   0.829   |  0.792  |   0.917   |
|        Board        |  0.520  |   0.469   |  0.458  |   0.414   |  0.816  |   0.813   |
|        Bolt         |  0.663  |   0.890   |  0.721  |   0.893   |  0.647  |   0.890   |
|        Bolt2        |  0.623  |   0.844   |  0.656  |   0.852   |  0.567  |   0.817   |
|         Box         |  0.819  |   0.903   |  0.672  |   0.768   |  0.748  |   0.822   |
|         Boy         |  0.806  |   0.948   |  0.775  |   0.934   |  0.841  |   0.960   |
|        Car1         |  0.801  |   0.963   |  0.767  |   0.968   |  0.854  |   0.973   |
|        Car2         |  0.851  |   0.945   |  0.759  |   0.946   |  0.858  |   0.965   |
|        Car24        |  0.816  |   0.941   |  0.817  |   0.948   |  0.885  |   0.964   |
|        Car4         |  0.861  |   0.952   |  0.780  |   0.940   |  0.859  |   0.954   |
|       CarDark       |  0.775  |   0.955   |  0.782  |   0.952   |  0.860  |   0.967   |
|      CarScale       |  0.845  |   0.942   |  0.742  |   0.829   |  0.740  |   0.757   |
|       ClifBar       |  0.505  |   0.706   |  0.306  |   0.411   |  0.573  |   0.807   |
|        Coke         |  0.690  |   0.857   |  0.604  |   0.847   |  0.538  |   0.716   |
|       Couple        |  0.710  |   0.914   |  0.665  |   0.882   |  0.672  |   0.882   |
|       Coupon        |  0.835  |   0.945   |  0.845  |   0.933   |  0.885  |   0.929   |
|      Crossing       |  0.813  |   0.964   |  0.698  |   0.951   |  0.781  |   0.965   |
|       Crowds        |  0.725  |   0.921   |  0.677  |   0.921   |  0.702  |   0.916   |
|       Dancer        |  0.759  |   0.858   |  0.763  |   0.870   |  0.781  |   0.860   |
|       Dancer2       |  0.737  |   0.857   |  0.783  |   0.824   |  0.730  |   0.855   |
|        David        |  0.681  |   0.918   |  0.676  |   0.882   |  0.833  |   0.938   |
|       David2        |  0.673  |   0.926   |  0.725  |   0.943   |  0.836  |   0.970   |
|       David3        |  0.698  |   0.901   |  0.691  |   0.891   |  0.774  |   0.913   |
|        Deer         |  0.563  |   0.772   |  0.645  |   0.795   |  0.789  |   0.904   |
|       Diving        |  0.622  |   0.834   |  0.581  |   0.743   |  0.326  |   0.629   |
|         Dog         |  0.488  |   0.855   |  0.546  |   0.865   |  0.598  |   0.875   |
|        Dog1         |  0.848  |   0.952   |  0.816  |   0.944   |  0.800  |   0.908   |
|        Doll         |  0.812  |   0.924   |  0.745  |   0.901   |  0.842  |   0.941   |
|     DragonBaby      |  0.673  |   0.824   |  0.683  |   0.835   |  0.695  |   0.809   |
|        Dudek        |  0.870  |   0.893   |  0.824  |   0.820   |  0.815  |   0.819   |
|      FaceOcc1       |  0.590  |   0.455   |  0.657  |   0.648   |  0.781  |   0.747   |
|      FaceOcc2       |  0.550  |   0.828   |  0.623  |   0.805   |  0.767  |   0.852   |
|        Fish         |  0.812  |   0.916   |  0.794  |   0.899   |  0.849  |   0.926   |
|      FleetFace      |  0.809  |   0.828   |  0.713  |   0.747   |  0.735  |   0.650   |
|      Football       |  0.637  |   0.817   |  0.644  |   0.902   |  0.625  |   0.826   |
|      Football1      |  0.790  |   0.935   |  0.674  |   0.908   |  0.536  |   0.833   |
|      Freeman1       |  0.664  |   0.892   |  0.676  |   0.902   |  0.553  |   0.827   |
|      Freeman3       |  0.723  |   0.938   |  0.780  |   0.955   |  0.802  |   0.965   |
|      Freeman4       |  0.635  |   0.912   |  0.645  |   0.916   |  0.564  |   0.779   |
|        Girl         |  0.767  |   0.936   |  0.729  |   0.940   |  0.782  |   0.957   |
|        Girl2        |  0.585  |   0.669   |  0.623  |   0.727   |  0.655  |   0.718   |
|         Gym         |  0.657  |   0.852   |  0.693  |   0.838   |  0.486  |   0.813   |
|       Human2        |  0.777  |   0.816   |  0.748  |   0.766   |  0.792  |   0.797   |
|       Human3        |  0.738  |   0.930   |  0.750  |   0.911   |  0.612  |   0.903   |
|      Human4-2       |  0.705  |   0.920   |  0.361  |   0.476   |  0.622  |   0.938   |
|       Human5        |  0.771  |   0.927   |  0.749  |   0.866   |  0.737  |   0.911   |
|       Human6        |  0.739  |   0.880   |  0.694  |   0.790   |  0.782  |   0.894   |
|       Human7        |  0.838  |   0.947   |  0.789  |   0.928   |  0.836  |   0.950   |
|       Human8        |  0.805  |   0.956   |  0.735  |   0.928   |  0.740  |   0.947   |
|       Human9        |  0.812  |   0.955   |  0.687  |   0.935   |  0.801  |   0.946   |
|       Ironman       |  0.638  |   0.790   |  0.402  |   0.529   |  0.595  |   0.797   |
|      Jogging-1      |  0.637  |   0.906   |  0.655  |   0.913   |  0.770  |   0.889   |
|      Jogging-2      |  0.771  |   0.930   |  0.739  |   0.911   |  0.733  |   0.905   |
|        Jump         |  0.410  |   0.612   |  0.328  |   0.515   |  0.096  |   0.083   |
|       Jumping       |  0.649  |   0.869   |  0.529  |   0.852   |  0.707  |   0.928   |
|      KiteSurf       |  0.826  |   0.961   |  0.759  |   0.944   |  0.757  |   0.940   |
|       Lemming       |  0.775  |   0.895   |  0.756  |   0.840   |  0.817  |   0.882   |
|       Liquor        |  0.705  |   0.765   |  0.445  |   0.469   |  0.838  |   0.896   |
|         Man         |  0.830  |   0.955   |  0.827  |   0.951   |  0.825  |   0.962   |
|       Matrix        |  0.680  |   0.858   |  0.432  |   0.579   |  0.542  |   0.801   |
|       Mhyang        |  0.723  |   0.955   |  0.738  |   0.928   |  0.828  |   0.950   |
|    MotorRolling     |  0.636  |   0.702   |  0.645  |   0.772   |  0.094  |   0.060   |
|    MountainBike     |  0.785  |   0.915   |  0.797  |   0.912   |  0.680  |   0.797   |
|        Panda        |  0.625  |   0.918   |  0.562  |   0.911   |  0.396  |   0.852   |
|       RedTeam       |  0.721  |   0.942   |  0.696  |   0.940   |  0.687  |   0.937   |
|        Rubik        |  0.708  |   0.749   |  0.670  |   0.716   |  0.775  |   0.889   |
|       Shaking       |  0.793  |   0.893   |  0.796  |   0.892   |  0.780  |   0.865   |
|       Singer1       |  0.780  |   0.877   |  0.746  |   0.808   |  0.848  |   0.939   |
|       Singer2       |  0.665  |   0.627   |  0.628  |   0.670   |  0.737  |   0.804   |
|       Skater        |  0.738  |   0.873   |  0.731  |   0.867   |  0.592  |   0.819   |
|       Skater2       |  0.704  |   0.844   |  0.694  |   0.843   |  0.574  |   0.621   |
|      Skating1       |  0.306  |   0.383   |  0.343  |   0.409   |  0.495  |   0.853   |
|     Skating2-1      |  0.442  |   0.546   |  0.405  |   0.500   |  0.474  |   0.609   |
|     Skating2-2      |  0.447  |   0.443   |  0.548  |   0.549   |  0.381  |   0.242   |
|       Skiing        |  0.588  |   0.917   |  0.499  |   0.890   |  0.095  |   0.128   |
|       Soccer        |  0.456  |   0.686   |  0.193  |   0.287   |  0.613  |   0.812   |
|       Subway        |  0.768  |   0.945   |  0.782  |   0.938   |  0.719  |   0.937   |
|       Surfer        |  0.686  |   0.903   |  0.712  |   0.918   |  0.704  |   0.915   |
|         Suv         |  0.593  |   0.761   |  0.507  |   0.615   |  0.786  |   0.908   |
|      Sylvester      |  0.762  |   0.908   |  0.698  |   0.883   |  0.716  |   0.869   |
|       Tiger1        |  0.694  |   0.762   |  0.677  |   0.755   |  0.735  |   0.827   |
|       Tiger2        |  0.650  |   0.735   |  0.608  |   0.714   |  0.680  |   0.792   |
|         Toy         |  0.638  |   0.805   |  0.636  |   0.814   |  0.671  |   0.840   |
|        Trans        |  0.678  |   0.699   |  0.656  |   0.505   |  0.502  |   0.296   |
|       Trellis       |  0.743  |   0.906   |  0.684  |   0.836   |  0.770  |   0.942   |
|      Twinnings      |  0.723  |   0.928   |  0.641  |   0.860   |  0.626  |   0.784   |
|        Vase         |  0.564  |   0.698   |  0.554  |   0.742   |  0.544  |   0.752   |
|       Walking       |  0.761  |   0.956   |  0.745  |   0.932   |  0.709  |   0.955   |
|      Walking2       |  0.362  |   0.476   |  0.263  |   0.371   |  0.793  |   0.941   |
|        Woman        |  0.615  |   0.908   |  0.648  |   0.887   |  0.771  |   0.936   |
-----------------------------------------------------------------------------------------
```

|     OTB100 Success Plot   	    | OTB100 Precision Plot	    |
| --------------------------------- | ----------------------------- |
|![](figs/OTB100_succ.png)  	    |![](figs/OTB100_pre.png)  	    |

### 3. Evaluation on VOT2018-LT

```bash
cd /path/to/pysot-toolkit
python bin/eval.py \
	--dataset_dir /path/to/dataset/root \		# dataset path
	--dataset VOT2018-LT \				# dataset name
	--tracker_result_dir /path/to/tracker/dir \	# tracker dir
	--trackers SiamRPN++ MBMD DaSiam-LT \		# tracker names 
	--num 4 \				  	# evaluation thread
	--vis \					  	# wether to draw graph

# you will see
-------------------------------------------
|Tracker Name| Precision | Recall |  F1   |
-------------------------------------------
| SiamRPN++  |   0.649   | 0.610  | 0.629 |
|    MBMD    |   0.634   | 0.588  | 0.610 |
| DaSiam-LT  |   0.627   | 0.588  | 0.607 |
|    MMLT    |   0.574   | 0.521  | 0.546 |
|  FuCoLoT   |   0.538   | 0.432  | 0.479 |
|  SiamVGG   |   0.552   | 0.393  | 0.459 |
|   SiamFC   |   0.600   | 0.334  | 0.429 |
-------------------------------------------
```

![](./figs/VOT2018-LT.png)

## Get Tracking Results of Your Own Tracker

Add pysot-toolkit to your PYTHONPATH

```bash
export PYTHONPATH=/path/to/pysot-toolkit:$PYTHONPATH
```

### 1. OPE (One Pass Evaluation)

```python
from pysot.datasets import DatasetFactory

dataset = DatasetFactory.create_dataset(name=dataset_name,
                                       	dataset_root=datset_root,
                                        load_img=False)
for video in dataset:
    for idx, (img, gt_bbox) in enumerate(video):
        if idx == 0:
            # init your tracker here
        else:
            # get tracking result here
```

## 2. Restarted Evaluation

```python
from pysot.datasets import DatasetFactory
from pysot.utils.region import vot_overlap

dataset = DatasetFactory.create_dataset(name=dataset_name,
                                       	dataset_root=datset_root,
                                        load_img=False)
frame_counter = 0
pred_bboxes = []
for video in dataset:
    for idx, (img, gt_bbox) in enumerate(video):
        if idx == frame_counter:
            # init your tracker here
            pred_bbox.append(1)
        elif idx > frame_counter:
            # get tracking result here
            pred_bbox = 
            overlap = vot_overlap(pred_bbox, gt_bbox, (img.shape[1], img.shape[0]))
            if overlap > 0: 
	    	# continue tracking
                pred_bboxes.append(pred_bbox)
            else: 
	    	# lost target, restart
                pred_bboxes.append(2)
                frame_counter = idx + 5
        else:
            pred_bboxes.append(0)
```

