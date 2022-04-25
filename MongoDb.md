# MongoDB Tshoot

<details>
  
<summary> MongoDB VM instances not starting the on reboot </summary>

Context: The MongoDB VMware instances cluster has been created via tar archive, on a separate user "mongo". The "start_mongo" script is not being run upon reboot.

Diagnosis: The log files of microservice shows connection issue with the DB server; as well as other VMs in the cluster.

Solution: Make "start_mongo" script to run at boot time.

To see last reboots:

```bash
$ last reboot
```

To add a command to start at boot time:

1. Cron
```bash
$ crontab -e

@reboot full/path/to/script
```

2. Systemd
```bash
[Unit]
Description=Job that runs your user script

[Service]
ExecStart=full/path/to/script
Type=oneshot
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
  
Resources:
- [Run-scripts-on-startup | Askubuntu ](https://askubuntu.com/questions/814/how-to-run-scripts-on-start-up)
</details>
