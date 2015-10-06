# Sleuth HDF5 input format
---------
The hdf5 file consumed by Sleuth has the structure detailed below.  We use `M` do denote the number of target transcripts. Each heading designates a top-level dataset or group by name (i.e. the input requires that the dataset or group be given this name). For a group, sub-headings designate nested datasets contained within that group.  The datatypes are provided in the Python / NumPy notation.

## est_counts `HDF5 dataset`
----------
An array of length `M`, each of type `<f8`, of the estimated counts per transcript (the results of the main estimation procedure)

## bootstrap `HDF5 group`
----------
This group is only present if a non-zero number of bootstrap samples were computed.  Otherwise, this group is absent.  When the group is present, if we have `k` bootstrap samples, it has the format described below:

#### bs0 `HDF5 dataset`
The samples from the first bootstrap.  An array of length `M`, each of type `<f8`.

#### bs1 `HDF5 dataset`
The samples from the second bootstrap.  An array of length `M`, each of type `<f8`.

#### bsk-1 `HDF5 dataset`
The samples from the `k`-th bootstrap.  An array of length `M`, each of type `<f8`.

## aux `HDF5 group`
----------
This is a HDF5 group, at the top-level, that contains relevant information about the quantification run

#### call `HDF5 dataset` 
The command line used to invoke the quantifier — the type is a fixed-width string `|SXX`.

#### eff_lengths `HDF5 dataset` 
The effective lengths of the transcripts. An array of length `M`, each of type `<f8`.  

#### ids `HDF5 dataset` 
The target names used for the transcripts. An array of length `M`, each a fixed-width string `|SXX`.

#### index_version `HDF5 dataset` 
The version of the (Kallisto) index for this quantification run — the type is `<i4`.

#### kallisto_version `HDF5 dataset`
The version of Kallisto used to produce this output file — the type is a fixed-width string `|SXX`.

#### lengths `HDF5 dataset` 
The actual (not effective) lengths of all of the transcripts. An array of length `M`, each of type `<i4`.

#### num_bootstrap `HDF5 dataset` 
The number of bootstrap samples that have been generated — the type is `<i4`.

#### num_processed `HDF5 dataset`
The number of fragments processed in the input dataset.  *Note*: This refers to the *total* number of fragments; not the number of mapped fragments. The type is `<i4`.

#### start_time `HDF5 dataset`
The time that quantification began (in the format returned by [asctime()](http://en.cppreference.com/w/cpp/chrono/c/asctime), but with the newline stripped). The type is a fixed-width string `|SXX`.
