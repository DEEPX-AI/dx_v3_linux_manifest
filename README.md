# rt_v3_linux_manifest
v3 linux manifest based on buildroot

## Source structure
| Directory           | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| trusted-firmware-m  | Provides the Secure Processing Environment and Bootcode for the Cortex-AM0  |
| trusted-firmware-a  | Provides the secure world software for the Cortex-A53                       |
| u-boot              | Embedded boot loader for the Cortex-A53                                     |
| linux               | Linux kernel                                                                |
| buildroot           | embedded root file system                                                   |
| tools               | Project and cross-toolchain building tools, and more                        |

## Download
```console
$ repo init -u https://github.com/DEEPX-AI/dx_v3_linux_manifest.git
$ repo sync
```

## Build with build script (build.sh)
- This is a shell script that supports building. This script build using the entered options.
```console
 Usage:
	build.sh <option>

 option:
	-m 		 menuconfig to select config
	-p [config]	 set build config.
	-t [target]	 set config's target.
	-i [image]	 select build target.
	-c [command] run commands supported by target.
	-o [option]	 add option to build,config,install (each step).
	-f 		     force build the next target even if a build error occurs
	-j [jobs]	 set build jobs
	-l		     listup targets in config
	-e		     edit config : /home/jhk/deepx/v3/git/tools/project/v3_haps.bs
	-v		     build verbose

 Build commands supported by target type :
* cmake	| commands : build install delete config prepare finalize clean complete 'misc command'
* 	    | order    : prepare config build finalize install complete
* meson	| commands : build install delete config prepare finalize clean complete 'misc command'
* 	    | order    : prepare config build finalize install complete
* make	| commands : build install delete prepare finalize clean complete 'misc command'
* 	    | order    : prepare build finalize install complete
* linux	| commands : build install delete prepare defconfig finalize clean menuconfig complete 'misc command'
* 	    | order    : prepare defconfig build finalize install complete

```

### Sselect project
```console
$ ./build -m
```
### Build all
```console
$ ./build.sh
```
### Build target
- Listup build targets
```console
$ ./build.sh -l

 * tfm      : cmake  - bl1_binaries bl2_binaries tfm_s_binaries
 * tfa      : make   - bl31
 * uboot    : linux  - u-boot.bin
 * linux    : linux  - Image deepx/v3-haps.dtb
 * br2      : linux  -
```

- Build target
- $ ./build.sh -t `<target>`
```console
$ ./build.sh -t linux
```
