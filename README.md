**Accelerating Geospatial DBSCAN Clustering Based on Vincenty Distance**
DBSCAN clustering is a commonly used clustering algorithm that focuses on spatial differences among points. This implementation replaces the usual Euclidean Distance with Vincenty Distance for measuring the geospatial distance between two points.

Parallel algorithms implemented:

DBSCAN calls the function gather_points which starts the process for computing Vincenty distance. The CUDA implementation parallelizes this section and calculates the distance for several points faster than typical serial operations.

Execution time comparison between sequential and parallel

Detailed analysis and discussion of results
