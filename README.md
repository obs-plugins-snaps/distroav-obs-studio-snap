# DistroAV Snap for OBS Studio

This snap delivers [DistroAV](https://github.com/DistroAV/DistroAV) (formerly OBS-NDI)
to the [OBS Studio snap](https://snapcraft.io/obs-studio).
DistroAV adds NDI® support to OBS Studio, allowing you to send and receive high-quality,
low-latency audio and video over your local network.

This snap is paired with the **ndi-runtime** snap, which provides the proprietary
NDI SDK runtime library (`libndi.so`). Both snaps connect to OBS Studio via the
`obs-plugins` content interface.

## Installation

### Install from the Store

```shell
sudo snap install distroav-obs-studio
sudo snap install ndi-runtime
```

### Connect to the OBS Studio snap

```shell
sudo snap connect obs-studio:obs-plugins distroav-obs-studio:obs-plugins
sudo snap connect obs-studio:obs-plugins ndi-runtime:obs-plugins
```

Once connected, DistroAV will appear in OBS Studio under **Tools → DistroAV** and as a source/filter.

## Architecture

```
obs-studio
  ├── obs-plugins:distroav-obs-studio  →  /distroav-obs-studio/plugins/libdistroav.so
  └── obs-plugins:ndi-runtime           →  /ndi-runtime/lib/libndi.so.6
```

OBS Studio's launcher scans all connected plugin snaps: it loads `.so` files from
`/plugins` and adds `/lib` directories to `LD_LIBRARY_PATH`. DistroAV's `dlopen`
fallback finds `libndi.so.6` via the runtime linker path — no source patching needed.

NDI® is a registered trademark of Vizrt NDI AB. For more information about NDI, visit [ndi.video](https://ndi.video/).

## Building locally

```shell
snapcraft
```

The plugin is built against the libobs headers shipped in the
`obs-studio` snap, so no local OBS build is required.

The snap starts in `devel` grade; flip it to `stable` in
`snap/snapcraft.yaml` once the packaged plugin is verified to work.
