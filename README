imuestat - classify inertial data stream by statistical properties
==================================================================

 This repository holds scripts to extract features from the dataset mentioned in
[1], as well as the extracted feature in a CSV file. It's purpose is to allow
easy reproduction of the mentioned results.

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

## Caveats

 The only tested input format are .mkv file at the moment. Should the
identified sensor type not match your exception, then please check whether your
data recording was interpolated with non-NaN values.

## Data Cleaning

 The following streams were removed prior to evaluation, since the senosr has
failed recording for more than 90% of the time:

 /home/phil/es/datasets/opportunity-2013/session_10_gerald_3.mkv  0:10 'left hand'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_5.mkv 0:9 'left hand'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_2.mkv 0:9 'left hand'
 /home/phil/es/datasets/opportunity-2013/session_11_tobi_5.mkv     0:4 'right hand'
 /home/phil/es/datasets/opportunity-2013/session_11_tobi_1.mkv     0:4 'right hand'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:3 'right upper arm (up)'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:4 'right upper arm (down)'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:6 'left wrist'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:7 'right wrist'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:9 'left hand'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:11 'left upper arm (up)'
 /home/phil/es/datasets/opportunity-2013/session_12_matthias_6.mkv 0:12 'left upper arm (down)'


[1]: Philipp M. Scholl, Kristof van Laerhoven - "On The Statistical Properties
     of Body-Worn Inertial Motion Data" in Internatiol Symposium on Wearable
     Computing, 2017 
