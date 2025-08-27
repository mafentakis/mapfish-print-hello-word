# MapFish Print Hello World

This repository contains a minimal MapFish Print 3 configuration and instructions to run it with the official Docker image.

## Codespaces

This project includes a [devcontainer](.devcontainer/devcontainer.json) that starts the MapFish Print service as a sidecar when you open the repository in GitHub Codespaces. The sidecar runs the `camptocamp/mapfish_print:3.53.0` image on port 8080, so there is no need to execute `docker-compose` or any other Docker command.

To test the setup, open the integrated terminal and generate a map with:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

The command downloads `map.pdf` into the workspace, which you can view directly in the Codespaces editor.

## Run locally with Docker

If you want to run MapFish Print outside Codespaces, start the official image and mount the configuration directory:

```
docker run --rm -p 8080:8080 -v $(pwd)/print-apps:/usr/local/tomcat/webapps/ROOT/print-apps camptocamp/mapfish_print:3.53.0
```

Once the container is running, send the provided print specification to generate the sample map:

```
curl -X POST -H "Content-Type: application/json" --data @spec.json http://localhost:8080/print/print.pdf -o map.pdf
```

The request uses the configuration in `print-apps/`. The map is centered on Siegen, Germany and renders tiles from the basemap.de WMTS service published by the Federal Agency for Cartography and Geodesy (BKG):

```
https://sgx.geodatenzentrum.de/wmts_basemapde/1.0.0/WMTSCapabilities.xml
```

The resulting PDF is written as `map.pdf`.
