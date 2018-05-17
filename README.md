# Openalpr 
----------

OpenALPR is an open source Automatic License Plate Recognition library written in C++ with bindings in C#, Java, Node.js, Go, and Python. The library analyzes images and video streams to identify license plates. The output is the text representation of any license plate characters.

Binaries
--------

Pre-compiled Windows binaries can be downloaded on the [releases](https://github.com/openalpr/openalpr/releases) page. Please use [Wiki](https://github.com/openalpr/openalpr/wiki) for compilation instructions.

Installation
------------

Install OpenALPR on Ubuntu 16.04 with the following commands:

```
sudo apt-get update && sudo apt-get install openalpr
```

OpenALPR requires the following additional libraries:

- [Tesseract OCR v3.0.4](https://github.com/tesseract-ocr/tesseract)
- [OpenCV v2.4.8+](http://opencv.org/)

After cloning this GitHub repository, you should download and extract Tesseract and OpenCV source code into their own directories. Compile both libraries.

User Guide
----------



OpenALPR includes a command line utility. Simply typing "alpr [image file path]" is enough to get started recognizing license plate images. This is a License Plate detector with added support for India using Openalpr library.

Recognising Indian Number Plates
--------------------------------

After the installing the opensource version of Openalpr. Clone this openalpr_lic repository in home directory and copy the contents of it to the openalpr installation runtime directory:


```
# Clone the latest code from Github

git clone https://github.com/abhishekworkspace/openalpr_lic

# Copy the contents of this repository
For example, the following output is created by analyzing this image: 
```
Plate Image:
------------
![alt text](https://raw.githubusercontent.com/abhishekworkspace/openalpr_lic/master/car.jpg)


```
user@linux:~/openalpr_lic$  alpr -c in car.jpg
plate0: 10 results
    - MH01AV8866	 confidence: 89.5252
    - MH01AV88G6	 confidence: 88.0583
    - MH01AV886G	 confidence: 86.326
    - MHD1AV8866	 confidence: 86.3117
    - MH01AV88B6	 confidence: 86.0594
    - MH01AV88S6	 confidence: 86.0235
    - MH01AV886B	 confidence: 85.7652
    - MH01AV886S	 confidence: 85.4283
    - MHQ1AV8866	 confidence: 84.8634
    - MH01AV88GG	 confidence: 84.8591
```

Detailed command line usage
---------------------------

```
user@linux:~/openalpr_lic$ alpr --help

USAGE: 

   alpr  [-c <country_code>] [--config <config_file>] [-n <topN>] [--seek
         <integer_ms>] [-p <pattern code>] [--clock] [-d] [-j] [--]
         [--version] [-h] <image_file_path>


Where: 

   -c <country_code>,  --country <country_code>
     Country code to identify (either us for USA or eu for Europe). 
     Default=us

   --config <config_file>
     Path to the openalpr.conf file

   -n <topN>,  --topn <topN>
     Max number of possible plate numbers to return.  Default=10

   --seek <integer_ms>
     Seek to the specified millisecond in a video file. Default=0

   -p <pattern code>,  --pattern <pattern code>
     Attempt to match the plate number against a plate pattern (e.g., md
     for Maryland, ca for California)

   --clock
     Measure/print the total time to process image and all plates. 
     Default=off

   -d,  --detect_region
     Attempt to detect the region of the plate image.  [Experimental] 
     Default=off

   -j,  --json
     Output recognition results in JSON format.  Default=off

   --,  --ignore_rest
     Ignores the rest of the labeled arguments following this flag.

   --version
     Displays version information and exits.

   -h,  --help
     Displays usage information and exits.

   <image_file_path>
     Image containing license plates
```
Using command line arguments for India
--------------------------------------

For India you can use the following command:

For recognising the images
```
  alpr -c in image.jpg
```
For recognising the Videos
```
  alpr -c in video.mp4
```
 For recognising using webcam
```
  alpr -c in webcam
```

>Check out extra test files under resources folder.

Generating output in text files
-------------------------------

```
#!/bin/bash
alpr -c in -n 1 car.jpg > all_reads.txt
grep "confidence" all_reads.txt | sort -k4 | tail -1 > best.txt
awk '{print $3 " " $4}' best.txt > highest.txt
ss=$(cat 'highest.txt')
grep -B 2 "$ss" all_reads.txt | head -1
```

Documentation
-------------

Documenation for building openalpr for any other country is available [here](doc.openalpr.com). 

Training
--------

Detailed documentation for training is available at
```
http://doc.openalpr.com/opensource.html
```

Training the detector
---------------------
Using the train detector for india
```
https://github.com/loxxy/train-detector
```

Training OCR
------------

```
https://github.com/openalpr/train-ocr
```

For Generating trained data file use Tesseract or jTessBoxEditor.

jTessBoxEditor
--------------

jTessBoxEditor is a box editor and trainer for Tesseract OCR, providing editing of box data of both Tesseract 2.0x and 3.0x formats and full automation of Tesseract training. It can read images of common image formats, including multi-page TIFF. The program requires Java Runtime Environment 7 or later.

Double click on the JAR file to launch the program, or execute the following command:
```
java -Xms128m -Xmx1024m -jar jTessBoxEditor.jar
```
*You will need to provide the TIFF/Box files as input to the editor. Which can be generated using cropped images of Liscense plates for using fonts of particular license plate to train the OCR and generate the trained file.* 

Images to be used in training should be of 300 DPI and 1 bpp (bit per pixel) black&white or 8 bpp grayscale uncompressed TIFF format; box files, encoded in UTF-8 format, are generated by Tesseract executables with appropriate command-line options (see Tesseract Training Wiki). Or they both can be created using the built-in TIFF/Box Generator.

For Detailed traning on Jtessdata follow the link below.
```
http://vietocr.sourceforge.net/training.html
```

>Check out Box and Tiff files for training of OCR and generation of trained data under resources folder.

Integrating the Library
-----------------------

OpenALPR is written in C++ and has [bindings](http://doc.openalpr.com/bindings.html) in C#, Python, Node.js, Go, and Java. Please see this guide for examples showing how to run OpenALPR in your application. 

Compiling
---------
OpenALPR compiles and runs on Linux, Mac OSX and Windows.
After cloning this GitHub repository, you should download and extract Tesseract and OpenCV source code into their own directories. Compile both libraries.

Please follow these detailed compilation guides for your respective operating system:

* [Windows](https://github.com/openalpr/openalpr/wiki/Compilation-instructions-(Windows))
* [Ubuntu Linux](https://github.com/openalpr/openalpr/wiki/Compilation-instructions-(Ubuntu-Linux))
* [OS X](https://github.com/openalpr/openalpr/wiki/Compilation-instructions-(OS-X))
* [Android Library](https://github.com/SandroMachado/openalpr-android)
* [Android Application Sample](https://github.com/sujaybhowmick/OpenAlprDroidApp)contents of it 
* [iOS](https://github.com/twelve17/openalpr-ios)
* [iOS React Native](https://github.com/cardash/react-native-openalpr)
* [Xamarin](https://github.com/kevinjpetersen/openalpr-xamarin)


Docker
------

Build docker image
------------------

```
docker build -t openalpr https://github.com/openalpr/openalpr.git

# Download test image

wget http://plates.openalpr.com/h786poj.jpg

# Run alpr on image

docker run -it --rm -v $(pwd):/data:ro openalpr -c eu h786poj.jpg
```

Questions
---------
Please post questions or comments to the *Google group list*: 
```
https://groups.google.com/forum/#!forum/openalpr
```


License
-------

GNU GPLv3 https://www.gnu.org/licenses/gpl-3.0.en.html
