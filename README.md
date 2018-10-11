# Plex, in Docker, on Synology, with Hardware Transcoding

The default Plex container runs perfectly fine on Synology, but hardware transcoding doesn't work.

There's a way to get it working by mapping in the `/dev/dri` devices, and changing their permissions: https://forums.plex.tv/t/plex-docker-hw-transcode-synology/174793/19?u=nzben

Problem is that the permissions get lost every time the container restarts, or if the image is updated.

This repo fixes that problem by doing a nasty `chmod` to `/dev/dri` every time the container starts.

¯\\\_(ツ)\_/¯

# HowTo

1. Grab the image from https://hub.docker.com/r/nzben/plex-synology, and create a Docker container on your Synology.
2. Follow steps 3 to 7 from that original helpful post: https://forums.plex.tv/t/plex-docker-hw-transcode-synology/174793/19?u=nzben
3. :thumbsup:
