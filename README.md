# GLAD-CMAKE-INSTALL

### build the project

```bash
git clone https://github.com/pumpkinblade/glad-cmake-install
cd glad-cmake-install
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

### install

```bash
sudo cmake --install build
```

or

```bash
cmake --install build --prefix <your-install-directory>
```

### how to use

```cmake
find_package(glad CONFIG REQUIRED)
target_link_libraries(main PRIVATE glad::glad)
```
