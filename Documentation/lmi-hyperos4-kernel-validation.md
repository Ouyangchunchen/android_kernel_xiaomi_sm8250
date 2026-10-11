# LMI HyperOS 4 kernel changes (2026-10-11)

Source base: a8adb96703d64a427c99a1456e7fbcc95ede6313.
Baseband-guard: a54e0dc6cf0aff4dd87fec49644a02d2eb612905, tracked as a pinned submodule.
Clone with --recurse-submodules, or run git submodule update --init Baseband-guard.
The security/baseband-guard symlink points to this dependency.

## Validation recorded before publication

The Wi-Fi power statistics changes and the signal change passed a full MIUI / NoKernelSU Image build. The effective configuration included Baseband-guard. Build intermediates and output were stored on the WSL Linux filesystem.

Wi-Fi-only Image SHA256: ac94cedc600c8fffce5b632d38098616bec0bd9b510d3c6cbe8677a6adc9607e.
Image including the signal change SHA256: 3620821f5504b981b98695d21bd534a8de0d5dd66c5893066d37c1ff2b64efc5.
Both Images were 47190032 bytes. Recorded effective .config SHA256: 3b49f9c7f73e4e5e9143e03c9ab4d96a39e874a0aadd2837b04d3d1b2abf7906.

The signal change was verified in vmlinux disassembly and in the emitted Image. The SIGKILL branch still queries CAP_KILL. Its runtime effect has not been verified; the publication does not claim that this Image has been flashed.

The Wi-Fi interface reuses actual firmware statistics; it does not synthesize values. This does not supply the missing cnss_diag_socket transmit-power backend.

## Configuration caveat

kernel/Makefile embeds lmi_stock-defconfig into /proc/config.gz for lmi. That embedded file must not be treated as the effective configuration of the running build. Use the actual build .config and runtime evidence.

These commits contain kernel source changes only. Recovery ramdisk property changes and Android userspace patches are separate work.
