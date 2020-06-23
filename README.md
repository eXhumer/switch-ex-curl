# switch-ex-curl
Modified version of [`switch-curl`](https://github.com/devkitPro/pacman-packages/tree/master/switch/curl) which includes mbdeltls SSL backend as default, along with libnx SSL backend as an alternative SSL backend.

To instead use the libnx SSL backend, call `curl_global_sslset(CURLSSLBACKEND_LIBNX)` before calling `curl_global_init()`.

LibNX SSL backend will not work for users who used Incognito/Incognito_RCM or on any switch with wiped PRODINFO partition, as it requires a valid SSL certificate which is stored in PRODINFO partition.

## Add pacman respository containing switch-ex-curl
You can follow the guide [here](https://github.com/eXhumer/pacman-packages#how-to-add-repository-to-pacman) to add a new repository to pacman which contains `switch-ex-curl`.

## Linker flags to add in external projects for linking switch-ex-curl with mbedtls SSL backend
```
-lcurl -lmbedtls -lmbedx509 -lmbedcrypto
```

## Linker flags to add in external projects for linking switch-ex-curl with mbedtls SSL backend
```
-lcurl -lnx
```

## Build Instructions
This package uses PKGBUILD/makepkg build system, used by Arch Linux based system.

### To build the package, installing any build pre-requisite needed
```
makepkg --syncdeps
```

### To install the package, installing any pre-requisite needed
```
makepkg --install
```
or
```
sudo (dkp-)pacman --upgrade switch-ex-curl-${pkgver}-${pkgrel}-any.pkg.tar.xz
```

Replacing `${pkgver}` and `${pkgrel}` with the version and release number of the built `.pkg.tar.xz` package.