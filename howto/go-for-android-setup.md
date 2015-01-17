Thanks @brnv for discovering correct order.

Installation process assumes that all development stuff will be located in
`$PLAYGROUND` dir.

1. Install packages (will take long time):

   * android-google-apis-19 (https://aur.archlinux.org/packages/android-google-apis-19)
   * android-ndk (https://aur.archlinux.org/packages/android-ndk)
   * android-platform-19 (https://aur.archlinux.org/packages/android-platform-19)
   * android-sdk-build-tools-19.1 (https://aur.archlinux.org/packages/android-sdk-build-tools-19.1)
   * android-sdk-platform-tools (https://aur.archlinux.org/packages/android-sdk-platform-tools)
   * android-sdk (https://aur.archlinux.org/packages/android-sdk)
   * android-udev (official repo)
   * apache-ant (official repo)

2. Bootstrap toolchain:

   ```
   /opt/android-ndk/build/tools/make-standalone-toolchain.sh \
     --platform=android-15 \
     --arch=arm \
     --install-dir=$PLAYGROUND/ndk-toolchain
   ```

3. Build Go with android crosscompilation:

   * go-android (https://aur.archlinux.org/packages/go-android)
   * run `makepkg` as :

     ```
     CC_FOR_TARGET=$PLAYGROUND/ndk-toolchain/bin/arm-linux-androideabi-gcc \
       makepkg
     ```

4. Copy examples (you can skip this step using `go get` as usual for the repo you want):

   ```
   mkdir -p $PLAYGROUND/go-mobile/src/
   cp -r /usr/share/go-android/misc/golang.org/ $PLAYGROUND/go-mobile/src/
   ```

5. Put in `$PATH` executable like this:
   https://github.com/seletskiy/dotfiles/blob/master/bin/setup-android-env-go

6. Connect android device, make sure it shown in `adb devices` list.

7. Compile and run `libhello` example:

   ```
   cd $PLAYGROUND/go-mobile/src/golang.org/x/mobile/example/libhello
   setup-android-env-go ./all.bash
   ```
