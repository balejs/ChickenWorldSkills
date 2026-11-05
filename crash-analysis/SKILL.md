---
name: crash-analysis
description: Analyse ESP32 and native crashes - backtrace symbolication, heap corruption, watchdog resets
---

# Skill: Crash Analysis

**Purpose**: Turn a crash into a located, symbolicated, evidenced root cause

**Use when**: The device reboots, aborts, shows Guru Meditation, a native test segfaults,
or a watchdog fires

**Last Updated**: 2026-11-05

Merges `esp32-crash-analysis`, `native-crash-analysis`, `callstack-decoding` and
`esp32-heap-debugging` - they were one workflow split by platform.

---

## CRITICAL RULES

1. **NEVER** run `pio test` directly on a crash-prone test - the device reboots forever and
   you lose the log. Use `test_esp32_crash_repeat.py`
2. **ALWAYS** capture the full crash log **before** analysing, and decode while it is fresh
3. **ALWAYS** symbolicate against the **matching** `firmware.elf` - a rebuilt ELF gives
   plausible, wrong line numbers
4. **NEVER** assume a crash location - get the actual backtrace first, then hypothesise
5. **NEVER** ignore heap corruption warnings; they are usually downstream of the real bug
6. **ALWAYS** quote the log lines and decoded frames that support your conclusion

---

## Platform routing

| Symptom | Route |
|---|---|
| ESP32 Guru Meditation / abort / reboot | ESP32 path below |
| `CORRUPT HEAP:`, `assert failed: multi_heap_malloc` | Heap path below |
| WDT reset | `parse_watchdog_crash_log.py`, then ESP32 path |
| Segfault on macOS/Linux native test | Native path below |

---

## ESP32 path

```bash
# 1. Reproduce with capture - builds AND uploads, then loops
~/devel/ChickenWorld/ChickenTools/bin/test_esp32_crash_repeat.py \
    -p ~/devel/ChickenWorld/<Project> -n 20

# 2. Symbolicate. The tool reads a raw log, a backtrace string, or bare addresses.
~/devel/ChickenWorld/ChickenTools/bin/decode_callstack.py \
    .pio/build/esp32dev/firmware.elf --file crash_log_<ts>.txt

~/devel/ChickenWorld/ChickenTools/bin/decode_callstack.py \
    firmware.elf --backtrace "0x400d5e2c:0x3ffb8d70 0x400d67bc:0x3ffb8d90"

# 3. Verify the fix - 20 iterations, 0 crashes
```

Output:
```
0x400d5e2c: myFunction at /path/to/file.cpp:123
0x400d67bc: callerFunction at /path/to/file.cpp:456
```

`test_esp32_crash_repeat.py` detects Guru Meditation, `CORRUPT HEAP:`, `ChickenPtr`
assertions and stack overflow, and distinguishes a `task_wdt` warning from a real crash.

## Heap corruption path

PlatformIO does not expose the ESP-IDF heap debugging knobs, or exposes them poorly, so use
the vendored ESP-IDF directly. It lives under `~/.platformio/packages/framework-espidf`.

```bash
export IDF_PATH=~/.platformio/packages/framework-espidf
python3 $IDF_PATH/tools/idf.py -C <project> fullclean
python3 $IDF_PATH/tools/idf.py -C <project> build
```

Set the real Kconfig symbols - `CONFIG(heap_poisoning)` is **not** one of them:

```
CONFIG_HEAP_POISONING_COMPREHENSIVE=y   # full canaries, slowest, best for hunting
CONFIG_HEAP_POISONING_LIGHT=y           # cheaper, for CI
CONFIG_HEAP_POISONING_DISABLED=y        # current committed default in sdkconfig.esp32dev
```

Then parse the watchdog log:

```bash
~/devel/ChickenWorld/ChickenTools/bin/parse_watchdog_crash_log.py crash.log
```

Common causes: buffer overflow/underflow, use-after-free, double free, stack overflow,
race on shared memory.

## Native path

```bash
lldb -o run -o "thread backtrace all" -o quit ./program     # macOS
gdb -ex run -ex "thread apply all bt" -batch ./program       # Linux
```

Document the actual frames in the investigation notes before forming a hypothesis.

---

**Key references**:
- [Debugging/ESP32_Testing_Procedures.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Testing_Procedures.md) - ESP32 testing
- [Debugging/FORENSIC_TECHNIQUES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md) - Log forensics
- [Debugging/ESP32_Heap_Poisoning_Guide.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Heap_Poisoning_Guide.md) - Heap poisoning
- [Debugging/ChickenHttpLib_Heap_Poisoning_Investigation.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ChickenHttpLib_Heap_Poisoning_Investigation.md) - Case study
- [ChickenTools/README.md](/Users/marco/devel/ChickenWorld/ChickenTools/README.md) - Tool reference
- [ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenFundamentalsLib/INVESTIGATION_CHICKENPTR_LIFECYCLE_VALIDATION_2026-02-28.md) - Lifecycle crash example

**Skills this relies on**:
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Testing procedures
- [timeout-hang-analysis](../timeout-hang-analysis/SKILL.md) - When it stalls without crashing
- [investigation-workflow](../investigation-workflow/SKILL.md) - Systematic investigation
