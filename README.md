# phoebus-docker

Run Phoebus in a Docker container

## Build image
```
docker compose build
```

## Run the image
Configure the display:
```
xhost +Local:*
```
Check that 'Local' appears:
```
xhost
```
Run the container:
```
docker run -e DISPLAY=unix$DISPLAY --net=host --rm -it phoebus:test
```
