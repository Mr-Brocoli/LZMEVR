LZMEVR - It's Got What Files Crave 
================================

LZMEVR library is provided as open-source software using BSD 2-Clause license.

Introduction
--------------------------------

Have you ever thought about
a world where everything
is exactly the same...

Except LZ4 has repcodes?
And short range matches?
And long range matches?

Well, it's fine now. Why?
Because LZMEVR is here!

LZMEVR is the work of I, Maximillian Elderitch Von Radom, but better known as Mr. Brocoli. 
But really, the name is only for the sake of a different name, LZMEVR is a bunch of things 
taped together from LZ4 / LZAV / ZSTD / Lizard.  

Benchmarks (to prove this project is not pointless)
-------------------------

The benchmark uses [lzbench], from @inikep
compiled with GCC v13.3.0 on Linux 64-bits.
The reference system uses a **Core i7-6700K CPU @ 4.0GHz (w/ turbo boost)**.
Benchmark evaluates the compression of reference [Silesia Corpus]
in single-thread mode.

[lzbench]: https://github.com/inikep/lzbench
[Silesia Corpus]: http://sun.aei.polsl.pl/~sdeor/index.php?page=silesia

|  Compressor                   | Factor  | Compression | Decompression |
|  ----------                   | -----   | ----------- | ------------- |
|  memcpy                       |  1.000  | 10134 MB/s  |  10136 MB/s   |
|**LZMEVR -0**                  |**2.125**| **830 MB/s**| **3780 MB/s** |
|**LZMEVR -1**                  |**2.482**| **575 MB/s**| **3030 MB/s** |
|**LZMEVR -2**                  |**2.640**| **377 MB/s**| **2805 MB/s** |
|**LZMEVR -3**                  |**2.735**| **292 MB/s**| **2466 MB/s** |
|**LZMEVR -4**                  |**2.783**| **260 MB/s**| **2362 MB/s** |
|  [LZ4] 1.10.0                 |  2.101  |   636 MB/s  |   4080 MB/s   |
|  [LZAV] 5.8                   |  2.503  |   430 MB/s  |   2300 MB/s   |
| [Zstandard] 1.5.7 --fast=1    |  2.438  |   495 MB/s  |   1747 MB/s   |
| [Zstandard] 1.5.7 -1          |  2.896  |   446 MB/s  |   1330 MB/s   |

[LZ4]: https://github.com/lz4/lz4
[Zstandard]: http://www.zstd.net/
[LZAV]: https://github.com/avaneev/lzav



Installation (32 BIT CURRENTLY NOT SUPPORTED)
-------------------------

```
make
make install     # this command may require root permissions
```

LZMEVR's `Makefile` supports standard [Makefile conventions],
including [staged installs], [redirection], or [command redefinition].
It is compatible with parallel builds (`-j#`).

[Makefile conventions]: https://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html
[staged installs]: https://www.gnu.org/prep/standards/html_node/DESTDIR.html
[redirection]: https://www.gnu.org/prep/standards/html_node/Directory-Variables.html
[command redefinition]: https://www.gnu.org/prep/standards/html_node/Utilities-in-Makefiles.html

Documentation
-------------------------

The raw LZMEVR block compression format is detailed within [lz4_Block_format].
(IF THERE IS NOTHING IN THE DOCUMENTATION IT IS BECAUSE PROTOTYPE STILL).

Arbitrarily long files or data streams are compressed using multiple blocks,
for streaming requirements. These blocks are organized into a frame,
defined into [lz4_Frame_format].
Interoperable versions of LZMEVR must also respect the frame format.

[lz4_Block_format]: doc/lz4_Block_format.md
[lz4_Frame_format]: doc/lz4_Frame_format.md



### Special Thanks
- Aleksey Vaneev, for LZAV to study.
- Yann Collet, for LZ4 and zstd base to study.
- Takayuki Matsuoka, aka @t-mat, for exceptional first-class support of LZ4 during the lifetime of it.
