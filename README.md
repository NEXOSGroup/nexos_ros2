# nexos_ros2

Central **civil** integration of the NEXOS ROS 2 stack (public, Apache-2.0).

This repo is the "our ROS 2 variant" meta-workspace: it pulls the per-technology
**driver repos** into a colcon workspace via [vcstool](https://github.com/dirk-thomas/vcstool)
and will host NEXOS-authored integration packages (bringup, robot descriptions,
shared messages).

## Structure

```
nexos_ros2.repos   vcstool manifest — which driver repos + versions to pull
src/               NEXOS-authored integration packages (nexos_* )   [added as needed]
```

## Build a workspace

```bash
mkdir -p ~/ros2_ws/src && cd ~/ros2_ws
# fetch the driver repos listed in the manifest
vcs import src < <(curl -fsSL https://raw.githubusercontent.com/NEXOSGroup/nexos_ros2/main/nexos_ros2.repos)
# ... plus install each driver's system prerequisites (see each repo's docs/BUILD.md)
source /opt/ros/lyrical/setup.bash
colcon build
```

## Technology drivers

| Technology | Repo | Notes |
|-----------|------|-------|
| maxon EPOS controller | [`nexos_ros2_epos`](https://github.com/NEXOSGroup/nexos_ros2_epos) | `ros2_control` over EPOS Command Library (USB/D2XX) |

Each technology lives in its **own public repo** `nexos_ros2_<technology>`,
independently versioned, with thorough docs under its `docs/`.

## Defence variant

The defence variant is private: `NEXOSGroup/nexos_ros2_defence`. It builds on this
integration plus the public drivers and adds defence-only packages/config/docs.
No defence content is in the public repos.

## Target platform

ROS 2 **Lyrical** on Ubuntu 26.04 (arm64), tested on Raspberry Pi 4.

> Repo/naming/doc standard: see memory `project_nexos_ros2_structure`.
