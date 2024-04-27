<!-- AUTOMATICALLY GENERATED, DO NOT EDIT -->
<!-- edit README.md.template instead -->

# Rust serialization benchmark

The goal of these benchmarks is to provide thorough and complete benchmarks for various rust
serialization frameworks.

## These benchmarks are a work in progress

These benchmarks are still being developed and pull requests to improve benchmarks are welcome.

## [Interactive site](https://djkoloski.github.io/rust_serialization_benchmark/)

Calculate the number of messages per second that can be sent/received with various rust serialization frameworks and compression libraries.
[Documentation](pages/README.md)

## Format

All tests benchmark the following properties (time or size):

* **Serialize**: serialize data into a buffer
* **Deserialize**: deserializes a buffer into a normal rust object
* **Size**: the size of the buffer when serialized
* **Zlib**: the size of the buffer after zlib compression
* **Zstd**: the size of the buffer after zstd compression
* **Zstd Time**: the time taken to compress the serialized buffer with zstd

Zero-copy deserialization libraries have an additional set of benchmarks:

* **Access**: accesses a buffer as structured data
* **Read**: runs through a buffer and reads fields out of it
* **Update**: updates a buffer as structured data

Some benchmark results may be italicized and followed by an asterisk. Mouse over these for more details on what situation was benchmarked. Other footnotes are located at the bottom.

## Last updated: 2024-4-27 19:21:46

<details><summary>Runtime info</summary>

### `rustc` version

```
rustc 1.77.0-nightly (11f32b73e 2024-01-31)
binary: rustc
commit-hash: 11f32b73e0dc9287e305b5b9980d24aecdc8c17f
commit-date: 2024-01-31
host: x86_64-unknown-linux-gnu
release: 1.77.0-nightly
LLVM version: 17.0.6
```

### CPU info

```
Architecture:                       x86_64
CPU op-mode(s):                     32-bit, 64-bit
Address sizes:                      39 bits physical, 48 bits virtual
Byte Order:                         Little Endian
CPU(s):                             24
On-line CPU(s) list:                0-23
Vendor ID:                          GenuineIntel
Model name:                         12th Gen Intel(R) Core(TM) i9-12900KF
CPU family:                         6
Model:                              151
Thread(s) per core:                 2
Core(s) per socket:                 16
Socket(s):                          1
Stepping:                           2
CPU(s) scaling MHz:                 32%
CPU max MHz:                        5200.0000
CPU min MHz:                        800.0000
BogoMIPS:                           6374.40
Flags:                              fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflushopt clwb intel_pt sha_ni xsaveopt xsavec xgetbv1 xsaves split_lock_detect avx_vnni dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp hwp_pkg_req hfi vnmi umip pku ospke waitpkg gfni vaes vpclmulqdq rdpid movdiri movdir64b fsrm md_clear serialize arch_lbr ibt flush_l1d arch_capabilities
Virtualization:                     VT-x
L1d cache:                          640 KiB (16 instances)
L1i cache:                          768 KiB (16 instances)
L2 cache:                           14 MiB (10 instances)
L3 cache:                           30 MiB (1 instance)
NUMA node(s):                       1
NUMA node0 CPU(s):                  0-23
Vulnerability Gather data sampling: Not affected
Vulnerability Itlb multihit:        Not affected
Vulnerability L1tf:                 Not affected
Vulnerability Mds:                  Not affected
Vulnerability Meltdown:             Not affected
Vulnerability Mmio stale data:      Not affected
Vulnerability Retbleed:             Not affected
Vulnerability Spec rstack overflow: Not affected
Vulnerability Spec store bypass:    Mitigation; Speculative Store Bypass disabled via prctl
Vulnerability Spectre v1:           Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:           Mitigation; Enhanced / Automatic IBRS, IBPB conditional, RSB filling, PBRSB-eIBRS SW sequence
Vulnerability Srbds:                Not affected
Vulnerability Tsx async abort:      Not affected
```

</details>

## `log`

This data set is composed of HTTP request logs that are small and contain many strings.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 112.50 µs | <span title="unvalidated">*1.0276 ms\**</span> | 1705800 | 520088 | 413256 | 3.6462 ms |
| [alkahest 0.1.5][alkahest] | 97.571 µs | † | 1045784 | 454157 | 389424 | 3.6065 ms |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*396.06 µs\**</span> <span title="prepend">*428.09 µs\**</span> | 1.8746 ms | 874632 | 355446 | 311723 | 2.8575 ms |
| [bincode 2.0.0-rc][bincode] | 112.44 µs | 1.5302 ms | 741295 | 303944 | 257153 | 2.2437 ms |
| [bincode 1.3.3][bincode1] | 238.87 µs | 1.2867 ms | 1045784 | 373127 | 311761 | 2.7137 ms |
| [bitcode 0.6.0][bitcode] | 100.54 µs | 1.0566 ms | 703710 | 288826 | 229755 | 1.4485 ms |
| [borsh 1.3.1][borsh] | 245.53 µs | 1.4029 ms | 885780 | 362204 | 286514 | 2.5611 ms |
| [bson 2.9.0][bson] | 1.0355 ms | 4.1949 ms | 1924682 | 532821 | 376270 | 3.1038 ms |
| [capnp 0.18.13][capnp] | 253.91 µs | † | 1443216 | 513986 | 428649 | 3.6957 ms |
| [cbor4ii 0.3.2][cbor4ii] | 306.43 µs | 3.0090 ms | 1407835 | 403440 | 324081 | 2.6946 ms |
| [ciborium 0.2.2][ciborium] | 1.8082 ms | 4.6325 ms | 1407835 | 403440 | 324081 | 2.6323 ms |
| [databuf 0.5.0][databuf] | 135.17 µs | 1.3324 ms | 765778 | 311715 | 264630 | 2.2480 ms |
| [dlhn 0.1.6][dlhn] | 384.20 µs | 1.5235 ms | 724953 | 301446 | 253629 | 2.1052 ms |
| [flatbuffers 23.5.26][flatbuffers] | 771.70 µs | † | 1276368 | 468539 | 388832 | 3.0419 ms |
| [msgpacker 0.4.3][msgpacker] | 582.94 µs | 1.5692 ms | 764996 | 315291 | 264898 | 2.3898 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.7099 ms | 2.4310 ms | 818669 | 332556 | 285514 | 2.6027 ms |
| [nanoserde 0.1.37][nanoserde] | 140.05 µs | 1.2919 ms | 1045784 | 373127 | 311761 | 2.7489 ms |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 308.49 µs | 1.3740 ms | 765778 | 311743 | 264518 | 2.3101 ms |
| [postcard 1.0.8][postcard] | 208.16 µs | 1.3807 ms | 724953 | 302399 | 253747 | 2.1377 ms |
| [pot 3.0.0][pot] | 1.2528 ms | 3.5033 ms | 971922 | 372513 | 304122 | 2.7658 ms |
| [prost 0.12.4][prost] | <span title="encode">*452.75 µs\**</span> <span title="populate + encode">*1.5462 ms\**</span> | 2.0002 ms | 884628 | 363130 | 315494 | 2.8578 ms |
| [rkyv 0.7.44][rkyv] | 125.43 µs | <span title="unvalidated">*1.0316 ms\**</span> <span title="validated upfront with error">*1.4066 ms\**</span> | 1011488 | 383862 | 333545 | 2.9522 ms |
| [rmp-serde 1.1.2][rmp-serde] | 670.99 µs | 1.8896 ms | 784997 | 325384 | 278219 | 2.4077 ms |
| [ron 0.8.1][ron] | 7.8007 ms | 8.1592 ms | 1607459 | 449158 | 349713 | 3.3915 ms |
| [savefile 0.16.5][savefile] | 97.885 µs | 1.3299 ms | 1045800 | 373139 | 311755 | 2.7147 ms |
| [serde_bare 0.5.0][serde_bare] | 313.13 µs | 1.3674 ms | 765778 | 311715 | 264630 | 2.3005 ms |
| [serde_cbor 0.11.2][serde_cbor] | 893.98 µs | 2.7621 ms | 1407835 | 403440 | 324081 | 2.6681 ms |
| [serde_json 1.0.115][serde_json] | 1.7614 ms | 3.2754 ms | 1827461 | 470560 | 361090 | 3.2653 ms |
| [simd-json 0.13.9][simd-json] | 1.1812 ms | 2.9031 ms | 1827461 | 470560 | 361090 | 3.4643 ms |
| [speedy 0.8.7][speedy] | 105.05 µs | 1.1906 ms | 885780 | 362204 | 286514 | 2.5461 ms |
| [wiring 0.2.1][wiring] | 97.625 µs | 1.2988 ms | 1045784 | 337930 | 276188 | 2.4286 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*23.576 µs\**</span> | <span title="unvalidated">*32.295 µs\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*14.673 µs\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*41.459 ns\**</span> | <span title="validated on-demand with error">*89.867 µs\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*1.0050 ms\**</span> | <span title="unvalidated">*29.095 µs\**</span> <span title="validated upfront with error">*1.0496 ms\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*377.65 µs\**</span> | <span title="unvalidated">*6.0866 µs\**</span> <span title="validated upfront with error">*384.11 µs\**</span> | 8.9250 µs |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 86.73% | <span title="unvalidated">*100.00%\**</span> | 41.25% | 55.53% | 55.60% | 39.73% |
| [alkahest 0.1.5][alkahest] | 100.00% | † | 67.29% | 63.60% | 59.00% | 40.16% |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*24.64%\**</span> <span title="prepend">*22.79%\**</span> | 54.82% | 80.46% | 81.26% | 73.70% | 50.69% |
| [bincode 2.0.0-rc][bincode] | 86.78% | 67.15% | 94.93% | 95.03% | 89.35% | 64.56% |
| [bincode 1.3.3][bincode1] | 40.85% | 79.86% | 67.29% | 77.41% | 73.70% | 53.38% |
| [bitcode 0.6.0][bitcode] | 97.05% | 97.26% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.3.1][borsh] | 39.74% | 73.25% | 79.45% | 79.74% | 80.19% | 56.56% |
| [bson 2.9.0][bson] | 9.42% | 24.50% | 36.56% | 54.21% | 61.06% | 46.67% |
| [capnp 0.18.13][capnp] | 38.43% | † | 48.76% | 56.19% | 53.60% | 39.19% |
| [cbor4ii 0.3.2][cbor4ii] | 31.84% | 34.15% | 49.99% | 71.59% | 70.89% | 53.76% |
| [ciborium 0.2.2][ciborium] | 5.40% | 22.18% | 49.99% | 71.59% | 70.89% | 55.03% |
| [databuf 0.5.0][databuf] | 72.18% | 77.12% | 91.89% | 92.66% | 86.82% | 64.44% |
| [dlhn 0.1.6][dlhn] | 25.40% | 67.45% | 97.07% | 95.81% | 90.59% | 68.81% |
| [flatbuffers 23.5.26][flatbuffers] | 12.64% | † | 55.13% | 61.64% | 59.09% | 47.62% |
| [msgpacker 0.4.3][msgpacker] | 16.74% | 65.49% | 91.99% | 91.61% | 86.73% | 60.61% |
| [nachricht-serde 0.4.0][nachricht-serde] | 3.60% | 42.27% | 85.96% | 86.85% | 80.47% | 55.65% |
| [nanoserde 0.1.37][nanoserde] | 69.67% | 79.54% | 67.29% | 77.41% | 73.70% | 52.69% |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 31.63% | 74.79% | 91.89% | 92.65% | 86.86% | 62.70% |
| [postcard 1.0.8][postcard] | 46.87% | 74.43% | 97.07% | 95.51% | 90.54% | 67.76% |
| [pot 3.0.0][pot] | 7.79% | 29.33% | 72.40% | 77.53% | 75.55% | 52.37% |
| [prost 0.12.4][prost] | <span title="encode">*21.55%\**</span> <span title="populate + encode">*6.31%\**</span> | 51.37% | 79.55% | 79.54% | 72.82% | 50.69% |
| [rkyv 0.7.44][rkyv] | 77.79% | <span title="unvalidated">*99.61%\**</span> <span title="validated upfront with error">*73.06%\**</span> | 69.57% | 75.24% | 68.88% | 49.07% |
| [rmp-serde 1.1.2][rmp-serde] | 14.54% | 54.38% | 89.64% | 88.76% | 82.58% | 60.16% |
| [ron 0.8.1][ron] | 1.25% | 12.59% | 43.78% | 64.30% | 65.70% | 42.71% |
| [savefile 0.16.5][savefile] | 99.68% | 77.27% | 67.29% | 77.40% | 73.70% | 53.36% |
| [serde_bare 0.5.0][serde_bare] | 31.16% | 75.15% | 91.89% | 92.66% | 86.82% | 62.96% |
| [serde_cbor 0.11.2][serde_cbor] | 10.91% | 37.20% | 49.99% | 71.59% | 70.89% | 54.29% |
| [serde_json 1.0.115][serde_json] | 5.54% | 31.37% | 38.51% | 61.38% | 63.63% | 44.36% |
| [simd-json 0.13.9][simd-json] | 8.26% | 35.40% | 38.51% | 61.38% | 63.63% | 41.81% |
| [speedy 0.8.7][speedy] | 92.88% | 86.31% | 79.45% | 79.74% | 80.19% | 56.89% |
| [wiring 0.2.1][wiring] | 99.94% | 79.12% | 67.29% | 85.47% | 83.19% | 59.64% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*0.18%\**</span> | <span title="unvalidated">*18.85%\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*41.48%\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*100.00%\**</span> | <span title="validated on-demand with error">*6.77%\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*20.92%\**</span> <span title="validated upfront with error">*0.58%\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*0.01%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*1.58%\**</span> | 100.00% |

## `mesh`

This data set is a single mesh. The mesh contains an array of triangles, each of which has three vertices and a normal vector.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 180.14 µs | <span title="unvalidated">*183.74 µs\**</span> | 6000024 | 5378513 | 5345890 | 4.5977 ms |
| [alkahest 0.1.5][alkahest] | 185.30 µs | † | 6000008 | 5378500 | 5345890 | 4.7723 ms |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*3.2085 ms\**</span> <span title="prepend">*3.5660 ms\**</span> | 4.6782 ms | 8625005 | 6443961 | 6231572 | 40.312 ms |
| [bincode 2.0.0-rc][bincode] | 249.55 µs | 551.91 µs | 6000005 | 5378497 | 5345897 | 4.5856 ms |
| [bincode 1.3.3][bincode1] | 1.8291 ms | 2.5973 ms | 6000008 | 5378500 | 5345890 | 4.5626 ms |
| [bitcode 0.6.0][bitcode] | 678.43 µs | 244.66 µs | 6000006 | 5182295 | 4923880 | 7.6787 ms |
| [borsh 1.3.1][borsh] | 2.4585 ms | 2.6751 ms | 6000004 | 5378496 | 5345889 | 4.8863 ms |
| [bson 2.9.0][bson] | 18.279 ms | 43.732 ms | 23013911 | 9212089 | 7497811 | 66.618 ms |
| [capnp 0.18.13][capnp] | 3.3168 ms | † | 14000088 | 7130367 | 6051062 | 44.187 ms |
| [cbor4ii 0.3.2][cbor4ii] | 5.0703 ms | 29.979 ms | 13125016 | 7524114 | 6757967 | 48.692 ms |
| [ciborium 0.2.2][ciborium] | 29.843 ms | 40.695 ms | 13122324 | 7524660 | 6759658 | 48.065 ms |
| [databuf 0.5.0][databuf] | 761.27 µs | 3.0253 ms | 6000003 | 5378495 | 5345900 | 4.8388 ms |
| [dlhn 0.1.6][dlhn] | 2.6881 ms | 3.6497 ms | 6000003 | 5378495 | 5345900 | 4.9403 ms |
| [flatbuffers 23.5.26][flatbuffers] | 521.15 µs | † | 6000024 | 5378434 | 5345910 | 4.7165 ms |
| [msgpacker 0.4.3][msgpacker] | 10.131 ms | 4.6453 ms | 7500005 | 6058442 | 6014337 | 6.0632 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 57.561 ms | 14.100 ms | 8125037 | 6493484 | 6386940 | 39.382 ms |
| [nanoserde 0.1.37][nanoserde] | 991.83 µs | 467.31 µs | 6000008 | 5378500 | 5345890 | 4.6306 ms |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 1.8115 ms | 2.4875 ms | 6000004 | 5378496 | 5345889 | 4.7315 ms |
| [postcard 1.0.8][postcard] | 270.53 µs | 1.1763 ms | 6000003 | 5378495 | 5345900 | 4.9137 ms |
| [pot 3.0.0][pot] | 19.922 ms | 34.814 ms | 10122342 | 6814618 | 6852251 | 44.931 ms |
| [prost 0.12.4][prost] | <span title="encode">*4.0965 ms\**</span> <span title="populate + encode">*5.0368 ms\**</span> | 7.2608 ms | 8750000 | 6665735 | 6421871 | 39.923 ms |
| [rkyv 0.7.44][rkyv] | 256.62 µs | <span title="unvalidated">*180.78 µs\**</span> <span title="validated upfront with error">*182.74 µs\**</span> | 6000008 | 5378500 | 5345892 | 4.8488 ms |
| [rmp-serde 1.1.2][rmp-serde] | 5.5933 ms | 6.2950 ms | 8125006 | 6494876 | 6391037 | 38.863 ms |
| [ron 0.8.1][ron] | 95.071 ms | 139.14 ms | 22192885 | 8970395 | 8138755 | 84.415 ms |
| [savefile 0.16.5][savefile] | 178.20 µs | 179.87 µs | 6000024 | 5378518 | 5345893 | 4.7140 ms |
| [serde_bare 0.5.0][serde_bare] | 2.6800 ms | 2.5729 ms | 6000003 | 5378495 | 5345900 | 4.6669 ms |
| [serde_cbor 0.11.2][serde_cbor] | 16.139 ms | 23.024 ms | 13122324 | 7524660 | 6759658 | 48.088 ms |
| [serde_json 1.0.115][serde_json] | 43.977 ms | 45.645 ms | 26192883 | 9566084 | 8586741 | 88.434 ms |
| [simd-json 0.13.9][simd-json] | 30.338 ms | 60.748 ms | 26192883 | 9566084 | 8586741 | 88.773 ms |
| [speedy 0.8.7][speedy] | 178.05 µs | 179.99 µs | 6000004 | 5378496 | 5345889 | 4.7135 ms |
| [wiring 0.2.1][wiring] | 180.26 µs | 200.67 µs | 6000008 | 5378952 | 5345894 | 4.6282 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | ‡ | <span title="unvalidated">*83.549 µs\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*36.623 µs\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*70.904 ns\**</span> | <span title="validated on-demand with error">*1.2430 ms\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*24.301 ns\**</span> | <span title="unvalidated">*24.676 µs\**</span> <span title="validated upfront with error">*39.309 µs\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*4.7111 ns\**</span> | <span title="unvalidated">*24.614 µs\**</span> <span title="validated upfront with error">*24.469 µs\**</span> | 119.29 µs |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 98.84% | <span title="unvalidated">*97.89%\**</span> | 100.00% | 96.35% | 92.11% | 99.24% |
| [alkahest 0.1.5][alkahest] | 96.09% | † | 100.00% | 96.35% | 92.11% | 95.61% |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*5.55%\**</span> <span title="prepend">*4.99%\**</span> | 3.84% | 69.57% | 80.42% | 79.02% | 11.32% |
| [bincode 2.0.0-rc][bincode] | 71.35% | 32.59% | 100.00% | 96.35% | 92.11% | 99.50% |
| [bincode 1.3.3][bincode1] | 9.73% | 6.93% | 100.00% | 96.35% | 92.11% | 100.00% |
| [bitcode 0.6.0][bitcode] | 26.24% | 73.52% | 100.00% | 100.00% | 100.00% | 59.42% |
| [borsh 1.3.1][borsh] | 7.24% | 6.72% | 100.00% | 96.35% | 92.11% | 93.38% |
| [bson 2.9.0][bson] | 0.97% | 0.41% | 26.07% | 56.26% | 65.67% | 6.85% |
| [capnp 0.18.13][capnp] | 5.37% | † | 42.86% | 72.68% | 81.37% | 10.33% |
| [cbor4ii 0.3.2][cbor4ii] | 3.51% | 0.60% | 45.71% | 68.88% | 72.86% | 9.37% |
| [ciborium 0.2.2][ciborium] | 0.60% | 0.44% | 45.72% | 68.87% | 72.84% | 9.49% |
| [databuf 0.5.0][databuf] | 23.39% | 5.95% | 100.00% | 96.35% | 92.11% | 94.29% |
| [dlhn 0.1.6][dlhn] | 6.62% | 4.93% | 100.00% | 96.35% | 92.11% | 92.35% |
| [flatbuffers 23.5.26][flatbuffers] | 34.16% | † | 100.00% | 96.35% | 92.11% | 96.74% |
| [msgpacker 0.4.3][msgpacker] | 1.76% | 3.87% | 80.00% | 85.54% | 81.87% | 75.25% |
| [nachricht-serde 0.4.0][nachricht-serde] | 0.31% | 1.28% | 73.85% | 79.81% | 77.09% | 11.59% |
| [nanoserde 0.1.37][nanoserde] | 17.95% | 38.49% | 100.00% | 96.35% | 92.11% | 98.53% |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 9.83% | 7.23% | 100.00% | 96.35% | 92.11% | 96.43% |
| [postcard 1.0.8][postcard] | 65.82% | 15.29% | 100.00% | 96.35% | 92.11% | 92.85% |
| [pot 3.0.0][pot] | 0.89% | 0.52% | 59.27% | 76.05% | 71.86% | 10.15% |
| [prost 0.12.4][prost] | <span title="encode">*4.35%\**</span> <span title="populate + encode">*3.53%\**</span> | 2.48% | 68.57% | 77.75% | 76.67% | 11.43% |
| [rkyv 0.7.44][rkyv] | 69.38% | <span title="unvalidated">*99.50%\**</span> <span title="validated upfront with error">*98.43%\**</span> | 100.00% | 96.35% | 92.11% | 94.10% |
| [rmp-serde 1.1.2][rmp-serde] | 3.18% | 2.86% | 73.85% | 79.79% | 77.04% | 11.74% |
| [ron 0.8.1][ron] | 0.19% | 0.13% | 27.04% | 57.77% | 60.50% | 5.40% |
| [savefile 0.16.5][savefile] | 99.92% | 100.00% | 100.00% | 96.35% | 92.11% | 96.79% |
| [serde_bare 0.5.0][serde_bare] | 6.64% | 6.99% | 100.00% | 96.35% | 92.11% | 97.77% |
| [serde_cbor 0.11.2][serde_cbor] | 1.10% | 0.78% | 45.72% | 68.87% | 72.84% | 9.49% |
| [serde_json 1.0.115][serde_json] | 0.40% | 0.39% | 22.91% | 54.17% | 57.34% | 5.16% |
| [simd-json 0.13.9][simd-json] | 0.59% | 0.30% | 22.91% | 54.17% | 57.34% | 5.14% |
| [speedy 0.8.7][speedy] | 100.00% | 99.93% | 100.00% | 96.35% | 92.11% | 96.80% |
| [wiring 0.2.1][wiring] | 98.77% | 89.63% | 100.00% | 96.34% | 92.11% | 98.58% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | ‡ | <span title="unvalidated">*29.29%\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*66.81%\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*6.64%\**</span> | <span title="validated on-demand with error">*1.97%\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*19.39%\**</span> | <span title="unvalidated">*99.16%\**</span> <span title="validated upfront with error">*62.25%\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*100.00%\**</span> | <span title="unvalidated">*99.41%\**</span> <span title="validated upfront with error">*100.00%\**</span> | 100.00% |

## `minecraft_savedata`

This data set is composed of Minecraft player saves that contain highly structured data.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 104.36 µs | <span title="unvalidated">*815.34 µs\**</span> | 1290592 | 394688 | 338107 | 2.8314 ms |
| [alkahest 0.1.5][alkahest] | 113.82 µs | † | 667570 | 325484 | 320452 | 2.4811 ms |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*552.14 µs\**</span> <span title="prepend">*616.76 µs\**</span> | 1.8619 ms | 489348 | 281173 | 249546 | 1.8442 ms |
| [bincode 2.0.0-rc][bincode] | 146.71 µs | 1.1802 ms | 367413 | 221291 | 206273 | 1.5555 ms |
| [bincode 1.3.3][bincode1] | 277.45 µs | 1.0989 ms | 569975 | 240525 | 232423 | 1.8526 ms |
| [bitcode 0.6.0][bitcode] | 68.720 µs | 806.32 µs | 327688 | 200947 | 182736 | 442.85 µs |
| [borsh 1.3.1][borsh] | 252.57 µs | 1.0673 ms | 446595 | 234236 | 210008 | 1.5375 ms |
| [bson 2.9.0][bson] | 1.4000 ms | 4.4897 ms | 1619653 | 502185 | 328399 | 2.7922 ms |
| [capnp 0.18.13][capnp] | 254.08 µs | † | 803896 | 335606 | 280851 | 2.2743 ms |
| [cbor4ii 0.3.2][cbor4ii] | 496.15 µs | 2.8539 ms | 1109831 | 344745 | 274514 | 2.2943 ms |
| [ciborium 0.2.2][ciborium] | 1.7846 ms | 4.4052 ms | 1109821 | 344751 | 274526 | 2.2909 ms |
| [databuf 0.5.0][databuf] | 176.58 µs | 1.0162 ms | 356311 | 213062 | 198488 | 1.5233 ms |
| [dlhn 0.1.6][dlhn] | 401.00 µs | 1.4790 ms | 366496 | 220600 | 205683 | 1.5647 ms |
| [flatbuffers 23.5.26][flatbuffers] | 2.0303 ms | † | 844168 | 345696 | 294015 | 2.3016 ms |
| [msgpacker 0.4.3][msgpacker] | 518.01 µs | 1.7115 ms | 391251 | 236877 | 220476 | 1.6599 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.5712 ms | 2.2477 ms | 449745 | 252432 | 231110 | 1.7135 ms |
| [nanoserde 0.1.37][nanoserde] | 131.70 µs | 1.1188 ms | 567975 | 239930 | 232419 | 1.7642 ms |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 311.11 µs | 1.1934 ms | 356311 | 212976 | 198524 | 1.4554 ms |
| [postcard 1.0.8][postcard] | 211.79 µs | 1.1469 ms | 367489 | 221913 | 207344 | 1.5445 ms |
| [pot 3.0.0][pot] | 1.1568 ms | 3.1997 ms | 599125 | 299158 | 247693 | 1.9136 ms |
| [prost 0.12.4][prost] | <span title="encode">*642.39 µs\**</span> <span title="populate + encode">*1.7122 ms\**</span> | 2.0307 ms | 596811 | 305319 | 269310 | 2.0860 ms |
| [rkyv 0.7.44][rkyv] | 172.06 µs | <span title="unvalidated">*780.49 µs\**</span> <span title="validated upfront with error">*1.1327 ms\**</span> | 596952 | 253967 | 220706 | 1.5982 ms |
| [rmp-serde 1.1.2][rmp-serde] | 683.86 µs | 1.7120 ms | 424533 | 245214 | 226188 | 1.7142 ms |
| [ron 0.8.1][ron] | 4.4537 ms | 8.8231 ms | 1465223 | 434935 | 343338 | 3.5604 ms |
| [savefile 0.16.5][savefile] | 109.50 µs | 1.0516 ms | 566991 | 239361 | 232010 | 1.8059 ms |
| [serde_bare 0.5.0][serde_bare] | 354.11 µs | 1.3330 ms | 356311 | 213062 | 198488 | 1.4571 ms |
| [serde_cbor 0.11.2][serde_cbor] | 917.92 µs | 2.8429 ms | 1109821 | 344751 | 274526 | 2.2417 ms |
| [serde_json 1.0.115][serde_json] | 1.8193 ms | 4.1760 ms | 1623191 | 466527 | 359623 | 3.6307 ms |
| [simd-json 0.13.9][simd-json] | 1.2768 ms | 2.6471 ms | 1623191 | 466527 | 359623 | 3.5592 ms |
| [speedy 0.8.7][speedy] | 148.31 µs | 958.18 µs | 449595 | 234970 | 210361 | 1.6011 ms |
| [wiring 0.2.1][wiring] | 104.31 µs | 1.1095 ms | 566975 | 247810 | 225259 | 1.7754 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*21.347 µs\**</span> | <span title="unvalidated">*22.039 µs\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*2.2174 µs\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*41.425 ns\**</span> | <span title="validated on-demand with error">*294.34 ns\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*1.1888 ms\**</span> | <span title="unvalidated">*823.59 ns\**</span> <span title="validated upfront with error">*1.1903 ms\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*331.13 µs\**</span> | <span title="unvalidated">*105.82 ns\**</span> <span title="validated upfront with error">*332.20 µs\**</span> | 916.23 ns |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 65.85% | <span title="unvalidated">*95.73%\**</span> | 25.39% | 50.91% | 54.05% | 15.64% |
| [alkahest 0.1.5][alkahest] | 60.38% | † | 49.09% | 61.74% | 57.02% | 17.85% |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*12.45%\**</span> <span title="prepend">*11.14%\**</span> | 41.92% | 66.96% | 71.47% | 73.23% | 24.01% |
| [bincode 2.0.0-rc][bincode] | 46.84% | 66.13% | 89.19% | 90.81% | 88.59% | 28.47% |
| [bincode 1.3.3][bincode1] | 24.77% | 71.02% | 57.49% | 83.55% | 78.62% | 23.90% |
| [bitcode 0.6.0][bitcode] | 100.00% | 96.80% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.3.1][borsh] | 27.21% | 73.13% | 73.37% | 85.79% | 87.01% | 28.80% |
| [bson 2.9.0][bson] | 4.91% | 17.38% | 20.23% | 40.01% | 55.64% | 15.86% |
| [capnp 0.18.13][capnp] | 27.05% | † | 40.76% | 59.88% | 65.07% | 19.47% |
| [cbor4ii 0.3.2][cbor4ii] | 13.85% | 27.35% | 29.53% | 58.29% | 66.57% | 19.30% |
| [ciborium 0.2.2][ciborium] | 3.85% | 17.72% | 29.53% | 58.29% | 66.56% | 19.33% |
| [databuf 0.5.0][databuf] | 38.92% | 76.80% | 91.97% | 94.31% | 92.06% | 29.07% |
| [dlhn 0.1.6][dlhn] | 17.14% | 52.77% | 89.41% | 91.09% | 88.84% | 28.30% |
| [flatbuffers 23.5.26][flatbuffers] | 3.38% | † | 38.82% | 58.13% | 62.15% | 19.24% |
| [msgpacker 0.4.3][msgpacker] | 13.27% | 45.60% | 83.75% | 84.83% | 82.88% | 26.68% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.67% | 34.72% | 72.86% | 79.60% | 79.07% | 25.84% |
| [nanoserde 0.1.37][nanoserde] | 52.18% | 69.76% | 57.69% | 83.75% | 78.62% | 25.10% |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 22.09% | 65.40% | 91.97% | 94.35% | 92.05% | 30.43% |
| [postcard 1.0.8][postcard] | 32.45% | 68.05% | 89.17% | 90.55% | 88.13% | 28.67% |
| [pot 3.0.0][pot] | 5.94% | 24.39% | 54.69% | 67.17% | 73.78% | 23.14% |
| [prost 0.12.4][prost] | <span title="encode">*10.70%\**</span> <span title="populate + encode">*4.01%\**</span> | 38.43% | 54.91% | 65.82% | 67.85% | 21.23% |
| [rkyv 0.7.44][rkyv] | 39.94% | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*68.91%\**</span> | 54.89% | 79.12% | 82.80% | 27.71% |
| [rmp-serde 1.1.2][rmp-serde] | 10.05% | 45.59% | 77.19% | 81.95% | 80.79% | 25.83% |
| [ron 0.8.1][ron] | 1.54% | 8.85% | 22.36% | 46.20% | 53.22% | 12.44% |
| [savefile 0.16.5][savefile] | 62.76% | 74.22% | 57.79% | 83.95% | 78.76% | 24.52% |
| [serde_bare 0.5.0][serde_bare] | 19.41% | 58.55% | 91.97% | 94.31% | 92.06% | 30.39% |
| [serde_cbor 0.11.2][serde_cbor] | 7.49% | 27.45% | 29.53% | 58.29% | 66.56% | 19.75% |
| [serde_json 1.0.115][serde_json] | 3.78% | 18.69% | 20.19% | 43.07% | 50.81% | 12.20% |
| [simd-json 0.13.9][simd-json] | 5.38% | 29.48% | 20.19% | 43.07% | 50.81% | 12.44% |
| [speedy 0.8.7][speedy] | 46.34% | 81.46% | 72.89% | 85.52% | 86.87% | 27.66% |
| [wiring 0.2.1][wiring] | 65.88% | 70.35% | 57.80% | 81.09% | 81.12% | 24.94% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*0.19%\**</span> | <span title="unvalidated">*0.48%\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*4.77%\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*100.00%\**</span> | <span title="validated on-demand with error">*35.95%\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*12.85%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*0.01%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.03%\**</span> | 100.00% |

## `mk48`

This data set is composed of mk48.io game updates that contain data with many exploitable patterns and invariants.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 281.85 µs | <span title="unvalidated">*1.3779 ms\**</span> | 2984682 | 1406979 | 1270254 | 8.2999 ms |
| [alkahest 0.1.5][alkahest] | 372.29 µs | † | 1863391 | 1234113 | 1202345 | 6.3993 ms |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*2.7189 ms\**</span> <span title="prepend">*1.6380 ms\**</span> | 5.0103 ms | 1664428 | 1264167 | 1216472 | 6.2515 ms |
| [bincode 2.0.0-rc][bincode] | 482.73 µs | 1.9988 ms | 1372381 | 1091486 | 1037296 | 5.1983 ms |
| [bincode 1.3.3][bincode1] | 1.6731 ms | 2.4369 ms | 1811011 | 1115281 | 1025627 | 5.7072 ms |
| [bitcode 0.6.0][bitcode] | 451.60 µs | 1.4109 ms | 948499 | 857321 | 837658 | 1.8901 ms |
| [borsh 1.3.1][borsh] | 1.2961 ms | 1.6781 ms | 1486162 | 1082357 | 1013550 | 5.4465 ms |
| [bson 2.9.0][bson] | 9.9614 ms | 22.880 ms | 10030880 | 2833079 | 1600859 | 16.380 ms |
| [capnp 0.18.13][capnp] | 1.1108 ms | † | 2664040 | 1511895 | 1212087 | 8.1528 ms |
| [cbor4ii 0.3.2][cbor4ii] | 1.8395 ms | 10.602 ms | 5878791 | 1655835 | 1431390 | 12.369 ms |
| [ciborium 0.2.2][ciborium] | 10.527 ms | 18.728 ms | 5878653 | 1655791 | 1431560 | 12.379 ms |
| [databuf 0.5.0][databuf] | 711.69 µs | 2.0368 ms | 1288257 | 1037579 | 984337 | 4.9284 ms |
| [dlhn 0.1.6][dlhn] | 2.6619 ms | 3.5463 ms | 1279599 | 1052061 | 1021161 | 5.1873 ms |
| [flatbuffers 23.5.26][flatbuffers] | 2.4481 ms | † | 2273740 | 1408408 | 1235566 | 7.2171 ms |
| [msgpacker 0.4.3][msgpacker] | 1.1389 ms | 2.6859 ms | 1424043 | 1128758 | 1110156 | 5.7541 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 15.000 ms | 8.3607 ms | 1728519 | 1247642 | 1233323 | 6.6637 ms |
| [nanoserde 0.1.37][nanoserde] | 520.04 µs | 1.7400 ms | 1770477 | 1108304 | 1029947 | 5.6408 ms |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 1.3747 ms | 1.6729 ms | 1288257 | 1039269 | 986510 | 4.9234 ms |
| [postcard 1.0.8][postcard] | 984.03 µs | 2.2236 ms | 1279599 | 1058243 | 1016738 | 4.8436 ms |
| [pot 3.0.0][pot] | 7.1147 ms | 15.797 ms | 2544810 | 1447453 | 1268390 | 8.5194 ms |
| [prost 0.12.4][prost] | <span title="encode">*3.6710 ms\**</span> <span title="populate + encode">*6.1430 ms\**</span> | 4.9730 ms | 1818378 | 1307777 | 1266311 | 6.8110 ms |
| [rkyv 0.7.44][rkyv] | 776.20 µs | <span title="unvalidated">*1.2571 ms\**</span> <span title="validated upfront with error">*1.6647 ms\**</span> | 2029080 | 1335117 | 1158855 | 6.8364 ms |
| [rmp-serde 1.1.2][rmp-serde] | 4.3934 ms | 6.1470 ms | 1703813 | 1231892 | 1200208 | 6.4638 ms |
| [ron 0.8.1][ron] | 19.773 ms | 47.890 ms | 8476284 | 2181196 | 1783971 | 21.188 ms |
| [savefile 0.16.5][savefile] | 401.04 µs | 1.5135 ms | 1750226 | 1101682 | 1027827 | 5.7249 ms |
| [serde_bare 0.5.0][serde_bare] | 2.1038 ms | 2.5977 ms | 1288257 | 1037597 | 984356 | 4.9186 ms |
| [serde_cbor 0.11.2][serde_cbor] | 4.7999 ms | 11.717 ms | 5878653 | 1655791 | 1431560 | 12.430 ms |
| [serde_json 1.0.115][serde_json] | 10.154 ms | 17.945 ms | 9175594 | 2334253 | 1800713 | 21.406 ms |
| [simd-json 0.13.9][simd-json] | 5.8753 ms | 21.329 ms | 9175594 | 2334253 | 1800713 | 21.160 ms |
| [speedy 0.8.7][speedy] | 395.36 µs | 1.4369 ms | 1546963 | 1093532 | 1013443 | 5.5872 ms |
| [wiring 0.2.1][wiring] | 356.81 µs | 1.6087 ms | 1750210 | 1129857 | 1058906 | 6.0904 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*80.180 µs\**</span> | <span title="unvalidated">*80.525 µs\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*320.82 ns\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*41.423 ns\**</span> | <span title="validated on-demand with error">*435.09 ns\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*2.3195 ms\**</span> | <span title="unvalidated">*1.5765 µs\**</span> <span title="validated upfront with error">*2.3188 ms\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*381.42 µs\**</span> | <span title="unvalidated">*189.15 ns\**</span> <span title="validated upfront with error">*380.20 µs\**</span> | 325.17 ns |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | 100.00% | <span title="unvalidated">*91.23%\**</span> | 31.78% | 60.93% | 65.94% | 22.77% |
| [alkahest 0.1.5][alkahest] | 75.71% | † | 50.90% | 69.47% | 69.67% | 29.54% |
| [bilrost 0.1006.0][bilrost] | <span title="encode">*10.37%\**</span> <span title="prepend">*17.21%\**</span> | 25.09% | 56.99% | 67.82% | 68.86% | 30.23% |
| [bincode 2.0.0-rc][bincode] | 58.39% | 62.89% | 69.11% | 78.55% | 80.75% | 36.36% |
| [bincode 1.3.3][bincode1] | 16.85% | 51.59% | 52.37% | 76.87% | 81.67% | 33.12% |
| [bitcode 0.6.0][bitcode] | 62.41% | 89.10% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.3.1][borsh] | 21.75% | 74.91% | 63.82% | 79.21% | 82.65% | 34.70% |
| [bson 2.9.0][bson] | 2.83% | 5.49% | 9.46% | 30.26% | 52.33% | 11.54% |
| [capnp 0.18.13][capnp] | 25.37% | † | 35.60% | 56.71% | 69.11% | 23.18% |
| [cbor4ii 0.3.2][cbor4ii] | 15.32% | 11.86% | 16.13% | 51.78% | 58.52% | 15.28% |
| [ciborium 0.2.2][ciborium] | 2.68% | 6.71% | 16.13% | 51.78% | 58.51% | 15.27% |
| [databuf 0.5.0][databuf] | 39.60% | 61.72% | 73.63% | 82.63% | 85.10% | 38.35% |
| [dlhn 0.1.6][dlhn] | 10.59% | 35.45% | 74.12% | 81.49% | 82.03% | 36.44% |
| [flatbuffers 23.5.26][flatbuffers] | 11.51% | † | 41.72% | 60.87% | 67.80% | 26.19% |
| [msgpacker 0.4.3][msgpacker] | 24.75% | 46.80% | 66.61% | 75.95% | 75.45% | 32.85% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.88% | 15.04% | 54.87% | 68.72% | 67.92% | 28.36% |
| [nanoserde 0.1.37][nanoserde] | 54.20% | 72.25% | 53.57% | 77.35% | 81.33% | 33.51% |
| [parity-scale-codec 3.6.9][parity-scale-codec] | 20.50% | 75.14% | 73.63% | 82.49% | 84.91% | 38.39% |
| [postcard 1.0.8][postcard] | 28.64% | 56.53% | 74.12% | 81.01% | 82.39% | 39.02% |
| [pot 3.0.0][pot] | 3.96% | 7.96% | 37.27% | 59.23% | 66.04% | 22.19% |
| [prost 0.12.4][prost] | <span title="encode">*7.68%\**</span> <span title="populate + encode">*4.59%\**</span> | 25.28% | 52.16% | 65.56% | 66.15% | 27.75% |
| [rkyv 0.7.44][rkyv] | 36.31% | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*75.52%\**</span> | 46.75% | 64.21% | 72.28% | 27.65% |
| [rmp-serde 1.1.2][rmp-serde] | 6.42% | 20.45% | 55.67% | 69.59% | 69.79% | 29.24% |
| [ron 0.8.1][ron] | 1.43% | 2.62% | 11.19% | 39.31% | 46.95% | 8.92% |
| [savefile 0.16.5][savefile] | 70.28% | 83.06% | 54.19% | 77.82% | 81.50% | 33.02% |
| [serde_bare 0.5.0][serde_bare] | 13.40% | 48.39% | 73.63% | 82.63% | 85.10% | 38.43% |
| [serde_cbor 0.11.2][serde_cbor] | 5.87% | 10.73% | 16.13% | 51.78% | 58.51% | 15.21% |
| [serde_json 1.0.115][serde_json] | 2.78% | 7.01% | 10.34% | 36.73% | 46.52% | 8.83% |
| [simd-json 0.13.9][simd-json] | 4.80% | 5.89% | 10.34% | 36.73% | 46.52% | 8.93% |
| [speedy 0.8.7][speedy] | 71.29% | 87.49% | 61.31% | 78.40% | 82.65% | 33.83% |
| [wiring 0.2.1][wiring] | 78.99% | 78.14% | 54.19% | 75.88% | 79.11% | 31.03% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [abomonation 0.7.3][abomonation] | <span title="unvalidated">*0.05%\**</span> | <span title="unvalidated">*0.23%\**</span> | ‡ |
| [alkahest 0.1.5][alkahest] | ‡ | <span title="validated on-demand with panic">*58.96%\**</span> | ‡ |
| [capnp 0.18.13][capnp] | <span title="validated on-demand with error">*100.00%\**</span> | <span title="validated on-demand with error">*43.47%\**</span> | ‡ |
| [flatbuffers 23.5.26][flatbuffers] | <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*12.00%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [rkyv 0.7.44][rkyv] | <span title="validated upfront with error">*0.01%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.05%\**</span> | 100.00% |

[abomonation]: https://crates.io/crates/abomonation/0.7.3
[alkahest]: https://crates.io/crates/alkahest/0.1.5
[bilrost]: https://crates.io/crates/bilrost/0.1006.0
[bincode]: https://crates.io/crates/bincode/2.0.0-rc
[bincode1]: https://crates.io/crates/bincode/1.3.3
[bitcode]: https://crates.io/crates/bitcode/0.6.0
[borsh]: https://crates.io/crates/borsh/1.3.1
[bson]: https://crates.io/crates/bson/2.9.0
[capnp]: https://crates.io/crates/capnp/0.18.13
[cbor4ii]: https://crates.io/crates/cbor4ii/0.3.2
[ciborium]: https://crates.io/crates/ciborium/0.2.2
[databuf]: https://crates.io/crates/databuf/0.5.0
[dlhn]: https://crates.io/crates/dlhn/0.1.6
[flatbuffers]: https://crates.io/crates/flatbuffers/23.5.26
[msgpacker]: https://crates.io/crates/msgpacker/0.4.3
[nachricht-serde]: https://crates.io/crates/nachricht-serde/0.4.0
[nanoserde]: https://crates.io/crates/nanoserde/0.1.37
[parity-scale-codec]: https://crates.io/crates/parity-scale-codec/3.6.9
[postcard]: https://crates.io/crates/postcard/1.0.8
[pot]: https://crates.io/crates/pot/3.0.0
[prost]: https://crates.io/crates/prost/0.12.4
[rkyv]: https://crates.io/crates/rkyv/0.7.44
[rmp-serde]: https://crates.io/crates/rmp-serde/1.1.2
[ron]: https://crates.io/crates/ron/0.8.1
[savefile]: https://crates.io/crates/savefile/0.16.5
[serde_bare]: https://crates.io/crates/serde_bare/0.5.0
[serde_cbor]: https://crates.io/crates/serde_cbor/0.11.2
[serde_json]: https://crates.io/crates/serde_json/1.0.115
[simd-json]: https://crates.io/crates/simd-json/0.13.9
[speedy]: https://crates.io/crates/speedy/0.8.7
[wiring]: https://crates.io/crates/wiring/0.2.1


## Footnotes:

\* *mouse over for situational details*

† *do not provide deserialization capabilities, but the user can write their own*

‡ *do not support buffer mutation (`capnp` and `flatbuffers` may but not for rust)*
