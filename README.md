A Gemini generated quickly thrown together "simple" rom authenticity checker

Here are some dat [files](https://files.catbox.moe/uktcfh.zip).

![](demo.gif)

Here is a Gemini list of features!

## Features

- **High-Performance DAT Parsing**: Utilizes memory-efficient streaming to clear XML DOM nodes on the fly. This allows the script to ingest massive, multi-gigabyte DAT databases (e.g., MAME, Redump, No-Intro) without ballooning system RAM.
- **Console Header Awareness (Pre-Computed Stripping)**: Automatically detects and bypasses system-specific copier/emulator headers (such as 16-byte iNES headers for `.nes` or 512-byte SMC headers for `.smc`). Hashes are computed strictly against the pure game data payload for 100% accurate database matching.
- **Deep-Audit Multi-Hash Matching**:
  - **Fast Mode (Sequential)**: Uses highly-optimized `SHA-1` indexing as a high-speed anchor lookup.
  - **Slow Mode (Deep Audit)**: Provides robust cross-verification using strict `SHA-256` matching with automatic graceful fallbacks to `SHA-1` and `MD5` if needed.
- **Container / Zip Parsing Lifecycle**: Extracts, maps, and validates individual compressed game ROMs inside `.zip` archives without requiring full manual disk extraction.
- **Ghost Dump Detection**: Pre-emptively scans data chunks during hashing to isolate broken, fake, or corrupted files whose data payloads consist strictly of empty `0x00` null bytes.
- **Output & Report Isolation Filters**: Includes granular tracking flags (`--only-good` and `--only-bad`) to tailor your console outputs and generated summary logs:
  - `--only-good`: Displays and logs exclusively verified healthy dumps.
  - `--only-bad`: Transforms the script into an error monitor, hiding passing files to expose only unknown, corrupted, or ghost dumps.
- **Dynamic Asynchronous Progress Tracking**: Built-in thread-safe job completion architecture accurately updates real-time execution statistics (`[Current / Total]`) across multi-threaded operations—even when hidden files are omitted by active output filters.
- **Hardware-Accelerated Concurrency**: Leverages a multi-threaded parallel workspace to audit thousands of files simultaneously across available CPU architectures.
- **Safe Automated Purge Engine**: Features target queues (`--delete-null` and `--purge`) paired with a clear-text terminal confirmation safe-guard (`"Yes, do as I say!"`) to permanently scrub unmapped or corrupted binaries from filesystem arrays safely.

PS. If you don't like IA you don't have to use it or read the slop above but the reason I conjured this up is because I for one was bored and number two I wanted someting that I could just throw some dat files and some roms at and be done with it. If I had to be honest I am not proud of it either. But I wanted something that works and works relatively well and just did what I wanted it to do. And that's what this is!
