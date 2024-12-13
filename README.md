# k8s-gke

1. Create cluster on gg cloud
2. Rancher
   a. Create VM server: rancher-server
   b. Add disk to store data
   c. Mount disk on rancher-server
     ```
     # sudo mkfs.ext4 -m 0 /dev/sdb
     # mkdir /data
     # echo "/dev/sdb  /data  ext4  defaults  0  0" | sudo tee -a /etc/fstab
     # mount -a
     # sudo df -h
     ```
   d. Install docker, docker-compose, rancher (check rancher version - k8s compatibility)
     ```
     docker run --name rancher-server -d --restart=unless-stopped -p 80:80 -p 443:443 -v /data/rancher:/var/lib/rancher --privileged rancher/rancher:v2.10.0
     docker logs  rancher-server  2>&1 | grep "Bootstrap Password:"
     ```
   e. Use public IP of rancher-server to access
