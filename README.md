# Data Loading/Preprocessing Libraries Overview

## Table of Contents
* [Data Loading and Preprocessing](#data-loading-and-preprocessing)
  * [aeon](#aeon)
  * [Benzina](#benzina)
  * [DALI](#dali)
  * [Dataset Loaders](#dataset-loaders)
  * [Fuel](#fuel)
  * [PyTorch](#pytorch)
  * [TensorFlow](#tensorflow)
* [Data Distribution](#data-distribution)
  * [Intake](#intake)
  * [Quilt](#quilt)
* [Distributed Data Loading and Computing](#distributed-data-loading-and-computing)
  * [Dask](#dask)
  * [Data Format](#data-format)
  * [Xarray](#xarray)

## Data Loading and Preprocessing

### aeon
aeon is a data loading and preprocessing library for image, video, audio and text files. Particularly, it has built-in support for image segmentation problems. It requires an ingest phase where the data should be split and balanced. A manifest file also needs to be provided for a dataset to describe the structure of its data. The data loader can be configured to cache the data on disk in .cpio files for fast future reads. aeon can also be setup to distribute the loading and preprocessing on a separate server.

aeon exposes interfaces to develop support for custom formats. It provides a compatibility layer for neon but it structures allows for simple implementation of custom machine learning libraries compatibility layers.

### Benzina
Benzina is a data loading and preprocessing library for images. It allows for fast GPU decoding and pre-processing of images. In its current state, it requires a fair amount of ingestion of the data before it can be used. In the ingestion phase, the data is normalized so all the images are of the same square size then converted to H.264.

Benzina exposes a PyTorch compatible dataset and a dataloader but its interface is light allowing for other compatibility layers to be implemented.

### DALI
DALI is a data loading and preprocessing library for images. It allows for fast hybrid CPU-GPU decoding of JPEG and fast GPU pre-processing of images. Other images formats are decoded on CPU using OpenCV in a parallel manner. It provides readers for Caffe and Caffe2 LMDB, MXNet RecordIO, TensorFlow TFRecord and a simple file reader.

DALI exposes compatibility layers for MXNet, PyTorch and TensorFlow.

### Dataset Loaders
Dataset Loaders is a collection of dataset loaders with preprocessing features built-in for images and videos. Datasets on shared drives can be copied over to a local directory to avoid network delays in subsequent read of the data. The loading of the data can be parallelized to multiple CPUs.

Dataset Loaders exposes an interface to develop support for custom datasets.

### Fuel
Fuel is a data loading and preprocessing library for image, audio and text. It requires an ingest phase to convert the data into a supported format, usually HDF5. It provides command line utilities to automatically download and ingest datasets. Fuel can also be setup to distribute the data loading on a separate server.

Fuel exposes interfaces to develop support for custom datasets, preprocessing functions, iteration schemes and downloaders and converters for custom datasets.

### PyTorch
PyTorch is a machine learning library with data loading and preprocessing provided through its torchvision package. It provides built-in support for images loading and preprocessing along with some dataset loaders for common images sets.

PyTorch exposes a simple interface to develop support for custom datasets, preprocessing functions and samplers.

### TensorFlow
TensorFlow is a machine learning library with data loading and preprocessing features. It provides built-in support for images and loading and preprocessing along with support to load audio and video files.

TensorFlow exposes utilities to extend the support for custom datasets and preprocessing functions.

## Data Distribution

### Intake
Intake is a library for distributed data loading and computation on clusters with a focus on datasets management. It abstracts the data source from its content and provides utilities to easily find and load datasets stored locally or in a cloud service. It allows to optimize the data storage, file format and data loading library without requiring an update on the loading procedure in the experiment. Built-in, the library can read data into NumPy ndarrays, Panda Dataframes and Python lists of dictionaries.

For parallel computation and datasets that don't fit in memory, data can be provided as Dask containers.

A distribution system is offered in catalogs, which can describe different partitions of a dataset and recursively contain catalogs to group datasets. 

Intake provides a simple interface to easily extend the supported list of data loaders and catalogs. Custom cataloging allows to automatilcally generates catalog access from web sources or local sources. Its Dask backend also allows to download and/or stream data from their original sources through protocols like http(s) and s3, so the initial ingestion process can be abstracted and automated.

For easy data access, it's possible to build condo package containing the data or reference to the data which can then be installed, updated or deleted using the terminal.

### Quilt
Quilt is a library for datasets loading and management. It allows to manage datasets like code with auto-versioning of the data for easy reference and rollback. Along it's command line interface to download, build and push local and remote datasets, it provides the same interface through python so everything can be done in code. It has built-in support for Pandas DataFrames and provides a virtual directory structure of the data which can be used to load custom data format using other data loaders.

Quilt can be purchased as a service with a free tier for public packages or can be self-hosted.

## Distributed Data Loading and Computing

### Dask
Dask is a library for distributed data loading and computation on local CPUs and clusters. It allows to easily scale NumPy ndarrays and Pandas DataFrames workflow and change the space limitation from "fits in memory" to "fits on disk". Its containers interfaces mimic the ones of NumPy and Pandas to allow minimal learning curve and rewrites of an experiment. Containers implementing the iterator interface can parallelize computation using Dask Bags and custom code computation can be parallelized using Dask Delayed or Dask's implementation of Python’s concurrent.futures. Built-in, the library can read data into NumPy ndarrays, images, Panda Dataframes and Python lists of dictionaries.

While Dask's built-in file type support is limited, it provides tools to parallelize the opening of a file to read it or bytes and stream it over a variety of protocols like http(s) and s3.

### Xarray
Xarray is a library that brings Pandas's features to multidimensional arrays using an interface that is the same as much as possible. It provides robust conversions from and to NumPy's ndarrays and Pandas DataFrames or Series. It supports NetCDF as its natural serialization format is NetCDF and integrates with Dask for parallel computations.
