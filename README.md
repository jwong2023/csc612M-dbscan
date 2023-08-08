**Accelerating Geospatial DBSCAN Clustering Based on Vincenty Distance**

DBSCAN clustering is a commonly used clustering algorithm that focuses on spatial differences among points. This implementation replaces the standard Euclidean Distance with Vincenty Distance for measuring the geospatial distance between two points. Vincenty Distance is shown to be a more accurate distance computation between geospatial points as it factors in the ellipsoidal nature of the earth.


**C++ Google Colaboratory:**

https://colab.research.google.com/drive/107is7gc2OJ8X7k843CQ-ki891RdoC9AA?usp=sharing#scrollTo=Aa1IdekgYUcb

**CUDA Google Colaboratory:**

https://colab.research.google.com/drive/1uXOLtt-eOH6h_w-r-gZJbtKAhW_3atC7?usp=sharing#scrollTo=nC9lKZQUkZaY


**Parallel algorithms implemented:**

DBSCAN calls the function gather_points which starts the process for computing Vincenty distance. The CUDA implementation parallelizes this section and calculates the distance for several points faster than typical serial operations.


**Execution time comparison between sequential and parallel**

| Number of Coordinates | C++ Run Time | CUDA Run Time | Performance |
| --- | --- | --- | --- |
| 100 | 22,392.30 | 327,317.54 | C++ faster by 14.62x |
| 1,000 | 1,808,276.60 | 3,067,625.04 | C++ faster by 1.70x |
| 10,000 | 174,354,861.60 | 30,989,797.68 | CUDA faster by 5.63 |
| 100,000 | 19,259,725,569.00 | 550,264,284.10 | CUDA faster by 16.83 |

All implementations of the program except for C++ and CUDA with 100,000 data points were run for a minimum of 10 runs to get the average execution time. With 100,000 data points, C++ takes a long time to run (~2.6 hours per run), while CUDA had inconsistent results. All run time in the table recorded are in microseconds.

**Detailed analysis and discussion of results**

With CUDA, it was initially thought to parallelize two parts of the gather_points function - one is the section where lambda is computed, and the other is the actual computation of the distance between a potential core point vs all other data points in the dataset. Upon doing multiple runs, it turned out that lambda computation did not require parallelization as the computation usually converged early hence the distance function is the focus of the parallelization.

While the conversion of logic from C++ to CUDA was done successfully, there still exists discrepancies between the cluster created when using the same parameters both in C++ and CUDA. Usually, CUDA has higher cluster count due to the logic not capturing all of the extended neighbors of the core point. This is a crucial section to be updated.

An interesting thing to note with the execution is that CUDA is generally faster when dealing with larger datasets as this fully utilizes the parallelized processing of multiple elements.

Improvements on the code can still be done such as re-inventing the creation of neighbor array as it is currently allocated with the size of the full dataset and needs an extra step of trimming of zero values from the array to arrive at the final neighbor array with only the qualified core data points.

