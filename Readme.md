# EMODnet - Heightmap Interpolation (Python)

Interpolation functions for heightmaps developed within the EMODnet Bathymetry (High Resolution Seabed Mapping) project.

Please visit the documentation at: https://emodnet-heightmap-interpolation.readthedocs.io/en/latest/

## Installation

This package and all its requirements can be installed through `setuptools` using:

```
python setup.py install 
```

Note that it requires python3.7 to run.

If you prefer to install it in a virtual environment:

```
python3.7 -m venv venv
source venv/bin/activate
pip install --upgrade pip
python3.7 setup.py install
```

For convenience, after installation, we recommend to put the main script of the package within the path:

 

## Usage

As mentioned above, the main entry point for interpolating NetCDF4 datasets is the `interpolate_netcdf4.py` script.

Since this package was developed within the EMODnet Bathymetry project, for the moment no other inputs are expected. For other inputs, take the code in this script as reference and use directly the different interpolation modules at your convenience. 

## Docker

For convenience, we also provide a docker image with all the dependencies intalled at DockerHub. Assuming you have docker installed, you can obtain it by:

```
docker pull coroniscomputing/heightmap_interpolation:<tag_name>
```

Where `<tag_name>` must be a specific version of the package, or `latest`.

Or, if you want to compile the docker image by yourself:

```
docker build -t <image_tag_name> .
```

Then, run it with:

```
docker run -it --user $(id -u):$(id -g) -v <data_folder>:/data coroniscomputing/heightmap_interpolation:<tag_name>
```

On the one hand, using the `-v` flag we are mounting the directory containing the data to process to the `/data` folder within the container. On the other hand, the `--user $(id -u):$(id -g)` part is to achieve that the files you generate within docker in the mounted volume are owned by your user (otherwise they would be owned by the *root* user!). 
The container will automatically run the `bash` command, and you will be inside the container. Thus, there we simply run the `interpolate_netcdf4.py` script with the desired parameters (it is included in the container's path, so you can call it directly). For instance:

```
interpolate_netcdf4.py -o /data/<netcdf_results_file> linear /data/<netcdf_input_file>
```  

Keep in mind that this way of running the docker does not provide visualization, so the "--show" flag will be useless! There are ways of sharing the Xs with docker, but these are out of the scope of this documentation.

## Acknowledgements

This project has been developed by Coronis Computing S.L. within the EMODnet Bathymetry (High Resolution Seabed Mapping) project.

* EMODnet: http://www.emodnet.eu/
* EMODnet (bathymetry): http://www.emodnet-bathymetry.eu/
* Coronis: http://www.coronis.es

