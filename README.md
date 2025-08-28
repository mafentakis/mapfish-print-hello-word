# MapFish Print Hello World

This repository contains a minimal MapFish Print 3 configuration and a Dockerfile that packages it into a runnable image.

## Codespaces

The included [devcontainer](.devcontainer/devcontainer.json) builds this Dockerfile and starts MapFish Print as a sidecar when you open the repository in GitHub Codespaces. The service listens on port 8080, so there is no need to run any Docker commands manually.

To test the setup, open the integrated terminal and generate a map:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

The command saves `map.pdf` in the workspace, which you can open directly in the editor.

## Run locally with Docker

To run MapFish Print outside Codespaces, build the image and start a container:

```
docker build -t mapfish-print .
docker run --rm -p 8080:8080 mapfish-print
```

In another terminal, send the provided print specification to generate the sample map:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

The request uses the configuration in `print-apps/`. The map is centered on Siegen, Germany and renders tiles from the basemap.de WMTS service published by the Federal Agency for Cartography and Geodesy (BKG):

```
https://sgx.geodatenzentrum.de/wmts_basemapde/1.0.0/WMTSCapabilities.xml
```

The resulting PDF is written as `map.pdf`.
