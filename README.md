# shell-stats
Command-line statistics calculator.

This tiny program complements tools like "awk", "sed", etc. which you use in a terminal console. Inspired by the "[st](https://github.com/nferraz/st)" project.

# Installation

You have to install the dependencies and then download the script:
```bash
pip3 install tabulate numpy

wget https://raw.githubusercontent.com/famzah/shell-stats/main/shell-stats
chmod +x shell-stats

./shell-stats --help
```

Optionally, you can move the file `shell-stats` to a directory in your $PATH locations. Traditionally, such directories are `~/bin` or `/usr/local/bin`.

# The problem and its solution by examples
Occasionally you end up with a list of numbers which you need to statistically analyze. Here is an example:
```bash
# cat numbers.3 | head
1537.87
-1959.41
690.752
-2112.1
-159.665
...
```

You can easily calculate "sum" and "count" using "awk" or "perl" one-liners. But sometimes you need a deeper analysis using one of the following functions:

* 95% percentile or other percentile values
* standard deviation
* min, max, mean, average
* count, sum

`shell-stats` lets you calculate those statistics for a bunch of numbers which you supply via STDIN. Here is an example:
```bash
# cat numbers.3 | shell-stats
  count      min    median     max    stddev
-------  -------  --------  ------  --------
     20  -2112.1     446.1  2081.8    1387.1
```

You can configure what statistics to be shown:
```bash
# cat numbers.3 | shell-stats --list-format=rows count min median max sum mean stddev 0% 1% 20% 25% 50% 66% 95% 99% 100%
stats      value
-------  -------
count       20.0
min      -2112.1
median     446.1
max       2081.8
sum       1293.2
mean        64.7
stddev    1387.1
0%       -2112.1
1%       -2085.7
20%      -1618.0
25%      -1228.1
50%        446.1
66%        964.5
95%       1723.7
99%       2010.2
100%      2081.8
```

The output can be formatted as follows:

* single row with headers (default)
* each statistics on a separate row
* JSON, so that you can use the results data programatically in other scripts

Please consult the usage help by `--help` for additional information.
