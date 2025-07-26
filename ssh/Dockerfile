FROM scratch
COPY --from=lscr.io/linuxserver/openssh-server:10.0_p1-r7-ls200 / /rootfs/usr/local/lib/containers/ssh
COPY ssh.yaml /rootfs/usr/local/etc/containers/ssh.yaml
COPY manifest.yaml /
RUN ls -hal /rootfs/usr/local/lib/containers/ssh
WORKDIR /rootfs/usr/local/lib/containers/ssh/


