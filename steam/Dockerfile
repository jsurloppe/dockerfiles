# docker run --rm \
# --privileged \
# -v /etc/localtime:/etc/localtime:ro \
# -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
# -v /dev/shm:/dev/shm \
# -v /home/steam:/home/steam \
# -v /run/dbus:/run/dbus \
# -v /etc/machine-id:/etc/machine-id:ro \
# -v /etc/machine-id:/var/lib/dbus/machine-id:ro \
# -v /run/user/$UID/pulse:/run/user/$UID/pulse:ro \
# -e DISPLAY=$DISPLAY \
# --group-add=27 \
# jsurloppe/steam:brewmaster-384.59

# build from
# sudo ../mkimage.sh -t jsurloppe/steamos:brewmaster debootstrap --variant=minbase brewmaster http://repo.steampowered.com/steamos
FROM jsurloppe/steamos:brewmaster

ENV DEBIAN_FRONTEND noninteractive
RUN dpkg --add-architecture i386
RUN apt-get update
# base steamos package
RUN apt-get install -yq libc6:i386 libgl1-mesa-dri:i386 libgl1-mesa-glx:i386 libgl1-nvidia-glx:i386 steamos-modeswitch-inhibitor:i386 steam:i386 nvidia-vdpau-driver:i386 libtxc-dxtn-s2tc0:i386 i965-va-driver:i386 libnvidia-encode1:i386 steamos-packages:i386 
# non-default-but-should-be
RUN apt-get install -yq pulseaudio:i386 bluetooth sudo libasound2-plugins:amd64

RUN adduser --gecos "" --disabled-password steam
RUN usermod -a -G audio,dip,video,plugdev,netdev,bluetooth,pulse-access steam

RUN date > /etc/skel/.imageversion
RUN cp /etc/skel/.imageversion /home/steam/.imageversion
RUN echo 'steam ALL = NOPASSWD: ALL' > /etc/sudoers.d/steam
RUN chmod 0440 /etc/sudoers.d/steam

ARG NVIDIA_DRIVER_VERSION
ADD http://http.download.nvidia.com/XFree86/Linux-x86_64/${NVIDIA_DRIVER_VERSION}/NVIDIA-Linux-x86_64-${NVIDIA_DRIVER_VERSION}.run /tmp/
RUN sh /tmp/NVIDIA-Linux-x86_64-${NVIDIA_DRIVER_VERSION}.run -a --skip-module-unload -q --no-nvidia-modprobe --no-rpms -b -r --no-kernel-module --no-x-check -z --no-cc-version-check --no-kernel-module-source --no-check-for-alternate-installs --no-unified-memory --no-drm --ui=none --no-distro-scripts --install-libglvnd -s

USER steam
ENV HOME /home/steam
VOLUME /home/steam

CMD ["steam"]
