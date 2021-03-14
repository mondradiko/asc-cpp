# Building asc-cpp

## Dependencies

### Wasmtime

Instructions for installing Wasmtime can be found [here](https://wasmtime.dev).

### Binaryen

Prebuilt packages for Binaryen can be found [here](https://github.com/WebAssembly/binaryen/releases/latest).

Alternatively, Binaryen can be built from source:
```bash
git clone https://github.com/WebAssembly/binaryen.git
cd binaryen
mkdir builddir
cd builddir
cmake ... -G Ninja
ninja
sudo ninja install
```

## Building

To be determined...