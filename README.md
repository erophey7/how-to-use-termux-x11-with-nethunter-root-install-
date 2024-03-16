# How to use termux-x11 with nethunter root

Instructions for using termux-x11 with kali nethunter:
1) Installation and setting up of termux and termux-x11:

  * Install termux from fdroid, run termux
  * Run commands:
  ```
$ pkg update && pkg upgrade
$ pkg intall x11-repo
$ pkg install root-repo
$ pkg install termux-x11-nightly tsu
  ```
  * Uncomment `allow-external-apps = true` in `termux_home/.termux/termux.properties`
  * Download termux-x11 apk from [Github](https://github.com/termux/termux-x11/releases/tag/nightly)
  * Test termux-x11: run
   ```
termux-x11 :1 &
pkg install firefox-esr     # or any GUI application
export DISPLAY=:1
firefox                     # or the application you installed
kill -                      # - is termux-x11 PID
   ```
2) Script to run termux-x11 from android shell

 `# nano path/to/script/x11_start` recomended path: `
/data/data/com.offsec.nhterm/files/home/.nhterm/script/x11_start`  ```
#!/system/bin/sh

export USER= #run whoami in termux

### Setup env ###

export SHELL=/data/data/com.termux/files/usr/bin/bash
export LD_PRELOAD=/data/data/com.termux/files/usr/lib/libtermux-exec.so
export BOOTCLASSPATH=/apex/com.android.art/javalib/core-oj.jar:/apex/com.android.art/javalib/core-libart.jar:/apex/com.android.art/javalib/okhttp.jar:/apex/com.android.art/javalib/bouncycastle.jar:/apex/com.android.art/javalib/apache-xml.jar:/system/framework/framework.jar:/system/framework/framework-graphics.jar:/system/framework/ext.jar:/system/framework/telephony-common.jar:/system/framework/voip-common.jar:/system/framework/ims-common.jar:/system/framework/telephony-ext.jar:/system/framework/WfdCommon.jar:/apex/com.android.i18n/javalib/core-icu4j.jar:/apex/com.android.adservices/javalib/framework-adservices.jar:/apex/com.android.adservices/javalib/framework-sdksandbox.jar:/apex/com.android.appsearch/javalib/framework-appsearch.jar:/apex/com.android.btservices/javalib/framework-bluetooth.jar:/apex/com.android.configinfrastructure/javalib/framework-configinfrastructure.jar:/apex/com.android.conscrypt/javalib/conscrypt.jar:/apex/com.android.devicelock/javalib/framework-devicelock.jar:/apex/com.android.healthfitness/javalib/framework-healthfitness.jar:/apex/com.android.ipsec/javalib/android.net.ipsec.ike.jar:/apex/com.android.media/javalib/updatable-media.jar:/apex/com.android.mediaprovider/javalib/framework-mediaprovider.jar:/apex/com.android.ondevicepersonalization/javalib/framework-ondevicepersonalization.jar:/apex/com.android.os.statsd/javalib/framework-statsd.jar:/apex/com.android.permission/javalib/framework-permission.jar:/apex/com.android.permission/javalib/framework-permission-s.jar:/apex/com.android.scheduling/javalib/framework-scheduling.jar:/apex/com.android.sdkext/javalib/framework-sdkextensions.jar:/apex/com.android.tethering/javalib/framework-connectivity.jar:/apex/com.android.tethering/javalib/framework-connectivity-t.jar:/apex/com.android.tethering/javalib/framework-tethering.jar:/apex/com.android.uwb/javalib/framework-uwb.jar:/apex/com.android.virt/javalib/framework-virtualization.jar:/apex/com.android.wifi/javalib/framework-wifi.jar
export PATH=/data/data/com.termux/files/usr/bin
export TMPDIR=/data/local/nhsystem/kali-arm64/tmp

### Run termux-x11 ###

echo $1
/data/data/com.termux/files/usr/bin/termux-x11 $1
 ```
 Edit `export USER=` with termux output without root `whoami`

  * Save the script and run from root `chmod +x path/to/script/x11_start`

3) Usage
  * Run script from root shell `path/to/script/x11_start :1` :1 is display number
  * Set display in kali shell `export DISPLAY=:1`
  * Run GUI app in kali shell
  
