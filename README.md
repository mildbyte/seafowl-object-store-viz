# seafowl-object-store-viz
Seafowl object store cache access visualizer

This notebook relies on a fork of Seafowl that instruments all object store
cache access (inbound requests from DataFusion and outbound requests to
the actual object store provider), consumes the traces, visualizes them for
a single Delta Table at multiple points in time and uses ffmpeg to collate
all individual frames into a single video.

Usage:

- Compile the Seafowl fork (https://github.com/splitgraph/seafowl/compare/main...dev/cache-action-tracing)
- Set up a Delta Table in S3-compatible storage and run some queries (DEBUG loglevel)
- Get the logs: `docker logs seafowl 2>&1 | grep LOGTRACE > initial.txt`
- Get ffmpeg and install Python dependencies: `pip install intervaltree minio pillow tqdm`
- In the notebook, configure the timescale (1 is realtime, 300 is 300x slower), FPS and the Minio client
  (only used to get file sizes and technically not required, the notebook currently doesn't care about
  the file sizes).
- Run the notebook: it'll render each individual frame and then merge them with ffmpeg.
