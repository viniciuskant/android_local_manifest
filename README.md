### Device specific configuration to build AOSP Android 16 for Raspberry Pi 5.

***

### How to build (Ubuntu 22.04 LTS):

1. Establish [Android build environment](https://source.android.com/docs/setup/start/requirements).

2. Install additional packages:

```
sudo apt-get install dosfstools e2fsprogs fdisk kpartx mtools rsync
```

3. Initialize repo:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-16.0.0_r3
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/viniciuskant/android_local_manifest/android-16.0/manifest_brcm_rpi.xml --create-dirs
```

Or optionally, you can reduce download size by creating a shallow clone and removing unneeded projects:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-16.0.0_r3 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/viniciuskant/android_local_manifest/android-16.0/manifest_brcm_rpi.xml --create-dirs
curl -o .repo/local_manifests/remove_projects.xml -L https://raw.githubusercontent.com/viniciuskant/android_local_manifest/android-16.0/remove_projects.xml

```

4. Sync source code:

```
repo sync
```

5. Setup Android build environment:

```
. build/envsetup.sh
```

6. Select the device `rpi5` and build target (tablet UI, `tv` for Android TV, or `car` for Android Automotive):

```
lunch aosp_rpi5-bp3a-userdebug
```
```
lunch aosp_rpi5_tv-bp3a-userdebug
```
```
lunch aosp_rpi5_car-bp3a-userdebug
```

7. Compile:

```
make bootimage systemimage vendorimage -j$(nproc)
```

8. Make flashable image:

```
./rpi5-mkimg.sh
```

Also look into [Linux kernel build instructions](https://github.com/raspberry-vanilla/android_kernel_manifest/tree/android-16.0).

***

### Issues:

- [Android](https://github.com/raspberry-vanilla/android_local_manifest/issues)
- [Linux kernel](https://github.com/raspberry-vanilla/android_kernel_manifest/issues)

***

### Wiki:

- [Audio](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Audio)
- [Desktop mode](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Desktop-mode)
- [DSI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/DSI-display)
- [HDMI display](https://github.com/raspberry-vanilla/android_local_manifest/wiki/HDMI-display)
- [HDMI-CEC](https://github.com/raspberry-vanilla/android_local_manifest/wiki/HDMI-CEC)
- [Interfaces](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Interfaces)
- [USB boot](https://github.com/raspberry-vanilla/android_local_manifest/wiki/USB-boot)
- [Utilities](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Utilities)
- [Video decoding & encoding](https://github.com/raspberry-vanilla/android_local_manifest/wiki/Video-decoding-&-encoding)
