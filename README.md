<img src="docs/_logo/banner.png">

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/phylopandas/Lobby)
[![Documentation Status](http://readthedocs.org/projects/phylopandas/badge/?version=latest)](http://phylopandas.readthedocs.io/en/latest/?badge=latest)
[![Build Status](https://dev.azure.com/heathcliff2333/heathcliff2333/_apis/build/status/heathcliff233.phylopandas?branchName=master)](https://dev.azure.com/heathcliff2333/heathcliff2333/_build/latest?definitionId=1&branchName=master)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/heathcliff233/phylopandas/master?filepath=examples%2Fintro-notebook.ipynb)

**Bringing the [Pandas](https://github.com/pandas-dev/pandas) `DataFrame` to phylogenetics.**


PhyloPandas provides a Pandas-like interface for reading sequence and phylogenetic tree data into pandas DataFrames. This enables easy manipulation of phylogenetic data using familiar Python/Pandas functions. Finally, phylogenetics for humans!

<img src='docs/_images/jlab.png' align="middle">

## How does it work?

Don't worry, we didn't reinvent the wheel. **PhyloPandas** is simply a [DataFrame](https://github.com/pandas-dev/pandas)
(great for human-accessible data storage) interface on top of [Biopython](https://github.com/biopython/biopython) (great for parsing/writing sequence data) and [DendroPy](https://github.com/jeetsukumaran/DendroPy) (great for reading tree data).

PhyloPandas does two things:
1. It offers new `read` functions to read sequence/tree data directly into a DataFrame.
2. It attaches a new `phylo` **accessor** to the Pandas DataFrame. This accessor provides writing methods for sequencing/tree data (powered by Biopython and dendropy).

## Basic Usage

**Sequence data:**

Read in a sequence file.
```python
import phylopandas as ph

df1 = ph.read_fasta('sequences.fasta')    # for fasta
df2 = ph.read_fasta_dev('sequence.fasta') # for two-line fasta
df3 = ph.read_phylip('sequences.phy')
```

Write to various sequence file formats.

```python
df1.phylo.to_clustal('sequences.clustal')
```

Convert between formats.

```python
# Read a format.
df = ph.read_fasta('sequences.fasta')

# Write to a different format.
df.phylo.to_phylip('sequences.phy')
df.phylo.to_fasta_dev('seq_two_line.fasta') # to two line fasta
df.phylo.to_embl(mtype='protein', filename='sequences.embl') # set type of SeqRecord annotation property with mtype arg
```

**Tree data:**

Read newick tree data
```python
df = ph.read_newick('tree.newick')
```

## Contributing

If you have ideas for the project, please share them on the project's [Gitter chat](https://gitter.im/phylopandas/Lobby).

It's *easy* to create new read/write functions and methods for PhyloPandas. If you
have a format you'd like to add, please submit PRs! There are many more formats
in Biopython that I haven't had the time to add myself, so please don't be afraid
to add them! I thank you ahead of time!

## Testing

PhyloPandas includes a small [pytest](https://docs.pytest.org/en/latest/) suite. Run these tests from base directory.
```
$ cd phylopandas
$ pytest
```

## Install

Install from PyPI:
```
pip install phylopandas
```

Install from source:
```
git clone https://github.com/heathcliff233/phylopandas
cd phylopandas
pip install -e .
```

## Dependencies

- [BioPython](https://github.com/biopython/biopython): Library for managing and manipulating biological data.
- [DendroPy](https://github.com/jeetsukumaran/DendroPy): Library for phylogenetic scripting, simulation, data processing and manipulation
- [Pandas](https://github.com/pandas-dev/pandas): Flexible and powerful data analysis / manipulation library for Python
- [pandas_flavor](https://github.com/Zsailer/pandas_flavor): Flavor pandas objects with new accessors using pandas' new register API (with backwards compatibility).
