# Plex, in Docker, on Synology, with Hardware Transcoding

The default Plex container runs perfectly fine on Synology, but hardware transcoding doesn't work.

There's a way to get it working by mapping in the `/dev/dri` devices, and changing their permissions, which has been [described on the Plex Forums](1). However, the problem is that the permissions get lost every time the container restarts, or if the image is updated.

This repo fixes that problem by doing a nasty `chmod 777` to `/dev/dri` every time the container starts.

¯\\\_(ツ)\_/¯

# HowTo

1. Grab the `plex-synology` image from [Docker Hub](https://hub.docker.com/r/nzben/plex-synology), and create a Docker container on your Synology. Configure the Advanced Settings as desired (Consult the [official pms-docker README](https://github.com/plexinc/pms-docker/blob/master/README.md) for more information.)
1. Export the container settings (Select **`<your container>`** > **Settings** > **Export** > **Container settings**)
1. Replace this line
    ```json
       "devices" : [],
    ```
    with the following:
    ```json
    "devices": [{"CgroupPermissions": "rwm", "PathInContainer": "\/dev\/dri", "PathOnHost": "\/dev\/dri"}],
    ```
1. Delete the container created in step 1
1. Import the edited json file; this should create a new container. (Select **Settings** > **Import** > **`<your edited json file>`**)
1. Start the new container, and then enable Hardware Transcode in your server settings. (Select **Settings** > **Transcoder** > **Show Advanced** > **Use hardware acceleration when available**)
1. :thumbsup:
