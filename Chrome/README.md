# Reproducing Chrome vulnerabilities

[Build](#build)

[Run](#run)

## Build

### Existing builds

Chrome has asan linux builds that can be used without building. If a vulnerability is known to be reproducable in a version of asan linux build, download directly using **gsutil**:

- install [gsutil](https://cloud.google.com/storage/docs/gsutil_install#sdk-install)

- copy an asan linux release build:

	```gsutil cp gs://chromium-browser-asan/linux-release/asan-linux-release-<build id>.zip```


### Own builds

:point_right: [Tutorial](https://chromium.googlesource.com/chromium/src/+/master/docs/linux/build_instructions.md)

#### 0. (First time only) install depot tool

```
	git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

add path of depot tool to $PATH, e.g. ```export PATH="$PATH:${HOME}/depot_tools"```

#### 1. get the code

```
	mkdir ~/chromium && cd ~/chromium
	fetch --nohooks chromium
```

To [checkout whatever version you need](http://www.chromium.org/developers/how-tos/get-the-code/working-with-release-branches):
```
	git fetch --tags
	git checkout refs/tags/<version number>
	gclient sync --with_branch_heads --with_tags
```

#### 2. build dependency
```
	cd src
	./build/install-build-deps.sh
	gclient runhooks
```

#### 3. configuration
```
	gn args out/<build name>
```
then enter configurations. For example, for an [asan build](https://chromium.googlesource.com/chromium/src/+/HEAD/docs/asan.md):
```
	is_asan= true
	is_debug = false
```

#### 4. build
```
	autoninja -C out/<build name> chrome
```

Other component can be built instead of chrome. For example, if just to build content shell: ```autoninja -C out/<build name> content_shell```


## Run

In build directory, run ```./chrome [<flag>]``` (or the component you built)

A list of flags available :point_right: [:link:](https://peter.sh/experiments/chromium-command-line-switches/)

### headless chrome

[Headless chrome](https://developers.google.com/web/updates/2017/04/headless-chrome) is supported:

run ```./chrome --no-sandbox --headless --disable-gpu <HTML file/ URL>```.

### run with asan

set asan flags: ``` export ASAN_OPTIONS="symbolize=1 external_symbolizer_path=../../third_party/llvm-build/Release+Asserts/bin/llvm-symbolizer detect_leaks=0 detect_odr_violation=0"```

then run as normal.

### trouble shooting

1. **run in remote server without a display**

use xvfb:
```
	sudo Xvfb :10 -ac
	export DISPLAY=:10
```

2. WARNING:discardable_shared_memory_manager.cc(188)] Less than 64MB of free space in temporary directory for shared memory files: 60

use flag: --disable-dev-shm-usage

3. **Failed to connect to the bus**: Failed to connect to socket /var/run/dbus/system_bus_socket: No such file or directory

check if there is ```system_bus_socket``` in ```/var/run/dbus/```, if not:

```
	sudo /etc/init.d/dbus restart
```

and check again. ([:link:](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=444668))


## Debug (Linux)

:point_right: [tutorial](https://chromium.googlesource.com/chromium/src/+/81c0fc6d4/docs/linux_debugging.md)

:point_right: [debug blink](https://www.chromium.org/blink/getting-started-with-blink-debugging)

To debug renderer:

```
	./content_shell --no-sandbox --renderer-startup-dialog --headless --disable-gpu /path/to/html
```

This will pause the renderer. Attach the renderer process to gdb:

```
	gdb -p <pid>
```

To continue the render, send signal in gdb: ```signal SIGUSR1```
