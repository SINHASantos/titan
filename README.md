# Titan: A RocksDB Plugin to Reduce Write Amplification

[![Build Status](https://travis-ci.org/tikv/titan.svg?branch=master)](https://travis-ci.org/tikv/titan)
[![codecov](https://codecov.io/gh/tikv/titan/branch/master/graph/badge.svg)](https://codecov.io/gh/tikv/titan)

Titan is a RocksDB Plugin for key-value separation, inspired by 
[WiscKey](https://www.usenix.org/system/files/conference/fast16/fast16-papers-lu.pdf).
For introduction and design details, see our
[blog post](https://pingcap.com/blog/titan-storage-engine-design-and-implementation/).

## Build and Test
Titan relies on RocksDB source code to build. You need to checkout RocksDB source code locally,
and provide the path to Titan build script.
```
# To build:
mkdir -p build
cd build
cmake ..
make -j<n>

# To specify custom rocksdb
cmake .. -DROCKSDB_DIR=<rocksdb_source_dir>
# or
cmake .. -DROCKSDB_GIT_REPO=<git_repo> -DROCKSDB_GIT_BRANCH=<branch>

# Build static lib (i.e. libtitan.a) only:
make titan -j<n>

# Release build:
cmake .. -DROCKSDB_DIR=<rocksdb_source_dir> -DCMAKE_BUILD_TYPE=Release

# Building with sanitizer (e.g. ASAN):
cmake .. -DROCKSDB_DIR=<rocksdb_source_dir> -DWITH_ASAN=ON

# Building with compression libraries (e.g. snappy):
cmake .. -DROCKSDB_DIR=<rocksdb_source_dir> -DWITH_SNAPPY=ON

# Run tests after build. You need to filter tests by "titan" prefix.
ctest -R titan

# To format code, install clang-format and run the script.
bash scripts/format-diff.sh
```

## Compatibility with RocksDB

| Titan Version | TiKV Version | RocksDB Version (TiKV fork) |
| --------------| ------------- | ---------------------------- |
| master        | 8.5.0 +       | [8.10.tikv]                  |
| [tikv-7.5]    | 7.5.0 +       | [6.29.tikv]                  |
| [tikv-7.1]    | 7.1.0 +       | [6.29.tikv]                  |
| [tikv-6.5]    | 6.5.0 +       | [6.29.tikv]                  |
| [tikv-6.1]    | 6.1.0 +       | [6.4.tikv]                   |

[6.4.tikv]: https://github.com/tikv/rocksdb/tree/6.4.tikv
[6.29.tikv]: https://github.com/tikv/rocksdb/tree/6.29.tikv
[8.10.tikv]: https://github.com/tikv/rocksdb/tree/8.10.tikv
[tikv-6.1]: https://github.com/tikv/titan/tree/tikv-6.1
[tikv-6.5]: https://github.com/tikv/titan/tree/tikv-6.5
[tikv-7.1]: https://github.com/tikv/titan/tree/tikv-7.1
[tikv-7.5]: https://github.com/tikv/titan/tree/tikv-7.5
