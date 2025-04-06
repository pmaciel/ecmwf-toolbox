# ECMWF Toolbox

This is a CMake-based bundle for building various ECMWF libraries and tools.

Features:
- Modular build configuration via CMake options
- Git submodules for dependencies

Requirements:
- CMake ≥ 3.12
- C++17 compiler
- Git

## Getting Started

Clone with submodules
```bash
git clone --recurse-submodules https://github.com/pmaciel/ecmwf-toolbox.git
cd ecmwf-toolbox
```

If you already cloned without `--recurse-submodules`, run:
```bash
git submodule update --init --recursive
```

Configure and build:
```bash
mkdir build && cd build
cmake ..  # add options eg. -G Ninja -DWITHOUT_METVIEW=ON
cmake --build .
```

---

For more information, refer to the individual component documentation.
