---
name: chickenworld-testing
description: Follow testing procedures for ChickenWorld projects
---

# Skill: ChickenWorld Testing

**Purpose**: Follow ChickenWorld testing procedures and best practices

**Use when**: Testing any ChickenWorld library or application

**CRITICAL RULES**:
1. **ALWAYS** use testing tools (build_and_test_all.py, test_esp32_crash_repeat.py)
2. **ALWAYS** enable verbose logging (-vvv) for ESP32 tests
3. **ALWAYS** use crash detection scripts for ESP32 tests that may crash/reboot
4. **NEVER** run pio test directly for crash-prone tests
5. **ALWAYS** save test output to timestamped log file: `timeout 120 pio test -e {env} -vvv 2>&1 | tee /Users/marco/devel/ChickenWorld/{Project}/investigation/logs/{test_name}_{YYYYMMDD_HHMMSS}.log`
6. **NEVER** re-run tests just to grep output - ALWAYS parse existing log files in investigation/logs/
7. **NEVER** assume heap objects at same logical location will have same address across test runs - EACH heap allocation can occur at different addresses
8. **NEVER** debug object lifetime issues by assuming addresses match - use actual address values from logs, never "it should be the same"

**Workflow**:
1. Read [ChickenTools/QUICK_REFERENCE.md](../../ChickenTools/QUICK_REFERENCE.md)
2. Check [ChickenDocs/Common/TESTING_QUICK_REFERENCE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TESTING_QUICK_REFERENCE.md)
3. Review [Debugging/ESP32_Testing_Procedures.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/ESP32_Testing_Procedures.md)
4. Run tests with appropriate flags

**Key references**:
- [ChickenTools/README.md](../../ChickenTools/README.md) - ChickenTools overview
- [ChickenDocs/Common/CHICKENTOOLS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/CHICKENTOOLS.md) - build_and_test_all.py usage
- [ChickenDocs/Common/TESTING_REMINDERS.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TESTING_REMINDERS.md) - Testing reminders
- [BUILD_PROCEDURES/README.md](/Users/marco/devel/ChickenWorld/ChickenDocs/BUILD_PROCEDURES/README.md) - Build procedures
- [ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md) - Circular references with LoopedSocketListener

**HttpServer Lifecycle Rule**: When testing HttpServer in ESP32 or native environments, **ALWAYS store HttpServer as a member variable**, not a local variable:
```cpp
// WRONG: Local variable - destroyed immediately
auto server = MakeHttpServer(port, loopScheduler, cert, key);
_updater = MakeSoftwareUpdate(server);

// CORRECT: Member variable - kept alive for tester lifetime
_httpServer = MakeHttpServer(port, loopScheduler, cert, key);
_updater = MakeSoftwareUpdate(_httpServer);

// Member variable declaration
SHttpServer _httpServer;
```
**Why**: TCPServerSocketLWIP uses raw pointers; if HttpServer is destroyed, incoming connections receive NULL arg and fail with "NULL connection" error.
**Heap allocation principle**: Each HttpServer instance will be allocated at different heap addresses across test runs - you can NEVER assume test_software_update_creation's server address matches test_software_update_interface's address.

**Error pattern to detect**: `SocketLWIP.cpp:771: Received accept for pcb <address> from NULL connection, closing pcb`
- What it means: Incoming connection callback received pointer to TcpServerSocketLWIP object that no longer exists
- Root cause: Object was destroyed (local variable went out of scope), but LWIP still had raw pointer reference
- How to verify: Compare timestamps of Started/Destroyed log messages with NULL connection timestamp. If `Destroyed` timestamp < NULL connection timestamp AND the addresses don't match, the NEW object's incoming connection is hitting the OLD object's DESTROYED memory (NULL).

**Skills this relies on**:
- [build-and-test-all](../build-and-test-all/SKILL.md) - Automated test runner
- [esp32-crash-analysis](../esp32-crash-analysis/SKILL.md) - ESP32 crash analysis
