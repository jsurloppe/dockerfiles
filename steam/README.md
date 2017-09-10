Run steam on docker with appropriate NVIDIA proprietary driver version and pulseaudio.

This is a fat non-optimized image for easily running steam on a gentoo 64 bits no-multilib.
PR welcome for stripping the unnecessary.

Tagged versions will follow gentoo stabilization of the driver.

For running it :

```
docker run --rm \
--privileged \
-v /etc/localtime:/etc/localtime:ro \
-v /tmp/.X11-unix:/tmp/.X11-unix:ro \
-v /dev/shm:/dev/shm \
-v /home/steam:/home/steam \
-v /run/dbus:/run/dbus \
-v /etc/machine-id:/etc/machine-id:ro \
-v /etc/machine-id:/var/lib/dbus/machine-id:ro \
-v /run/user/$UID/pulse:/run/user/$UID/pulse:ro \
-e DISPLAY=$DISPLAY \
--group-add=27 \
jsurloppe/steam:brewmaster-384.59
```

You may need to add some group(s) to your container;
as example, if your host video group id differ from debian, add ```--group-add=<gid>``` to the docker run command.

You can modify the host steam volume to your preference.
