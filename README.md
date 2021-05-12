Performance of uniform-OpenMP based vs hybrid-OpenMP based PageRank (pull, CSR).

This experiment was for comparing the performance between:
1. Find pagerank using **uniform** OpenMP (all routines use OpenMP).
2. Find pagerank using **hybrid** OpenMP (some routines are sequential).

Both techniques were attempted on different types of graphs, running each
technique 5 times per graph to get a good time measure. It appears that
**hybrid** approach only performs slightly better than **uniform** approach
in a few cases, but in most other cases, it performs worse. I am not sure why
that is the case, possibly there could be some correlation between execution
time and some other parameter.

Number of threads for this experiment (using `OMP_NUM_THREADS`) was varied
from `2` to `48`. All outputs are saved in [out/](out/) and outputs for `4`,
`48` threads are listed here. See ["pagerank-sequential-vs-openmp"] for a
comparision on single-threaded approach, and OpenMP. The input data used for
this experiment is available at ["graphs"] (for small ones), and the
[SuiteSparse Matrix Collection].

```bash
$ g++ -O3 main.cxx
$ export OMP_NUM_THREADS=4
$ ./a.out ~/data/min-1DeadEnd.mtx
$ ./a.out ~/data/min-2SCC.mtx
$ ...

# Loading graph /home/subhajit/data/min-1DeadEnd.mtx ...
# order: 5 size: 6 {}
# order: 5 size: 6 {} (transposeWithDegree)
# [00000.557 ms; 016 iters.] [0.0000e+00 err.] pagerankUniform
# [00000.420 ms; 016 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-2SCC.mtx ...
# order: 8 size: 12 {}
# order: 8 size: 12 {} (transposeWithDegree)
# [00001.114 ms; 039 iters.] [0.0000e+00 err.] pagerankUniform
# [00000.763 ms; 039 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-4SCC.mtx ...
# order: 21 size: 35 {}
# order: 21 size: 35 {} (transposeWithDegree)
# [00001.374 ms; 044 iters.] [0.0000e+00 err.] pagerankUniform
# [00000.843 ms; 044 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-NvgraphEx.mtx ...
# order: 6 size: 10 {}
# order: 6 size: 10 {} (transposeWithDegree)
# [00000.593 ms; 023 iters.] [0.0000e+00 err.] pagerankUniform
# [00000.410 ms; 023 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-Stanford.mtx ...
# order: 281903 size: 2312497 {}
# order: 281903 size: 2312497 {} (transposeWithDegree)
# [00125.334 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [00135.899 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-BerkStan.mtx ...
# order: 685230 size: 7600595 {}
# order: 685230 size: 7600595 {} (transposeWithDegree)
# [00284.237 ms; 063 iters.] [0.0000e+00 err.] pagerankUniform
# [00315.633 ms; 063 iters.] [4.8175e-11 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-Google.mtx ...
# order: 916428 size: 5105039 {}
# order: 916428 size: 5105039 {} (transposeWithDegree)
# [00457.871 ms; 061 iters.] [0.0000e+00 err.] pagerankUniform
# [00500.167 ms; 061 iters.] [1.0246e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-NotreDame.mtx ...
# order: 325729 size: 1497134 {}
# order: 325729 size: 1497134 {} (transposeWithDegree)
# [00070.703 ms; 057 iters.] [0.0000e+00 err.] pagerankUniform
# [00081.472 ms; 057 iters.] [7.7362e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Slashdot0811.mtx ...
# order: 77360 size: 905468 {}
# order: 77360 size: 905468 {} (transposeWithDegree)
# [00033.634 ms; 054 iters.] [0.0000e+00 err.] pagerankUniform
# [00035.530 ms; 054 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Slashdot0902.mtx ...
# order: 82168 size: 948464 {}
# order: 82168 size: 948464 {} (transposeWithDegree)
# [00036.167 ms; 055 iters.] [0.0000e+00 err.] pagerankUniform
# [00038.795 ms; 055 iters.] [3.6918e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Epinions1.mtx ...
# order: 75888 size: 508837 {}
# order: 75888 size: 508837 {} (transposeWithDegree)
# [00036.694 ms; 053 iters.] [0.0000e+00 err.] pagerankUniform
# [00037.343 ms; 053 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coAuthorsDBLP.mtx ...
# order: 299067 size: 1955352 {}
# order: 299067 size: 1955352 {} (transposeWithDegree)
# [00081.274 ms; 044 iters.] [0.0000e+00 err.] pagerankUniform
# [00091.089 ms; 044 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coAuthorsCiteseer.mtx ...
# order: 227320 size: 1628268 {}
# order: 227320 size: 1628268 {} (transposeWithDegree)
# [00068.195 ms; 047 iters.] [0.0000e+00 err.] pagerankUniform
# [00075.015 ms; 047 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-LiveJournal1.mtx ...
# order: 4847571 size: 68993773 {}
# order: 4847571 size: 68993773 {} (transposeWithDegree)
# [04092.295 ms; 050 iters.] [0.0000e+00 err.] pagerankUniform
# [04471.955 ms; 050 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coPapersCiteseer.mtx ...
# order: 434102 size: 32073440 {}
# order: 434102 size: 32073440 {} (transposeWithDegree)
# [00668.533 ms; 050 iters.] [0.0000e+00 err.] pagerankUniform
# [00697.251 ms; 050 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coPapersDBLP.mtx ...
# order: 540486 size: 30491458 {}
# order: 540486 size: 30491458 {} (transposeWithDegree)
# [00677.000 ms; 048 iters.] [0.0000e+00 err.] pagerankUniform
# [00686.653 ms; 048 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/indochina-2004.mtx ...
# order: 7414866 size: 194109311 {}
# order: 7414866 size: 194109311 {} (transposeWithDegree)
# [07275.811 ms; 059 iters.] [0.0000e+00 err.] pagerankUniform
# [07712.278 ms; 059 iters.] [1.2554e-09 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/italy_osm.mtx ...
# order: 6686493 size: 14027956 {}
# order: 6686493 size: 14027956 {} (transposeWithDegree)
# [01455.947 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [01798.928 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/great-britain_osm.mtx ...
# order: 7733822 size: 16313034 {}
# order: 7733822 size: 16313034 {} (transposeWithDegree)
# [02130.661 ms; 066 iters.] [0.0000e+00 err.] pagerankUniform
# [02549.137 ms; 066 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/germany_osm.mtx ...
# order: 11548845 size: 24738362 {}
# order: 11548845 size: 24738362 {} (transposeWithDegree)
# [03455.949 ms; 064 iters.] [0.0000e+00 err.] pagerankUniform
# [04052.994 ms; 064 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/asia_osm.mtx ...
# order: 11950757 size: 25423206 {}
# order: 11950757 size: 25423206 {} (transposeWithDegree)
# [02581.598 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [03217.129 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
```

```bash
$ g++ -O3 main.cxx
$ export OMP_NUM_THREADS=48
$ ./a.out ~/data/min-1DeadEnd.mtx
$ ./a.out ~/data/min-2SCC.mtx
$ ...

# Loading graph /home/subhajit/data/min-1DeadEnd.mtx ...
# order: 5 size: 6 {}
# order: 5 size: 6 {} (transposeWithDegree)
# [00020.568 ms; 016 iters.] [0.0000e+00 err.] pagerankUniform
# [00000.850 ms; 016 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-2SCC.mtx ...
# order: 8 size: 12 {}
# order: 8 size: 12 {} (transposeWithDegree)
# [00018.690 ms; 039 iters.] [0.0000e+00 err.] pagerankUniform
# [00002.109 ms; 039 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-4SCC.mtx ...
# order: 21 size: 35 {}
# order: 21 size: 35 {} (transposeWithDegree)
# [00021.733 ms; 044 iters.] [0.0000e+00 err.] pagerankUniform
# [00001.972 ms; 044 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/min-NvgraphEx.mtx ...
# order: 6 size: 10 {}
# order: 6 size: 10 {} (transposeWithDegree)
# [00016.673 ms; 023 iters.] [0.0000e+00 err.] pagerankUniform
# [00001.290 ms; 023 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-Stanford.mtx ...
# order: 281903 size: 2312497 {}
# order: 281903 size: 2312497 {} (transposeWithDegree)
# [00065.371 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [00051.436 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-BerkStan.mtx ...
# order: 685230 size: 7600595 {}
# order: 685230 size: 7600595 {} (transposeWithDegree)
# [00107.469 ms; 063 iters.] [0.0000e+00 err.] pagerankUniform
# [00132.635 ms; 063 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-Google.mtx ...
# order: 916428 size: 5105039 {}
# order: 916428 size: 5105039 {} (transposeWithDegree)
# [00136.516 ms; 061 iters.] [0.0000e+00 err.] pagerankUniform
# [00161.865 ms; 061 iters.] [5.3046e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/web-NotreDame.mtx ...
# order: 325729 size: 1497134 {}
# order: 325729 size: 1497134 {} (transposeWithDegree)
# [00042.922 ms; 057 iters.] [0.0000e+00 err.] pagerankUniform
# [00047.288 ms; 058 iters.] [9.3681e-07 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Slashdot0811.mtx ...
# order: 77360 size: 905468 {}
# order: 77360 size: 905468 {} (transposeWithDegree)
# [00044.038 ms; 054 iters.] [0.0000e+00 err.] pagerankUniform
# [00028.499 ms; 054 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Slashdot0902.mtx ...
# order: 82168 size: 948464 {}
# order: 82168 size: 948464 {} (transposeWithDegree)
# [00044.100 ms; 055 iters.] [0.0000e+00 err.] pagerankUniform
# [00031.186 ms; 055 iters.] [5.1949e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-Epinions1.mtx ...
# order: 75888 size: 508837 {}
# order: 75888 size: 508837 {} (transposeWithDegree)
# [00051.899 ms; 053 iters.] [0.0000e+00 err.] pagerankUniform
# [00034.818 ms; 053 iters.] [2.0387e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coAuthorsDBLP.mtx ...
# order: 299067 size: 1955352 {}
# order: 299067 size: 1955352 {} (transposeWithDegree)
# [00040.016 ms; 044 iters.] [0.0000e+00 err.] pagerankUniform
# [00034.274 ms; 044 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coAuthorsCiteseer.mtx ...
# order: 227320 size: 1628268 {}
# order: 227320 size: 1628268 {} (transposeWithDegree)
# [00054.101 ms; 047 iters.] [0.0000e+00 err.] pagerankUniform
# [00030.752 ms; 047 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/soc-LiveJournal1.mtx ...
# order: 4847571 size: 68993773 {}
# order: 4847571 size: 68993773 {} (transposeWithDegree)
# [00805.687 ms; 050 iters.] [0.0000e+00 err.] pagerankUniform
# [01108.808 ms; 050 iters.] [2.5879e-08 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coPapersCiteseer.mtx ...
# order: 434102 size: 32073440 {}
# order: 434102 size: 32073440 {} (transposeWithDegree)
# [00212.052 ms; 050 iters.] [0.0000e+00 err.] pagerankUniform
# [00208.679 ms; 050 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/coPapersDBLP.mtx ...
# order: 540486 size: 30491458 {}
# order: 540486 size: 30491458 {} (transposeWithDegree)
# [00141.253 ms; 048 iters.] [0.0000e+00 err.] pagerankUniform
# [00171.092 ms; 048 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/indochina-2004.mtx ...
# order: 7414866 size: 194109311 {}
# order: 7414866 size: 194109311 {} (transposeWithDegree)
# [03935.948 ms; 060 iters.] [0.0000e+00 err.] pagerankUniform
# [04329.989 ms; 060 iters.] [1.9407e-09 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/italy_osm.mtx ...
# order: 6686493 size: 14027956 {}
# order: 6686493 size: 14027956 {} (transposeWithDegree)
# [00531.134 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [00820.799 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/great-britain_osm.mtx ...
# order: 7733822 size: 16313034 {}
# order: 7733822 size: 16313034 {} (transposeWithDegree)
# [00619.666 ms; 066 iters.] [0.0000e+00 err.] pagerankUniform
# [01054.278 ms; 066 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/germany_osm.mtx ...
# order: 11548845 size: 24738362 {}
# order: 11548845 size: 24738362 {} (transposeWithDegree)
# [00845.922 ms; 064 iters.] [0.0000e+00 err.] pagerankUniform
# [01551.040 ms; 064 iters.] [0.0000e+00 err.] pagerankHybrid
#
# Loading graph /home/subhajit/data/asia_osm.mtx ...
# order: 11950757 size: 25423206 {}
# order: 11950757 size: 25423206 {} (transposeWithDegree)
# [00726.156 ms; 062 iters.] [0.0000e+00 err.] pagerankUniform
# [01473.381 ms; 062 iters.] [0.0000e+00 err.] pagerankHybrid
```

<br>
<br>


## References

- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](http://snap.stanford.edu/class/cs246-videos-2019/lec9_190205-cs246-720.mp4)
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/wzUtVOY.jpg)](https://www.youtube.com/watch?v=rKv_l1RnSqs)

["pagerank-sequential-vs-openmp"]: https://github.com/puzzlef/pagerank-sequential-vs-openmp
["graphs"]: https://github.com/puzzlef/graphs
[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
