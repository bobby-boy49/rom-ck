A Gemini generated quickly thrown together "simple" rom authenticity checker

Here are some dat [files](https://files.catbox.moe/a0nmpf.zip).

![](demo.gif)

## Features

### 🔍 Core Architecture & Platform Support
* **Multi-System Compatibility:** Pre-configured with a master validation list supporting a wide range of extensions across Nintendo, Sega, Atari, SNK, Bandai, NEC, and arcade platforms.
* **Dual-Format DAT Intake:** Accepts raw `.dat` XML files, recursively scans directories containing multiple DAT targets, or loads a pre-existing SQLite database cache directly.
* **Intelligent Header Logic:** Automatically identifies and strips system-specific headers (e.g., NES, SNES, Sega, Atari) to calculate accurate headerless hashes.

### ⚡ Performance & Caching Optimizations
* **Dynamic Cache Validation:** Tracks DAT file changes using a unique `SHA-256` state hash to skip rebuilding the database cache if nothing has modified.
* **High-Throughput SQLite Engine:** Rebuilds fresh database caches using highly optimized write-time parameters (`PRAGMA synchronous = OFF`, `journal_mode = MEMORY`) and large dedicated RAM workspaces.
* **Multi-Threaded Parallel Execution:** Employs an asynchronous `ThreadPoolExecutor` to process files concurrently utilizing maximum hardware capacity.
* **Safe Storage Handlers:** Features thread-local database connections to prevent connection churning mid-run, alongside an explicit fallback to sequential processing to protect fragile storage media like SD cards.
* **Single-Pass Stream Hashing:** Minimizes I/O overhead by opening loose files and compressed zip entries exactly once, reading data in optimized 1MB chunks to feed multiple hash engines simultaneously.

### 🛡️ Audit Capabilities & Integrity Analysis
* **Dual Audit Processing Modes:**
  * **Fast Mode (Default):** Runs a quick, optimized evaluation utilizing a `SHA-1` index anchor.
  * **Slow Mode:** Executes a deep cryptographic audit anchoring to `SHA-256` with automated fallbacks to `SHA-1` and `MD5`.
* **Deep Zip Archive Inspection:** Drills down into `.zip` containers on the fly to authenticate individual sub-files against standard entries, shared BIOS files, or driver variations without requiring extraction to disk.
* **Ghost Dump Identification:** Automatically flags corrupt, broken, or fake "ghost" dumps whose contents consist entirely of empty null zeroes.

### 🎛️ Automation, Filtering & Safety Actions
* **Tailored System Reporting:** Automatically outputs a comprehensive `rom_verification_report.txt` breaking down good, bad, and unmapped variants with explicit audit summaries.
* **Console Filtering Switches:** Tweak terminal noise by instructing the engine to print and log only verified dumps (`--only-good`) or bad/unknown entries (`--only-bad`).
* **Destructive Clean-up Protections:** Includes strict switches to wipe empty dummy files (`--delete-null`) or completely clear out invalid dumps (`--purge`).
* **Interactive Guardrail:** Destructive disk processes require an explicit, un-bypassable terminal confirmation: `"Yes, do as I say!"`.

---

## Command Line Flags

| Flag | Description |
| :--- | :--- |
| `path_to_dat_folder_or_db` | **(Required)** Path to your system `.dat` file, folder of DATs, or pre-built `.db` cache. |
| `path_to_roms_dir` | **(Required)** Path to the directory or single file containing the ROMs you want to verify. |
| `--slow` | Deep Audit Mode. Force checks all hashes (`SHA-256`, `SHA-1`, `MD5`) instead of just `SHA-1`. |
| `--thread [n]` | Multi-threaded mode. Set a manual thread worker pool or use `0` to maximize available system CPU power. |
| `--only-good` | Filters console logging and reporting outputs to exclusively show verified good dumps. |
| `--only-bad` | Filters console logging and reporting outputs to exclusively show broken/unmapped dumps. |
| `--delete-null` | Targets and queues entirely zeroed-out "ghost" dumps for local filesystem deletion. |
| `--purge` | Queues all unmapped, bad, or corrupt files for total filesystem deletion. |
| `--build-cache` | Standalone flag. Builds the SQLite database cache from your DAT files and exits immediately without running an audit. |

PS. If you don't like AI you don't have to use it. Or read the slop above. But the reason I conjured this up is because I, for one was bored and number two, I wanted someting that I could just throw some dat files and some roms at and be done with it. If I had to be honest I am not proud of it either. But I wanted something that works and works relatively well and just did what I wanted it to do. And that's what this is!
