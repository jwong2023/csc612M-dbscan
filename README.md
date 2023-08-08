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
| 100 | 1 | 2 | 3 | 4 |
| 1,000 | 1 | 2 | 3 | 4 |
| 10,000 | 1 | 2 | 3 | 4 |
| 100,000 | 1 | 2 | 3 | 4 |

**Detailed analysis and discussion of results**
