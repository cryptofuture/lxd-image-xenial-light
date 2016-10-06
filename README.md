# lxd-image-xenial-light
###### Light image with Ubuntu Xenial for use with lxc/lxd
Import:
* Download [xenial-light.tar.gz](https://github.com/cryptofuture/lxd-image-xenial-light/raw/master/xenial-light.tar.gz)
* Check sha256sum with `sha256sum xenial-light.tar.gz`.
```
# Correct output:
03b10effb5a45f0ed0bcacd9a03f62b72850f68b3331ca8be02130975853499b  xenial-light.tar.gz
```
* Import image with: `lxc image import xenial-light.tar.gz --alias xenial-light`
