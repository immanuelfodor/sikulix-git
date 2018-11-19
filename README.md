# SikuliX 1.1.4 Manjaro (Arch) Linux package

## Tested on Manjaro Linux (64-bit)

```bash
uname -a
# Linux pc-name 4.19.1-1-MANJARO #1 SMP PREEMPT Sun Nov 4 16:05:34 UTC 2018 x86_64 GNU/Linux
```

## Usage of this repo

```bash
# install dependencies
# you might need different language packs for tesseract
sudo pacman -S jdk-10-openjdk jre-10-openjdk jre-10-openjdk-headless tesseract tesseract-data-eng tesseract-data-hun opencv wmctrl lsb-release xdotool maven git
# set default JDK version to the installed version
# @see: https://wiki.archlinux.org/index.php/java
sudo archlinux-java set java-10-openjdk
sudo archlinux-java status

# clone this repo and build the package
git clone https://github.com/immanuelfodor/sikulix-git.git
cd sikulix-git
makepkg
```

## Starting from scratch

If things go sour, we can clean up our folder:

```bash
rm -rf src
rm -rf sikulix-git
rm -rf pkg
```

# Known issues

The build executes but fails at the package installation step as the repo structure is different for SikuliX 1.1.4 and it can't find some files.

My workaround was to get `jython` and the pre-compiled `sikulix` JAR from the developer to be able to run it:

```bash
sudo yaourt -S opencv-java

mkdir -p $HOME/.Sikulix/Extensions
mkdir -p $HOME/sikulix
cd sikulix

wget -O $HOME/.Sikulix/Extensions/jython-standalone-2.7.1.jar https://repo1.maven.org/maven2/org/python/jython-standalone/2.7.1/jython-standalone-2.7.1.jar

wget -O sikulix.jar https://raiman.github.io/SikuliX1/sikulix.jar
java -jar sikulix.jar -v
java -jar sikulix.jar
```

But it also fails with an error:

```
[error] RunTimeIDE: loadLib: opencv_java not usable: 
java.lang.UnsatisfiedLinkError: no opencv_java in java.library.path: [/usr/java/packages/lib, /usr/lib64, /lib64, /lib, /usr/lib]
[error] RunTimeIDE:  *** terminating: problem with native library: opencv_java
```

:(
