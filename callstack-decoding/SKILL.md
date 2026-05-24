---
name: callstack-decoding
description: Decode ESP32 crash backtraces using decode_callstack.py
---

# Skill: Callstack Decoding

**Purpose**: Decode ESP32 crash backtraces using decode_callstack.py

**Use when**: ESP32 crashes with backtrace addresses that need symbol resolution

**CRITICAL RULES**:
1. **ALWAYS** capture full crash log before decoding
2. **ALWAYS** use correct firmware.elf binary
3. **ALWAYS** document decoded crash location
4. Decode immediately while crash details are fresh

**Workflow**:
```bash
# 1. Run test and capture crash log
pio test -e esp32dev -vvv 2>&1 | tee crash.log

# 2. Decode backtrace
./ChickenWorld/ChickenTools/bin/decode_callstack.py \
    .pio/build/esp32dev/firmware.elf --file crash.log

# 3. Or decode specific addresses
./ChickenWorld/ChickenTools/bin/decode_callstack.py \
    firmware.elf 0x400d5e2c 0x400d67bc
```

**Key references**:
- [ChickenTools/QUICK_REFERENCE.md](../../ChickenTools/QUICK_REFERENCE.md) - Quick reference
- [ChickenTools/README.md](../../ChickenTools/README.md) - Full documentation
- [ChickenDocs/Common/CHICKENTOOLS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/CHICKENTOOLS.md) - ChickenTools docs
- [ChickenTools/bin/decode_callstack.py](../../ChickenTools/bin/decode_callstack.py) - Tool source

**Output format**:
```
Backtrace: 0x400d5e2c:0x3ffb8d70 0x400d67bc:0x3ffb8d90

0x400d5e2c: myFunction at /path/to/file.cpp:123
0x400d67bc: callerFunction at /path/to/file.cpp:456
```

**Skills this relies on**:
- [esp32-crash-analysis](../esp32-crash-analysis/SKILL.md) - Crash analysis workflow
