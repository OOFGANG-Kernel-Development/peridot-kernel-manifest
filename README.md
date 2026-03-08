# peridot-kernel-manifest

`repo` manifest for the Xiaomi peridot (SM8650) Android 14 kernel.

This manifest describes all the git repos needed to build the kernel. It is consumed by Google's `repo` tool — or automatically by `build.sh` in the workspace repo.

---

## Quick Start (recommended)

Use the all-in-one build script from the workspace repo — it handles everything automatically:

```bash
git clone https://github.com/ApexLegend007/sm8650-peridot-kernel
cd sm8650-peridot-kernel
./build.sh
```

Select **"1) Full setup + build"** on first run.

---

## Manual repo Setup (advanced)

If you prefer to use `repo` directly:

```bash
# Create a build directory
mkdir peridot-kernel && cd peridot-kernel

# Initialise repo with this manifest
repo init -u https://github.com/ApexLegend007/peridot-kernel-manifest -b main --depth=1

# Sync all sources
repo sync -c --no-tags --no-clone-bundle -j$(nproc)

# Then run the build script from the synced workspace root
./build.sh --skip-toolchain   # if clang is already present
# or
./build.sh                    # downloads clang and builds
```

> **Note**: `repo init` requires the target directory to **not** already contain a `.git` folder. If you have already `git clone`d the workspace repo, use `build.sh` directly — it detects the pre-cloned environment and uses per-repo `git clone` automatically.

---

## Projects in this Manifest

| Project | Path | Remote | Branch |
|---------|------|--------|--------|
| sm8650-peridot-kernel | `.` (workspace root) | ApexLegend007 | `main` |
| peridot-msm-kernel | `msm-kernel` | ApexLegend007 | `peridot-u-oss` |
| peridot-kernel-devicetree | `msm-kernel/arch/arm64/boot/dts/vendor` | ApexLegend007 | `peridot-u-oss` |
| peridot-kernel-build | `build/kernel` | ApexLegend007 | `peridot-u-oss` |
| peridot-bazel-common-rules | `build/bazel_common_rules` | ApexLegend007 | `android14-release` |
| peridot-external-dtc | `external/dtc` | ApexLegend007 | `master` |
| peridot-external-bazel-skylib | `external/bazel-skylib` | ApexLegend007 | `master` |
| peridot-external-absl-py | `external/python/absl-py` | ApexLegend007 | `master` |
| peridot-external-stardoc | `external/stardoc` | ApexLegend007 | `main` |
| peridot-kernel-prebuilts-build-tools | `prebuilts/kernel-build-tools` | ApexLegend007 | `main` |
| kernel_xiaomi_sm8650-modules | `vendor` | ApexLegend007 | `main` |
| platform/system/tools/mkbootimg | `tools/mkbootimg` | AOSP | `android14-release` |

**Not managed by repo** (set up by `build.sh`):
- `prebuilts/clang/host/linux-x86/clang-r487747c` — downloaded as tarball from AOSP
- `tools/bazel` — Bazelisk binary downloaded from GitHub releases
- `prebuilts/build-tools/path/` — machine-local tool symlinks created at build time

---

## Device Info

| Item | Value |
|------|-------|
| Device codename | peridot |
| Marketing name | Xiaomi peridot / POCO F6 / Redmi Turbo 3 |
| SoC | SM8650 (Snapdragon 8 Gen 3) |
| Platform (Qualcomm) | pineapple |
| Android | 14 (U) |
| Kernel | 6.1 GKI 2.0 |
| Compiler | clang-r487747c (LLVM 17) |
| Build system | Kleaf (Bazel) |

---

## More Information

See the [workspace repo README](https://github.com/ApexLegend007/sm8650-peridot-kernel) for full build instructions, troubleshooting, and flashing guide.
