# ctrld

A Control-D-Inc DNS forwarding proxy compiled for arm64 for Mikrotik. Used it on my CCR2004 running smoothly without issues. It is humming on the latest release V1.30.

https://github.com/Control-D-Inc/ctrld

CR2004 only have 128MB of storage but I still have left 64% free after setting up this container.

1. Import 

Clone ctrld github site into my Ubuntu 20.04 server.
Recompile ctrld utility using the following code:
env GOOS=linux GOARCH=arm64 go build -a -gcflags=all"-l -B" -ldflags="-w -s" ./cmd/ctrld

Then compile into Docker container with only 3 files in my directory, a. ctrld utility, b. Dockerfile c. custom config file
I placed my custom config file in a subfolder, named "config".
run the folllowing in docker build
docker buildx build --no-cache --platform=linux/arm64 -t ctrld130:debian .
docker save ctrld130 > ctrld130_arm64.tar

Export ctrld130_arm64.tar to your PC/Mac and you can then import into your Mikrotik.
Create subfolder "config" in your Mikrotik and place your custom config into this folder.
Create a container with mount pointing to your custom "config" subfolder in no.7.
You should then be able to run ctrld utility in your Mikrotik.
You can streamline the process with a multistage Dockerfile instead but I was figuring out what went wrong hence the separate steps above.
