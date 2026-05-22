# Skill: Organize AGENTS.md Content

**Purpose**: Systematically move content from AGENTS.md to appropriate ChickenDocs locations, keeping AGENTS.md as minimal index

**Use when**:
- Reducing AGENTS.md size
- Reorganizing documentation structure
- Moving content to proper ChickenDocs locations
- Creating minimal redirect references

---

## Rules

**AGENTS.md should be ≤100 lines** with ONLY:
1. Search rule (add references when finding useful docs)
2. Quick reference index (table with links)
3. Minimal redirect references (1-2 lines per topic)

**CRITICAL**: All detailed content must exist in ChickenDocs before creating AGENTS.md reference

---

## Workflow

### 1. Categorize Content

**Review each section in AGENTS.md and categorize**:

**Category A: Generic ChickenWorld Knowledge**
- Logging best practices
- Avoid std::string rule
- Tokenizer optimization
- Circular references
- TLS SNI requirement
- Lifecycle management
- Formatted string creation

→ **Move to**: ChickenDocs/Common/

**Category B: Project-Specific Architecture**
- Test architecture pattern
- Test sequencing
- Environment variables
- Build flags
- Connection error handling

→ **Move to**: ChickenDocs/ChickenSoftwareUpdateLib/

**Category C: Investigation-Specific Details**
- Avoid ratholing guidance
- Manual testing procedures
- Session-specific findings

→ **Move to**: project/investigation/ or keep as redirect to ChickenDocs/Common/

### 2. Check Existing Documentation

**Before creating new docs, search ChickenDocs**:

**Generic content**:
```bash
cd /Users/marco/devel/ChickenWorld/ChickenDocs/Common
grep -r "logging\|lifecycle\|tokenizer" . --include="*.md"
```

**Project-specific content**:
```bash
cd /Users/marco/devel/ChickenWorld/ChickenDocs
grep -r "ChickenSoftwareUpdate\|test.*sequenc" . --include="*.md"
```

**Reference**: [development_guidelines.md](../../ChickenDocs/development_guidelines.md#documentation-first-investigation) - Documentation-first rule

### 3. Move Content to Appropriate Locations

**For Generic Knowledge**:
- IfChickenDocs/Common/LOGGING_BEST_PRACTICES.md exists, extend it
- IfChickenDocs/Common/TLS_SNI_REQUIREMENT_2025-11-25.md exists, extend it
- Create new file only if topic doesn't exist

**For Project-Specific Content**:
- Check if ChickenDocs/ChickenSoftwareUpdateLib/ exists
- Create ChickenDocs/ChickenSoftwareUpdateLib/ChickenSoftwareUpdateLib_PROJECT_STRUCTURE.md
- Move test sequencing details there

**Reference**:
- [DOCUMENTATION_ORGANIZATION_RULES.md](DOCUMENTATION_ORGANIZATION_RULES.md) - Organization rules
- [ChickenNetworkingLib_PROJECT_STRUCTURE.md](../../ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md) - Project structure template

### 4. Create Minimal Redirects in AGENTS.md

**Format** (keep each redirect to 2-3 lines max):

```markdown
### Logging
**See**: [ChickenDocs/Common/LOGGING_BEST_PRACTICES.md](../../ChickenDocs/Common/LOGGING_BEST_PRACTICES.md)
```

**NOT this** (too detailed for AGENTS.md):
```markdown
### Logging
- **NEVER** use `std::cout`/`std::cerr` - use ChickenWorld logging macros
- **Use**: `_debug()`, `_info()`, `_warning()`, `_error()` and tagged variants
- **Per-file setup**: Define component log level BEFORE includes:
  ```cpp
  #ifdef CHICKEN_SOFTWARE_UPDATE_LOG_LEVEL
  #define CHICKEN_LOG_LEVEL CHICKEN_SOFTWARE_UPDATE_LOG_LEVEL
  #endif
  #include <SoftwareUpdate.h>
  ```
```

### 5. Update Index Table

**Quick Reference Index should list ALL topics with direct links**:

```markdown
## Quick Reference Index

| Topic | Reference |
|-------|-----------|
| Logging | [ChickenDocs/Common/LOGGING_BEST_PRACTICES.md](../../ChickenDocs/Common/LOGGING_BEST_PRACTICES.md) |
| Circular References | [ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md](../../ChickenDocs/Common/LOOPED_LISTENER_CIRCULAR_REFERENCE_2025-12-06.md) |
| Test Architecture | [ChickenDocs/ChickenSoftwareUpdateLib/TEST_ARCHITECTURE.md](../../ChickenDocs/ChickenSoftwareUpdateLib/TEST_ARCHITECTURE.md) |
```

---

## Execution Steps

### Step 1: Inventory Current AGENTS.md
```bash
# Count sections and estimate size reduction
grep "^##" AGENTS.md
wc -l AGENTS.md
```

### Step 2: Search ChickenDocs for Existing Content
```bash
# Search for logging docs
grep -r "LOGGING\|logging" ChickenDocs/ --include="*.md" | head -20

# Search for lifecycle docs
grep -r "lifecycle\|ChickenPtr" ChickenDocs/Common/ --include="*.md" | head -20
```

### Step 3: Create Missing Documentation
- ChickenDocs/Common/DOCUMENTATION_LIFECYCLE_MANAGEMENT.md
- ChickenDocs/ChickenSoftwareUpdateLib/ChickenSoftwareUpdateLib_PROJECT_STRUCTURE.md
- ChickenDocs/ChickenSoftwareUpdateLib/TEST_ARCHITECTURE.md

### Step 4: Update AGENTS.md
- Keep only search rule + index table
- Add minimal redirects for each category
- Target: ≤100 lines total

---

## References This Skill Uses

1. **ChickenDocs/Common/** - Generic ChickenWorld guidelines
2. **ChickenDocs/ChickenSoftwareUpdateLib/** - Project-specific documentation
3. **DOCUMENTATION_ORGANIZATION_RULES.md** - Complete organization rules
4. **development_guidelines.md** - Development best practices
5. **ChickenDocs/ChickenNetworkingLib/ChickenNetworkingLib_PROJECT_STRUCTURE.md** - Project structure template

---

**Created**: 2026-05-21  
**Purpose**: Systematically reduce AGENTS.md to minimal index with proper references
