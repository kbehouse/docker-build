
# Build OpenCV using alpine

Build only you want opencv module, the image only **192MB** 

Including module *core,imgproc,imgcodecs,python3*

## Build & Test

Build base builder

```
docker build -t alpine-opencv-py3-builder -f Dockerfile_builder .
```

Build docker
```
docker build -t alpine-opencv-py3 .
```

Test (check output line.jpg)
```
docker run -v ${PWD}:/app -t alpine-opencv-py3 python3 test_draw_line.py  
```

## Build Only You Want Module

1. using **BUILD_LIST** 

```
cmake -DBUILD_LIST="core,imgproc,python3" ....
```

2. check BUILD_LIST

check here: https://docs.opencv.org/4.1.2/index.html


3. BUILD_LIST meaning:

https://docs.opencv.org/2.4/  (ex: core, imageproc ... etc.)

https://docs.opencv.org/3.0-beta/modules/refman.html

https://docs.opencv.org/4.1.2/index.html


## Check need library

Check need library

```
docker run -it alpine-opencv-py3-builder /bin/bash
lddtree /usr/lib/python3.7/site-packages/cv2/python-3.7/cv2.cpython-37m-x86_64-linux-gnu.so
```

Copy & Paste need library to Dockerfile


## Note

1. when build imgcodec, if you don't have the shared library(.so), it will not link

Example, you don't have tiff.so, it will not link library with tiff.so

2. using cmake-gui and check prefix is **opencv_** (for BUILD_LIST)

(Prefix is **opencv_**, refer it  https://github.com/opencv/opencv/commit/5b17410f7cd89d3f6b9a7def79e8ad1a670daf21)

```
cmake-gui  
```

## Refer

1. build list commit (from: OpenCV 3.4 ) 
    https://github.com/opencv/opencv/commit/5b17410f7cd89d3f6b9a7def79e8ad1a670daf21

    https://stackoverflow.com/questions/25594003/build-specific-modules-opencv

2. opencv alpine

    https://github.com/czeni/opencv-video-minimal/blob/master/Dockerfile


