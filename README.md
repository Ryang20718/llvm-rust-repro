LLVM 20 + Rust 1.87 macro coverage bug

To repro:
```
cd examples/all_crate_deps/; bazelisk coverage //:my_library_test
```

```
// Copyright 2015 The Bazel Authors. All rights reserved.
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//    http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

fn main() -> anyhow::Result<()> {
    println!("Hello, world!");
    Ok(())
}


#[cfg(test)]
mod tests {

    #[test]
    fn test_main() {
    log::info!(
        "Worker {} Testing {}",
        "TESTGINGGGGGGGOKOERKOEKROEKROEKROKER",
        "TESTGINGGGGGGGOKOERKOEKROEKROEKROKER",
    );
    }
}

```

Generated coverage is where line 26 is covered, but line 27 isn't (the second line of the macro

```
SF:src/main.rs
FN:15,_RNvCsfJqfc9I5GUN_10my_library4main
FN:25,_RNvNtCsfJqfc9I5GUN_10my_library5testss_9test_main
FNDA:0,_RNvCsfJqfc9I5GUN_10my_library4main
FNDA:1,_RNvNtCsfJqfc9I5GUN_10my_library5testss_9test_main
FNF:2
FNH:1
DA:15,0
DA:16,0
DA:17,0
DA:18,0
DA:25,1
DA:26,1
DA:27,0
DA:31,1
LH:3
LF:8
end_of_record
```
