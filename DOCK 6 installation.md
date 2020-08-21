# DOCK 6 tutorial demo #1

For installation, please obtain a license file from http://dock.compbio.ucsf.edu/DOCK_6/index.htm

## Command line-based installation:

### 1) Navigate to the folder that contains the installation file:

`cd /Volumes/JP_External/DOCK/install`

### 2) Decompress and extract folders using the following commands:

`tar -zxvf dock.6.0.tar.gz`

### 3) Configure the Makefile for the appropriate operating system:

To navigate back one directory `cd -`

Then, since the configure file is in the dock6/install folder `cd dock6/install`

Then, execute the configure file `./configure gnu`

### 4) Build the DOCK executable(s): 

`make all` or
`make dock` or
`make utils`

### 5) Test the built executable(s):

`cd test`

`make clean`

`make test`

