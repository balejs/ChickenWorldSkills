# Skill: Networking Debugging

**Purpose**: Debug networking and connection issues in ChickenWorld projects

**Use when**: HTTP requests fail, URI parsing issues, or connection errors occur

**CRITICAL RULES**:
1. **ALWAYS** verify URI has proper path component (add '/' if missing)
2. **ALWAYS** use setStateListener() for HttpExchange to detect errors
3. **ALWAYS** check for proper SNI when using TLS with IP addresses
4. **ALWAYS** enable verbose logging for network debugging

**Workflow**:
```cpp
// Enable verbose logging
#define CHICKEN_HTTP_EXCHANGE_LOG_LEVEL 4
#define CHICKEN_SOCKET_LOG_LEVEL 4

// Add state listener for error detection
_httpExchange->setStateListener(sharedPtr(this));
```

```bash
# Debug networking issues
pio test -e native -vvv 2>&1 | tee network_debug.log
```

**Key references**:
- [Debugging/uri_path_handling.md](../../ChickenDocs/Debugging/uri_path_handling.md) - URI path handling
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](../../ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Networking architecture
- [Common/TLS_SNI_REQUIREMENT_2025-11-25.md](../../ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md) - TLS SNI requirement
- [Debugging/tls_debugging_procedure.md](../../ChickenDocs/Debugging/tls_debugging_procedure.md) - TLS debugging

**Common issues**:
- **400 Bad Request**: Missing '/' in URI path
- **Connection refused**: Test server not running
- **TLS handshake failed**: Missing SNI or certificate issues

**Skills this relies on**:
- [chickenworld-coding](chickenworld-coding.md) - Coding standards
- [chickenworld-testing](chickenworld-testing.md) - Testing procedures
