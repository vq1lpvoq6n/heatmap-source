# heatmap-source

The present script allows the rendering of a heat map which can display the behaviour of activities across different event logs, which have been grouped into clusters by applying a clustering algorithm.
The script takes two files as input:
- one .csv file, containing the result of the clustering process: it is expected to contain two columns, respectively of log names and cluster ID's;
- one .csv file, containing all the detail about the activities that compose each log: it is expected to contain at least information, in columns, about the names of the activities and the names of the logs. In its current shape, the script will also check for information about any repeating behavior of activities, which are expected to be found in a column labeled 'IsRepeating'. The script will produce a Pandas dataframe of size n x m, where n is the total number of logs and m is the total number of activities. The extracted information can be summarized as follows:
the generic pair (log, activity) is either found in the .csv thus labeled as present, or not found thus labeled as not present - a further specification of the behavior can be specified by detecting any repeating behavior, which leads to a total of three possible outcomes: 1) the activity is not in the log; 2) the activity is in the log; 3) the activity is in the log and it is repeating. The three statuses are translated into the numeric values 0, 0.5, and 1.

All the activities provided are sorted by the following criterion: the one(s) that appear in the most clusters come first, followed by the ones that appear in less clusters, and so forth. The sorted list of activities is used as the set of values in the X axis of the heat map. Regarding the Y axis, it displays the provided event logs, which are only grouped by cluster: in our study case, clusters IDs are represented with natural numbers 0 to N, thus the clusters appear sorted numerically (0 being on top of the heat map, N on the bottom).

A green scale has been used, with values 0 as white, 0.5 as green, 1 as a darker shade of green.
To better visualize the edges between two clusters, horizontal lines were drawn on the heatmap, by first gathering the coordinates of said edges (that is to say, "the points where cluster X ends, and cluster Y begins").
In many cases, the dataset to be visualized may feature a huge number of clusters containing very few activities each: in such cases, the horizontal lines can add too much visual noise, and are recommended to be turned off by ignoring the instruction with a '#'.
