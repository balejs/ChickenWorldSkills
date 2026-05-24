---
name: tls-debugging
description: Debug TLS/HTTPS issues in ChickenWorld networking
---

# Skill: TLS Debugging

**Purpose**: Debug TLS/HTTPS connection and certificate issues

**Use when**: TLS handshakes fail, certificate verification errors, or HTTPS connections don't work

**CRITICAL RULES**:
1. **ALWAYS** provide SNI (Server Name Indication) when using IP addresses
2. **ALWAYS** verify certificate chain is complete
3. **ALWAYS** check mbedTLS error codes for specific failure reasons
4. **ALWAYS** use verbose logging for TLS debugging

**Workflow**:
```cpp
// Enable verbose TLS logging
#define CHICKEN_TLS_SOCKET_LOG_LEVEL 4

// Use explicit SNI with IP addresses
auto exchange = MakeHttpExchange(scheduler, "192.168.1.100", 443,
                                 ROOT_CA, weakPtr(this),
                                 "mydevice.local");  // SNI = domain
```

```bash
# Run test with TLS debugging
pio test -e native -vvv 2>&1 | tee tls_debug.log
```

**Key references**:
- [Debugging/tls_debugging_procedure.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/tls_debugging_procedure.md) - Complete TLS debugging guide
- [Common/TLS_SNI_REQUIREMENT_2025-11-25.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md) - SNI requirements
- [Common/TLS_CERTIFICATE_GENERATION.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TLS_CERTIFICATE_GENERATION.md) - Certificate generation
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - TLS implementation notes

**Common error codes**:
- `-9984` - Certificate verification failed (usually missing SNI)
- `-9985` - Certificate not yet valid
- `-9986` - Certificate has expired

**Skills this relies on**:
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Testing procedures
- [chickenworld-coding](../chickenworld-coding/SKILL.md) - Coding patterns
