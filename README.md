# fix-pm2-ENOMEM-error-thrown-after-spawn
fix pm2 ENOMEM error thrown after spawn

```
I had the same problem and as it turned out, my system had no swap space enabled. Check if this is the case by running the command free -m:
```

```
Looking at the bottom row we can see we have a total of 0 bytes swap memory. Not good. Node can get pretty memory hungry and if no swap space is available when memory runs out, errors are bound to happen.
```


```
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab
```


ref: https://stackoverflow.com/questions/26193654/node-js-catch-enomem-error-thrown-after-spawn
