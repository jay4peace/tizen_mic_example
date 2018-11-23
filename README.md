
# How to create custom Tizen IoT image.

* Prerequisites
	- OS : Ubuntu 16.04 LTS
	- Install Git Build System(GBS) and Image Creator(MIC) for Tizen developer
	```shell
	$ echo "deb [trusted=yes] http://download.tizen.org/tools/latest-release/Ubuntu_16.04/ /" >> /etc/apt/sources.list
	$ sudo apt-get update
	$ sudo apt-get install gbs mic
	```
	> See [Installing Development Tools](https://source.tizen.org/ko/documentation/developer-guide/getting-started-guide/installing-development-tools) page in Tizen Developer Site to get more detail.

1. Download `Kickstart(.ks)` file from Tizen download site.

	- for example tizen-unified IoT headless for artik image
		```shell
		$ wget http://download.tizen.org/snapshots/tizen/unified/tizen-unified_20181122.2/images/standard/iot-headless-2parts-armv7l-artik530_710/tizen-unified_20181122.2_iot-headless-2parts-armv7l-artik530_710.ks
		```
2. Edit `kickstart(.ks) file`

	* Add building block name which you needed, in `%packages` section in `kickstart` file

		```ks
		%packages
		# @ IoT Headless Base
		...
		# @ IoT Adaptation Artik530_710 Headless
		...

		# camera blocks  <-- New building block to use camera API added
		building-blocks-sub2-Preset_boards-ARTIK530-Camera_Headless

		%end
		```

	> To find a specific building block name, please refer to [mapping-bb-rs.xml](https://git.tizen.org/cgit/tools/building-blocks/plain/mapping-bb-rs.xml?h=tizen_5.0) in Tizen building block repository.

3. make image
	```shell
	$ gbs createimage --ks-file=xxxxx.ks
	```
	* You can find a new custom image in `mic-output` directory
	```shell
	$ ls -al ./mic-output
	```

> See [Creating Tizen Images with MIC](https://source.tizen.org/ko/documentation/developer-guide/getting-started-guide/creating-tizen-images-mic) to get more detail.
