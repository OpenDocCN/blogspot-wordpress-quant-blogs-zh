<!--yml
category: 未分类
date: 2024-05-12 17:56:10
-->

# FTCA2 | CSSA

> 来源：[https://cssanalytics.wordpress.com/2013/12/05/ftca2/#0001-01-01](https://cssanalytics.wordpress.com/2013/12/05/ftca2/#0001-01-01)

The strength of [FTCA](https://cssanalytics.wordpress.com/2013/11/26/fast-threshold-clustering-algorithm-ftca/ "Fast Threshold Clustering Algorithm (FTCA)") is both speed and simplicity. One of the weaknesses that FTCA has however, is that cluster membership is determined by a threshold to one asset only at each step (either MC or LC). Asset relationships can be complex, and there is no assurance that all members of a cluster have a correlation to each other member that is higher than the threshold. This can lead to fewer clusters, and potentially incorrect cluster membership assignments. To improve upon these weaknesses, FTCA2 uses the same baseline method but computes the correlation threshold to ALL current cluster members rather than just to MC or LC. In this case, the average correlation to current cluster members is always calculated to determine the threshold. It also selects assets in order of the closest correlation to the current cluster members.

The pseudo-code is presented below:

***While there are assets that have not been assigned to a cluster***

*   **If only one asset remaining then**
    *   **Add a new cluster**
    *   **Only member is the remaining asset**
*   **Else**
    *   **Find the asset with the Highest Average Correlation (HC) to all assets not yet been assigned to a Cluster**
    *   **Find the asset with the Lowest Average Correlation (LC) to all assets not yet assigned to a Cluster**
    *   **If Correlation between HC and LC > Threshold**
        *   **Add a new Cluster made of HC and LC**
        *   **Try adding each of the remaining assets that have not yet been assigned to a Cluster in order of highest correlation to the current cluster if correlation of the asset is > the average correlation of the the current cluster.**
    *   **Else**
        *   **Add a Cluster made of HC**
            *   **Try adding each of the remaining assets that have not yet been assigned to a Cluster in order of highest correlation to the current cluster if correlation of the asset is > the average correlation of the the current cluster.**
        *   **Add a Cluster made of LC**
            *   **Try adding each of the remaining assets that have not yet been assigned to a Cluster in order of highest correlation to the current cluster if correlation of the asset is > the average correlation of the the current cluster**
    *   **End if**
*   **End if**

***End While***