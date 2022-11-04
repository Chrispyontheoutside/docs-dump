# Faster-RCNN_TF

## Description

This is an experimental Tensorflow implementation of Faster RCNN - a
convnet for object detection with a region proposal network. For details
about R-CNN please refer to the paper Faster R-CNN: Towards Real-Time
Object Detection with Region Proposal Networks by Shaoqing Ren, Kaiming
He, Ross Girshick, Jian Sun.

  - Homepage: <https://github.com/smallcorgi/Faster-RCNN_TF>

## Access

Faster-RCNN\_TF is open to all HPRC users.

<font color=red>There are restrictions as to which version (GPU/CPU) of
Faster-RCNN\_TF works on each cluster. Please note these restrictions in
the following sections and plan your jobs accordingly.</font>

### Anaconda and Faster-RCNN\_TF Packages

TAMU HPRC currently supports the user of Faster-RCNN\_TF though the
Anaconda modules. However, a user needs to install faster-rcnn\_tf on
their own following the instructions below:

    [NetID@terra3 ~]$module load CUDA/8.0.44-GCC-system  
    [NetID@terra3 ~]$module load Anaconda/2-5.0.1  
    [NetID@terra3 ~]$source activate faster-r-cnn  
    (faster-r-cnn)[NetID@terrra3 ~] now you need edit the lib/make.sh used for installation of faster-rcnn_tf as the following:

    TF_INC=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_include())')  
    CUDA_PATH=/sw/hprc/sw/Anaconda/2-5.0.1/envs/faster-r-cnn/  
    CXXFLAGS=''  
    HEADER='/sw/hprc/sw/Anaconda/2-5.0.1/envs/faster-r-cnn/lib/python2.7/site-packages/tensorflow/include/external/nsync/public'  
    TF_LIB=$(python -c 'import tensorflow as tf; print(tf.sysconfig.get_lib())')  
    cd roi_pooling_layer  
    if [ -d "$CUDA_PATH" ]; then  
        nvcc -std=c++11 -c -o roi_pooling_op.cu.o roi_pooling_op_gpu.cu.cc   
            -I$TF_INC -I$HEADER -L$TF_LIB -D GOOGLE_CUDA=1 -x cu -Xcompiler -fPIC $CXXFLAGS --expt-relaxed-constexpr   
            -arch=sm_37  
        g++ -std=c++11 -shared -ltensorflow_framework -o roi_pooling.so roi_pooling_op.cc   
             roi_pooling_op.cu.o -I $TF_INC -L$TF_LIB -I $HEADER -D GOOGLE_CUDA=1 -fPIC $CXXFLAGS   
             -lcudart -L $CUDA_PATH/lib  
    else  
        g++ -std=c++11 -I$HEADER -L$TF_LIB -ltensorflow_framework -shared -o roi_pooling.so roi_pooling_op.cc   
             -I $TF_INC -fPIC $CXXFLAGS  
    fi  
    cd ..

    (faster-r-cnn) [netid@terra3 lib]$ now you can run 'make' to install.

After you install the Faster-RCNN\_TF, you can run programs to access
the package. But CUDA/8.0.44-GCC-system is not required to be loaded any
more. That is, you only need do the followings to access the package:

    [NetID@terra3 ~]$module load Anaconda/2-5.0.1  
    [NetID@terra3 ~]$source activate faster-r-cnn
