# Plex, for Synology

The default Plex container runs perfectly fine on Synology, but hardware transcoding doesn't work.

There's a way to get it working, but mapping in the `/dev/dri` devices, and changing their permissions: https://forums.plex.tv/t/plex-docker-hw-transcode-synology/174793/19?u=nzben

Problem is that the permissions get lost every time the container restarts, or if it's updated.

This repo fixes that problem by doing a nasty `chmod` to `/dev/dri` every time the container starts.

¯\\\_(ツ)\_/¯
