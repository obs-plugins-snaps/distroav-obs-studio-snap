# DistroAV Snap for OBS Studio

This snap delivers [DistroAV](https://github.com/DistroAV/DistroAV) (formerly OBS-NDI)
to the [OBS Studio snap](https://snapcraft.io/obs-studio).
DistroAV adds NDI® support to OBS Studio, allowing you to send and receive high-quality,
low-latency audio and video over your local network.

## Installation

### Install from the Store

```shell
sudo snap install distroav-obs-studio
```

### Connect to the OBS Studio snap

```shell
sudo snap connect obs-studio:obs-plugins distroav-obs-studio:obs-plugins
```

Once connected, DistroAV will appear in OBS Studio under **Tools → DistroAV** and as a source/filter.

NDI® is a registered trademark of Vizrt NDI AB. For more information about NDI, visit [ndi.video](https://ndi.video/).

> [!WARNING]
> The current `snapcraft.yaml` bundles the NDI SDK (proprietary) alongside the GPL-licensed DistroAV plugin.
> This means the snap as a whole is not distributable as GPL, and the NDI library loading does **not**
> actually work at runtime—the plugin fails to find `libndi.so.6`. This is **not legal advice**; consult a
> lawyer if you have concerns about license compatibility.
