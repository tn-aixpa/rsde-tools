# rsde-tools

Set of base tools for RSDE analysis

#### AIPC

- `kind`: component
- `ai`: remote sensing
- `domain`: generic

A base Docker image pre-configured with essential libraries and tools for remote sensing workflows. Designed to serve as a foundation for satellite imagery processing, geospatial analysis, and related projects.


## Key Features

Pre-installed libraries for geospatial and remote sensing tasks.

Reproducible and portable environment for consistent results.

Simplified setup for new projects—no need to install dependencies manually.

## Included Libraries

- GDAL – Geospatial Data Abstraction Library

- Rasterio – Pythonic raster handling

- Geopandas – Spatial operations on vector data

- Shapely – Geometric operations

- OpenCV – Image processing

- scikit-image – Scientific image analysis

- Python 3.10

## Build

docker build -t rsde-tool .

## License

[Apache License 2.0](./LICENSE)
