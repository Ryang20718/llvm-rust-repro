LLVM 20 + Rust 1.87 macro coverage bug

To repro:
```
cd examples/all_crate_deps/; bazelisk coverage //:my_library_test
```
