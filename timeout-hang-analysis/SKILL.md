---
name: timeout-hang-analysis
description: Distinguish a legitimate timeout from a hang by testing whether the system was still making progress when the timer fired
---

# Skill: Timeout and Hang Analysis

**Purpose**: Decide whether a timeout cut off work that was still progressing, or exposed a genuine hang

**Use when**: A test times out, a transfer stalls, or a run shows no progress while still "running"

**Last Updated**: 2026-11-02

---

## CRITICAL RULES

1. **NEVER** raise a timeout to make a test pass before classifying it — a raised timeout hides hangs permanently
2. **ALWAYS** decide hang-vs-timeout from two log facts: the last activity timestamp, and whether a progress counter was advancing
3. **NEVER** infer the classification from the elapsed duration alone — a 543s run can be either case
4. **ALWAYS** quote the log lines that carry the timestamps and counter values when reporting the verdict

---

## The Deciding Test

| Evidence | Legitimate timeout | Hang |
|----------|--------------------|------|
| Last activity timestamp | Seconds before the timeout | Frozen for minutes |
| Progress counter | Advancing | Stuck, or looping on one value |
| Completion markers | Seen once, then finalization | Repeated, never finalized |
| Iteration count | Matches expected chunk count | Far exceeds it, never ends |

**Timestamps stuck = HANG. Timestamps advancing = TIMEOUT.**

A legitimate timeout means the operation needed more time than configured. A hang means
it would never have finished, and raising the timeout only lengthens the wait.

---

## Workflow

```bash
LOG=investigation/logs/<test>_<YYYYMMDD_HHMMSS>.log

# 1. Is the clock moving?
grep -oE "\[0[0-9]:[0-9]{2}:[0-9]{2}" "$LOG" | tail -5

# 2. Is the counter moving?
grep -E "Wrote .* to OTA partition|total:" "$LOG" | tail -5

# 3. Did completion fire once, or repeatedly?
grep -c "HttpMessageCompleted" "$LOG"

# 4. Does the chunk count match firmware_size / chunk_size?
grep -c "Wrote .* to OTA partition" "$LOG"
```

Then compare the last timestamp against the timeout point. If the gap is seconds and the
counter was climbing, the timeout is legitimate — size it from the measured rate.

---

## The Margin Model

A timeout that fires mid-operation is usually a **margin** problem, not a logic bug: a
single blocking call inside the window eats the slack. Measure the blocking call, then
compare against the configured timeout.

Measured instance: `esp_ota_begin()` synchronously erases the OTA partition and took
6.0–7.3 s in every run against a fixed 10 s `HttpServer` timeout — ~3.5 s of slack for
the whole transfer, which is what produced the 40–50% flakiness. Fix by resetting the
timeout around the blocking call, not by raising the global value.

- [investigation/TLS_DESYNC_INVESTIGATION_STATUS.md](/Users/marco/devel/ChickenWorld/ChickenSoftwareUpdateLib/investigation/TLS_DESYNC_INVESTIGATION_STATUS.md) — Root Cause Chain (measured)

---

## Action Items

1. **STOP** — do not increase the timeout
2. **CLASSIFY** — run the deciding test above
3. **IF HANG** — find the looping condition; look for missing finalization or a missing size check
4. **IF TIMEOUT** — compute the required budget from measured rates, and reset the timer around known blocking calls
5. **VERIFY** — re-run enough iterations to show the margin holds, not just one green run

---

**Key references**:
- [Debugging/FORENSIC_TECHNIQUES.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/FORENSIC_TECHNIQUES.md) - Log forensics techniques
- [Debugging/tls_debugging_procedure.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/tls_debugging_procedure.md) - TLS debugging procedure
- [Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md) - A hang whose cause is a leaked listener

**Skills this relies on**:
- [networking-debugging](../networking-debugging/SKILL.md) - Networking issues
- [tls-debugging](../tls-debugging/SKILL.md) - TLS/HTTPS issues
- [investigation-workflow](../investigation-workflow/SKILL.md) - Evidence-based investigation
