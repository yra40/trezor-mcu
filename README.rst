TREZOR Firmware
===============

http://bitcointrezor.com/

How to build Trezor firmware?
-----------------------------

1. Install Docker (from docker.com or from your distribution repositories)
2. ``git clone https://github.com/trezor/trezor-mcu.git``
3. ``cd trezor-mcu``
4. ``./firmware-docker-build.sh TAG`` (where TAG is v1.3.2 for example, if left blank the script builds latest commit)

This creates file ``output/trezor-TAG.bin`` and prints its fingerprint at the last line of the build log.

How to get fingerprint of firmware signed and distributed by SatoshiLabs?
-------------------------------------------------------------------------

1. Pick version of firmware binary listed on https://mytrezor.com/data/firmware/releases.json
2. Download it: ``wget -O trezor.signed.bin.hex https://mytrezor.com/data/firmware/trezor-1.1.0.bin.hex``
3. ``xxd -r -p trezor.signed.bin.hex trezor.signed.bin``
4. ``./firmware-fingerprint.sh trezor.signed.bin``

Step 4 should produce the same sha256 fingerprint like your local build (for the same version tag).

The reasoning for ``firmware-fingerprint.sh`` script is that signed firmware has special header holding signatures themselves, which must be avoided while calculating the fingerprint.
