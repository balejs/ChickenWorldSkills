---
name: network-debugging
description: Debug ChickenWorld networking and TLS issues - URI paths, state listeners, SNI, certificate failures
---

# Skill: Network Debugging

**Purpose**: Diagnose HTTP/HTTPS connection failures, from malformed URIs to TLS handshakes

**Use when**: Requests fail, connections drop, handshakes error, or a socket misbehaves

**Last Updated**: 2026-11-05

Merges `networking-debugging` and `tls-debugging` - TLS is a transport inside networking,
not a separate discipline; both cited the same SNI and procedure docs.

---

## CRITICAL RULES

1. **ALWAYS** verify the URI has a path component - send `/`, not an empty string
2. **ALWAYS** attach a state listener to every HttpExchange; without one, errors are silent
3. **ALWAYS** pass SNI explicitly when connecting to an IP address over TLS
4. **ALWAYS** read the mbedTLS error code before guessing at certificate problems
5. **NEVER** conclude a connection failed for transport reasons before checking whether the
   peer simply finished and closed - see timeout-hang-analysis

## Workflow

```cpp
#define CHICKEN_HTTP_EXCHANGE_LOG_LEVEL 4
#define CHICKEN_SOCKET_LOG_LEVEL 4
#define CHICKEN_TLS_SOCKET_LOG_LEVEL 4        // TLS only

// SNI is mandatory when the host is an IP literal
auto exchange = MakeHttpExchange(scheduler, "192.168.1.100", 443,
                                 ROOT_CA, weakPtr(this),
                                 "mydevice.local");        // SNI = real hostname

_httpExchange->setStateListener(sharedPtr(this));       // errors stop being silent
```

```bash
pio test -e native -vvv 2>&1 > investigation/logs/net_debug_$(date +%Y%m%d_%H%M%S).log
```

## Failure table

| Symptom | Likely cause |
|---|---|
| `400 Bad Request` | Missing `/` in URI path |
| Connection refused | Test server not running - kill and restart it first |
| TLS handshake failed | Missing SNI, or incomplete certificate chain |
| `-9984` | Certificate verification failed - usually missing SNI |
| `-9985` | Certificate not yet valid |
| `-9986` | Certificate expired |
| Connection closed mid-body | Desync or premature destruction - see timeout-hang-analysis |

---

**Key references**:
- [Debugging/tls_debugging_procedure.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/tls_debugging_procedure.md) - Complete TLS procedure
- [Debugging/uri_path_handling.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Debugging/uri_path_handling.md) - URI path handling
- [Common/TLS_SNI_REQUIREMENT_2025-11-25.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md) - SNI requirement
- [Common/TLS_CERTIFICATE_GENERATION.md](/Users/marco/devel/ChickenWorld/ChickenDocs/Common/TLS_CERTIFICATE_GENERATION.md) - Certificate generation
- [ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md](/Users/marco/devel/ChickenWorld/ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Architecture

**Skills this relies on**:
- [coding](../coding/SKILL.md) - Coding standards
- [chickenworld-testing](../chickenworld-testing/SKILL.md) - Testing procedures
- [timeout-hang-analysis](../timeout-hang-analysis/SKILL.md) - Stalled vs slow transfers
