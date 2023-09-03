# A ctrld utility recompiled for Mikrotik router

Reference from Control-D-Inc source.
https://github.com/Control-D-Inc/ctrld

A Control-D-Inc DNS forwarding proxy compiled in arm64 for Mikrotik router. Used on my CCR2004 running smoothly without issues. It is humming on the latest release V1.30.
I've recompiled the arm64 binary release from Control-D-Inc as it includes upx compression. Mikrotik container does not have the necessary dependencies to run it.

CCR2004 only have 128MB of storage but I still had left about 64% free after setting up this container.

1. Import .tar file into your Mikrotik using its File Manager or FTP.
2. Create a new Mount giving any name "ctrld_config", Src= /"location of custom toml in your Mikrotik", Dst=/etc/controld
   e.g. name=ctrld src=/config dst=/etc/controld
3. Upload your config.toml into the config folder in Mikrotik e.g. /config/config.toml
4. Create a new container with the parameters: Interface="veth1" Root Dir="ctrld" Mounts="ctrld_config". Check the boxes for "Logging" and "Start on Boot". "Logging" is optional.
5. Once container is created, you should see Tag=ctrld130:debian OS:linux Arch:arm64.
6. You can then start the container.

You can change the names of folders accordingly but do match these name change to th parameters of your container and mount.
