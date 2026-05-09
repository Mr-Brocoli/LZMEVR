LZMEVR - Extremely fast compression (That is just LZ4 with a hat on it) 
================================

LZMEVR is LZ4 but I made many changes to make it fast,
for fun and for research.
I removed a lot of features to focus on certain things
I wanted to right now, like speed.
It's intended to be safe enough, but I don't know exactly
what I'm doing entirely.
Thankyou Yann Collet for giving LZ4 as a base and all
who have contributed to it.

Benchmarks
-------------------------

The benchmark uses [lzbench], from @inikep
compiled with GCC v8.2.0 on Linux 64-bits (Ubuntu 4.18.0-17).
The reference system uses a Core i7-9700K CPU @ 4.9GHz (w/ turbo boost).
Benchmark evaluates the compression of reference [Silesia Corpus]
in single-thread mode.

[lzbench]: https://github.com/inikep/lzbench
[Silesia Corpus]: http://sun.aei.polsl.pl/~sdeor/index.php?page=silesia

|  Compressor             | Factor  | Compression | Decompression |
|  ----------             | -----   | ----------- | ------------- |
|  memcpy                 |  1.000  | 13700 MB/s  |  13700 MB/s   |
|**LZ4 default (v1.9.0)** |**2.101**| **780 MB/s**| **4970 MB/s** |
|  LZO 2.09               |  2.108  |   670 MB/s  |    860 MB/s   |
|  QuickLZ 1.5.0          |  2.238  |   575 MB/s  |    780 MB/s   |
|  Snappy 1.1.4           |  2.091  |   565 MB/s  |   1950 MB/s   |
| [Zstandard] 1.4.0 -1    |  2.883  |   515 MB/s  |   1380 MB/s   |
|  LZF v3.6               |  2.073  |   415 MB/s  |    910 MB/s   |
| [zlib] deflate 1.2.11 -1|  2.730  |   100 MB/s  |    415 MB/s   |
|**LZ4 HC -9 (v1.9.0)**   |**2.721**|    41 MB/s  | **4900 MB/s** |
| [zlib] deflate 1.2.11 -6|  3.099  |    36 MB/s  |    445 MB/s   |

[zlib]: http://www.zlib.net/
[Zstandard]: http://www.zstd.net/


Installation
-------------------------

```
make
make install     # this command may require root permissions
```

LZ4's `Makefile` supports standard [Makefile conventions],
including [staged installs], [redirection], or [command redefinition].
It is compatible with parallel builds (`-j#`).

[Makefile conventions]: https://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html
[staged installs]: https://www.gnu.org/prep/standards/html_node/DESTDIR.html
[redirection]: https://www.gnu.org/prep/standards/html_node/Directory-Variables.html
[command redefinition]: https://www.gnu.org/prep/standards/html_node/Utilities-in-Makefiles.html

### Building LZ4 - Using vcpkg

You can download and install LZ4 using the [vcpkg](https://github.com/Microsoft/vcpkg) dependency manager:

    git clone https://github.com/Microsoft/vcpkg.git
    cd vcpkg
    ./bootstrap-vcpkg.sh
    ./vcpkg integrate install
    ./vcpkg.exe install lz4

The LZ4 port in vcpkg is kept up to date by Microsoft team members and community contributors. If the version is out of date, please [create an issue or pull request](https://github.com/Microsoft/vcpkg) on the vcpkg repository.

Documentation
-------------------------

The raw LZ4 block compression format is detailed within [lz4_Block_format].

Arbitrarily long files or data streams are compressed using multiple blocks,
for streaming requirements. These blocks are organized into a frame,
defined into [lz4_Frame_format].
Interoperable versions of LZ4 must also respect the frame format.

[lz4_Block_format]: doc/lz4_Block_format.md
[lz4_Frame_format]: doc/lz4_Frame_format.md


Other source versions
-------------------------

Beyond the C reference source,
many contributors have created versions of lz4 in multiple languages
(Java, C#, Python, Perl, Ruby, etc.).
A list of known source ports is maintained on the [LZ4 Homepage].

[LZ4 Homepage]: http://www.lz4.org

### Packaging status

Most distributions are bundled with a package manager
which allows easy installation of both the `liblz4` library
and the `lz4` command line interface.

[![Packaging status](https://repology.org/badge/vertical-allrepos/lz4.svg?columns=4&exclude_unsupported=1)](https://repology.org/project/lz4/versions)


### Special Thanks

- Takayuki Matsuoka, aka @t-mat, for exceptional first-class support throughout the lifetime of this project
