imuestat - classify inertial data stream by statistical properties
==================================================================

 This repository holds scripts to extract features from the dataset mentioned in
[1], as well as the extracted feature in a CSV file. It's purpose is to allow
easy reproduction of the mentioned results.

## Results

 The results of the run as described in the paper can be found in the 'results'
file.

## Usage

 The imustat script can be used to classify streams and extract the features.
It's output is in csv format, and it takes .mkv (or other formats that ffmpeg
can read) and analyzes the contained streams. You can turn on debugging which
will print additional information on each row:

```bash
./imustat -d b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv
acc   acc   acc   1.000   1.00000     1.00000    66.72874   "b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv" "none"
gyr   gyr   gyr   0.008   6.00000    -4.00000    32.34980   "b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv" "none"
mag   mag   mag   0.797   3.00000    -1.00000     1.08561   "b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv" "none"
none  none  none  0.977   2.00000     0.00000    15.03113   "b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv" "none"
```

The meaning of each row is:

 1. ground truth sensor type (value of NAME tag in stream)
 1. estimated sensor type (simple ruleset)
 1. estimated sensor type (accmag ruleset)
 1. empirical mode of the distribution (value)
 1. number of peaks
 1. difference of mean number of peaks of none-gyro streams and number of peaks
 1. kurtosis of data ditribution
 1. input filename
 1. value of POSITION tag in input stream

 Without '-d' only the results of the classification will be printed

```bash
./imustat b6276bb5-168d-4b84-a2cd-88b35a5ad354.mkv
acc
gyr
mag
none
```

## Requirements

 This software requires a recent version of ffmpeg, numpy, matplotlib and scipy. For I/O the [ffmpeginput](github.com/pscholl/ffmpeginput) module is required.

## Caveats

 The only tested input format are .mkv file at the moment. Should the
identified sensor type not match your exception, then please check whether your
data recording was interpolated with non-NaN values.

[1]: Philipp M. Scholl, Kristof van Laerhoven - "On The Statistical Properties
     of Body-Worn Inertial Motion Data" in Internatiol Symposium on Wearable
     Computing, 2017 
