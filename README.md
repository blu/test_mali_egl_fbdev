Burning GPU cycles on Arm Mali via EGL fbdev
------------------------------------------------

This is a quick'n'dirty compilation of GPU unit tests that were built for aarch64-a64/arm64 and arm-mali-fbdev userspace blob.
Hypothetically they should run on any arm64 userland featuring a mali-fbdev GLES3 stack, but in practice they were run (and tuned) only on ODROID-N2 with `/dev/fb0` of 32-bit pixel depth.

How to run
----------

Each individual test can be run via its corresponding binary but that requires familiarity with the test CLI. Alternatively, a dedicated script `test.sh` is provided that runs all four unit tests in a row, for a set number of frames, and finally prints the SoC temperatures. That script was written and tested on an ODROID-N2 -- using it on other hosts will require apt editing. At the very minimum changes to the hardcoded `taskset` and EGL configs are expected on non-N2 hosts.

Due to the nature of mali-fbdev stack as of this writing, running the tests requires root privileges. For instance, run the script as:

	sudo bash -c ./test.sh

If root priviledges are not provided, test session terminates abruptly with an `EGL_BAD_MATCH` error while attempting an `eglCreateWindowSurface` EGL call.
