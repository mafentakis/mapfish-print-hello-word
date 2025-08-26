# MapFish Print Hello World

This repository contains a minimal MapFish Print 3 configuration and instructions to run it with the official Docker image.

## Codespaces

This project includes a [devcontainer](.devcontainer/devcontainer.json) setup that runs the MapFish Print service as a sidecar container. When opened in GitHub Codespaces, the `print` service uses the `camptocamp/mapfish_print:3` image and is exposed on port 8080.

From the integrated terminal you can request a map with:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

## Run the container

```
docker run --rm -p 8080:8080 -v $(pwd)/print-apps:/usr/local/tomcat/webapps/ROOT/print-apps camptocamp/mapfish_print:3
```

The service will be available at `http://localhost:8080`.

## Generate a sample map

Send the provided print specification to the running container:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

The request uses the configuration in `print-apps/`. The map is centered on Siegen, Germany and renders tiles from the basemap.de WMTS service published by the Federal Agency for Cartography and Geodesy (BKG):

```
https://sgx.geodatenzentrum.de/wmts_basemapde/1.0.0/WMTSCapabilities.xml
```

It returns the resulting map as `map.pdf`.
