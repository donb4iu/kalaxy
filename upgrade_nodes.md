    #containerd_version: 1.4.3-1
    # Do you want to delete local data in k3s, k8s and Docker upon teardown?
    #delete_local_data: no
    #docker_apt_key_id: 8D81803C0EBFCD88
    #docker_apt_key_url: "https://download.docker.com/linux/{{ ansible_lsb.id.lower() }}/gpg"
    #docker_apt_repository: "deb https://download.docker.com/linux/{{ ansible_lsb.id.lower() }} {{ ansible_lsb.codename.lower() }} stable"
    # Make sure to match the `no_proxy` list or otherwise expect Docker images to be proxied twice:
    #docker_registry_mirror_url: https://my-docker-registry-mirror.local/
    #docker_version: "5:20.10.0~3-0~{{ ansible_lsb.id.lower() }}-{{ ansible_lsb.codename.lower() }}" # (https://docs.docker.com/install/linux/docker-ce/ubuntu/)
    #k3s_version: v1.19.5+k3s1 # (https://github.com/rancher/k3s/releases)
    #k8s_version: 1.19.5-00 # (https://github.com/kubernetes/kubernetes/releases)
    #locale: C.UTF-8
    # Make sure to match all nodes and the `docker_registry_mirror_url`:
    #no_proxy: 127.0.0.1,.local,localhost
    # Make sure to use an IP address, not a hostname, or otherwise expect the Kubernetes setup to fail:
    #proxy_url: http://10.0.0.1:3128/
    #timezone: UTC
    
    
    
    
- hosts: raspberry_pi
  roles:
    - raspberry-pi-up
- hosts: amd64
  roles:
    - amd64-up
- hosts: raspbian
  roles:
    - raspbian-up
- hosts: rpi4
  roles:
    - ubuntu-up
- hosts: amdC2
  roles:
    - ubuntu-up
- hosts: raspbian
  roles:
    - debian-up
- hosts: rpi4
  roles:
    - debian-up
- hosts: amdC2
  roles:
    - debian-up
- hosts: all
  roles:
    - docker-up
- hosts: k3s_master
  roles:
    - k3s-master-up
  run_once: yes
- hosts: k3s_worker
  roles:
    - k3s-worker-up
- hosts:
    - k8s_master
    - k8s_worker
  roles:
    - k8s-commons-up
- hosts: k8s_master
  roles:
    - k8s-master-up
  run_once: yes
- hosts: k8s_worker
  roles:
    - k8s-worker-up
