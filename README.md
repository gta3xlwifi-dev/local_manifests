## Local_manifests

This readme provides instructions for setting up the local manifest for building AOSP (Android Open Source Project) on the Galaxy Tab A 10.1 (2019).


Before diving in, make sure you have the following installed:

Ubuntu is the standard build environment for anything Android 

```
sudo apt-get install bison g++-multilib git git-lfs gperf libxml2-utils make zip liblz4-tool libssl-dev bc flex curl python3-full python-is-python3 zlib1g-dev libelf-dev dwarves
```

For Ubuntu Mantic (23.10) and newer, you'll need to install additional dependencies due to library versioning changes. Run the following commands to install the required versions of `libtinfo` and `libncurses`:

```
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.4-2_amd64.deb && sudo dpkg -i libtinfo5_6.4-2_amd64.deb && rm -f libtinfo5_6.4-2_amd64.deb
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.4-2_amd64.deb && sudo dpkg -i libncurses5_6.4-2_amd64.deb && rm -f libncurses5_6.4-2_amd64.deb
```
**Installing and Configuring the repo Tool**

The `repo` tool is essential for managing the manifest files required for building AOSP or working with other large-scale repositories. While it's available through Ubuntu repositories, it will not always provide the latest version.

1. Create a directory named `.bin` in your home directory to store the `repo` binary:

```
$ mkdir -p ~/.bin
```

2. Update your PATH to include the created `.bin` directory. Add this to the end of your ~/.bashrc file.

```
 PATH="${HOME}/.bin:${PATH}"
```

3. Download the latest version of the `repo` tool from Google Cloud Storage:

```
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
```

4. Grant executable permissions to the `repo` binary:

```
$ chmod a+rx ~/.bin/repo
```


**Initializing the Repository**

1. Initialize the repo using the following command:

```
repo init -u git://github.com/LineageOS/android.git -b lineage-18.0 --git-lfs
```

This command fetches the LineageOS manifest repository from GitHub and initializes it using the `lineage-18.0` branch. The `--git-lfs` flag ensures downloading large files efficiently.

2. Synchronize the repository with the latest changes:

```
repo sync -j64 --optimized-fetch
```

Have fun.

**Note:** Replace `lineage-18.0` with the desired LineageOS branch name corresponding to the Android version you want to build.

I will assume familiarity with AOSP development, as this list is not exhaustive.
