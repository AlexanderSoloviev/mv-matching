This git repository is an implementation of the **Micali Vazirani Maximum Cardinality Matching Algorithm**, allegedly the fastest known algorithm for maximum matching in general graphs. Using Python (2.7) and NetworkX (1.10), this code seeks to establish a comparison with the Edmonds's blossom algorithm (max_weight_matching in NetworkX). Furthermore, the current hope is that the implementation could be used within the NetworkX library as an additional matching tool. Note that PyGraphViz and Matplotlib are also used in an effort to draw simpler graphs and observe the actual matching.

The code is currently in its early stages and has several bugs, especially in testing random graphs. The current plan is to:

1. Add more test cases (or specifically find small graphs that cause issues)
2. Fix any bugs to obtain a working version
3. Run time complexity tests with the Edmond's blossom algorithm
4. Determine whether the MV algorithm is truly the fastest (perhaps with the addition of path compression)

# Obtaining the Project

To get the latest version of the project, the code can either be forked or downloaded as a zip file. Before proceeding, make sure you have the following libraries:

- NetworkX 1.10
- PyGraphViz (not necessary for basic usage)
- Matplotlib (not necessary for basic usage)

NetworkX can be found here:

```
https://networkx.github.io/documentation/latest/overview.html
```

The Install tab provides excellent detail on how to set up the library. One thing to note is that NetworkX is not yet compatible with Python versions 3.0 and above. As for the other libraries mentioned, the easiest method of getting them all is by installing a package containing the full SciPy stack. There are several options for this, namely Anaconda, Enthought Canopy, Python(x,y), etc. The full list of options can be found here:

```
http://scipy.org/install.html
```

After everything has been successfully installed, the code can be run by calling the function max_cardinality_matching. It is located in matching/matching.py. The matching directory contains the full algorithm implementation and is the only one necessary for using the code. Hence, for basic usage, nothing else needs to be done.

For testing or working on the code, a good IDE is Eclipse. To work on the code locally, add the following software packages to Eclipse,

- PyDev [http://www.pydev.org/]
- EGit (optional, if you do not want to sync edits to GitHub) [http://www.eclipse.org/egit/]

Then the project can be imported into Eclipse from your GitHub branch directly (File > Import... > Git > Projects from Git) or setup from a local copy (File > New > PyDev Project). The local copy setup must be done as well if you are using EGit, as the importing only downloads all of the files from GitHub and sets up a local repository, but does not create a new Eclipse project. The setup should be finished after the project is created. For testing purposes, the testing/test_driver.py file must be run, with the corresponding testing suites.

# Organization of the Project

The code has three packages: matching, structures, and test.

The matching package contains the algorithm implementation in the form of a single function, located in matching/matching.py. This function is max_cardinality_matching, which takes a NetworkX graph as input and returns a dictionary of matched edges as output.

The structures package contains the data structure OrderedSet in the file structures/ordered_set.py. This implementation was borrowed from Python Recipes. It is necessary in the max_cardinality_matching function.

The test package contains all of the testing suites currently implemented for the matching algorithm. The test_driver.py file has the main function for running all of the testing suites. This is the file to run for testing! The test_matching_simple.py file contains simple graphs with less than 30 vertices that do not have too many blooms. The simple graphs start out with very simple line graphs and easy blooms. The test_matching_compound.py file uses NetworkX graph generators for creating large graphs of more than 60 vertices. This test suite is more complicated in size but not in bloom structure. Lastly, the test_matching_random.py file uses NetworkX random graph generators to create incredibly intricate graphs, such as shell graphs. These have lots of interlocking blooms.

So far, there are about 100 graphs in each testing suite. Of these, about two shell graphs in the test_matching_random suite cause the matching code to fail. These failures do not happen consistently, however.
