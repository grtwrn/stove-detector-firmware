# KitchenEye firmware releases

Compiled, **signed** firmware for KitchenEye units. Source is private; this repo
holds only what the units download over the air.

```
esp32/manifest.json          build number, size, SHA-256 of the firmware
esp32/manifest.sig           ECDSA P-256 signature over manifest.json
esp32/firmware-<build>.bin
```

Public on purpose. The binaries contain no secrets — each unit's credentials are
provisioned separately onto the device. What makes an update trustworthy is the
signature: a unit installs an image only if the manifest verifies against the
public key compiled into its firmware, the build is newer than what it runs, and
the download matches the signed SHA-256. Anything else is refused.

Published by `esp32/provision-esp32.sh release --push`. Don't edit by hand — a
changed manifest without a fresh signature is rejected by every unit.
