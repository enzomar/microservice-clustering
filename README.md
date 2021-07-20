# microservice-clustering

## Problem statement
This is you challenge: you have 100 services (microservices) and you are asked to group them in a way that workload and infrastructure resources are equally repartitioned. How to do you? On a small number I am sure you will sort it out by using common sense but, on a larger number or servers, a more industrialized way would be needed, at least to start with. What you will read here after is based on "just" math, of course a functional and organizational interpretation would be needed.
In other words the problem we are tring to solve is: clustering microservices.
Severals features could be condisered to drive the optimal clustering such as:
- TPS (number of processed messages per seconcds)
- RAM (mainly RSS)
- Disk (bin/lib disk space occupied)
- Databases calls
- …

From all the above factors, here under I will consider only the TPS. The reason is that I consider it as the most restrictive criteria for our exercise and often there is a strong link between the TPS processed and the CPU / RAM / DB calls needed to process such TPS. Of course those are empirical deductions and may vary from case to case.
Collateral thinking
Oh yes, let not be obvius and try to tackle the challenge from a different angle. In the area of socials network and AI several algorithms have been studied and implemented to ease the identification of patterns, similitudes or proximity across members of a network
https://en.wikipedia.org/wiki/Cluster_analysis
https://scikit-learn.org/stable/modules/clustering.html

I found very interesting the idea to make a parallel among the social network for instance facebook freinds community and a microservices that tries to conunicate among them. SO what would hapen if I aplis communiti detection algorithm to microservices where the intesity of a connection among n friends I can visualize such as the TPS exchanged by n microservices?
https://scikit-learn.org/stable/modules/clustering.htmlOne of the unsupervised clustering learning techique

##The experiment
After having reviewed different approaches and libraries I will focus here below on the spectral clustering in python.
###Input
2 inputs are needed:
- Topology and resource consumption
- Number of target communities or clusters

#### Topology and resources consumption
I created an excel with stat for each backend and the tps exchanged (relative values)
Adjacent matris and info for each backend

Each row contains:
- BE: Name of the Backend, to be used as label in the final graph
- TPS: total TPS received and so processed by the backend
- RAM[MB]
- DISK[MB]: size of the source code or compiled executable / library ( depends on the technology)
- Adjacent Matrix: Number of TPS exchanged across BEs.

#### Number of target communities or cluster
In the basic implementation of th spectral clustering the number of cluster is needed as inptu parameter. A more advced implementation allow to find optimal number automatically. TODO.
I set 3 as number of wished clusters

### Logic
The idea is to implement the base spectral clustering. Steps:
- Load the excel file and extract the adjacent matrix.
- Compute the cluster association via spectral clustering ( Laplacian from the adjacent matrix and then k-means)
- Draw the results

## How to run
