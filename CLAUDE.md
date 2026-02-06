# Horizon Agent - Claude Code AI Framework

## 📋 Project Overview

**Horizon Agent** is a sophisticated Claude Code AI Agent Framework that enhances Claude's development capabilities through specialized personas, enforced best practices, and integrated workflows. This is a **meta-programming framework** that teaches Claude how to work more effectively across diverse technical domains.

### What This Framework Provides

- **🎭 13 Specialized Agent Personas** - Expert roles for different development tasks
- **⚡ 12 User-Invoked Commands** - Workflows for complex operations
- **🎯 9 Skill Domains** - Deep reference material for best practices
- **📏 Comprehensive Rule Sets** - Language-agnostic and language-specific standards
- **🔗 Claude Code Hooks** - Integration with tool ecosystem for automation

### Core Philosophy

This framework operates on a **persona-based approach** where Claude adopts different expert identities based on the task at hand. It enforces quality through multi-layered checks: security reviews, code quality analysis, test coverage requirements, and performance optimization.

---

## 🏗️ Project Structure

```
Horizon_agent/
├── agents/              # 13 specialized expert personas
│   ├── architect.md
│   ├── planner.md
│   ├── code-reviewer.md
│   ├── python-reviewer.md
│   ├── security-reviewer.md
│   ├── build-error-resolver.md
│   ├── database-reviewer.md
│   ├── e2e-runner.md
│   ├── doc-updater.md
│   ├── refactor-cleaner.md
│   ├── tdd-guide.md
│   ├── go-reviewer.md
│   └── go-build-resolver.md
│
├── commands/            # 12 user-invoked workflows
│   ├── code-review.md
│   ├── python-review.md
│   ├── build-fix.md
│   ├── checkpoint.md
│   ├── evolve.md
│   ├── learn.md
│   ├── refactor-clean.md
│   ├── update-docs.md
│   ├── update-codemaps.md
│   ├── multi-backend.md
│   ├── multi-frontend.md
│   └── multi-execute.md
│
├── skills/              # 9 best practice domains
│   ├── python-patterns/
│   ├── python-testing/
│   ├── tdd-workflow/
│   ├── backend-patterns/
│   ├── frontend-patterns/
│   ├── coding-standards/
│   ├── verification-loop/
│   ├── strategic-compact/
│   └── iterative-retrieval/
│
├── rules/               # Standards & conventions
│   ├── common/          # Language-agnostic rules
│   │   ├── coding-style.md
│   │   ├── git-workflow.md
│   │   ├── testing.md
│   │   ├── security.md
│   │   ├── performance.md
│   │   ├── patterns.md
│   │   ├── agents.md
│   │   └── hooks.md
│   ├── python/          # Python-specific rules
│   │   ├── coding-style.md
│   │   ├── testing.md
│   │   ├── security.md
│   │   ├── patterns.md
│   │   └── hooks.md
│   └── README.md
│
├── hooks/
│   └── hooks.json       # Claude Code tool integration
│
├── CLAUDE.md            # This file
└── main.py              # Sample Python script
```

---

## 🎭 Agents (Expert Personas)

Agents are specialized personas that Claude adopts for specific development tasks. Each agent has expertise in a particular domain and uses specific tools.

### Development & Planning Agents

#### 1. **architect** (`agents/architect.md`)
**When to Use:** System design, scalability planning, architectural decisions
- Designs system architecture for new features
- Evaluates technical trade-offs
- Recommends patterns and best practices
- Creates Architecture Decision Records (ADRs)
- Plans for scalability and future growth
- **Model:** Opus (for complex reasoning)
- **Tools:** Read, Grep, Glob

#### 2. **planner** (`agents/planner.md`)
**When to Use:** Breaking down complex features into implementable tasks
- Creates detailed implementation plans
- Breaks down features into actionable steps
- Identifies dependencies and risks
- Provides specific file paths for changes
- Estimates complexity and timeline
- **Model:** Opus
- **Tools:** Read, Grep, Glob

### Code Review Agents

#### 3. **code-reviewer** (`agents/code-reviewer.md`)
**When to Use:** General code quality review (any language)
- Comprehensive quality assessment
- Security vulnerability detection
- Performance analysis
- Best practices enforcement
- Blocking/Warning/Suggestion categorization
- **Model:** Opus
- **Tools:** Read, Grep, Glob, Bash

#### 4. **python-reviewer** (`agents/python-reviewer.md`)
**When to Use:** Python-specific code review (REQUIRED for Python projects)
- PEP 8 compliance checking
- Type hint validation
- Pythonic idioms enforcement
- SQL/Command injection detection
- Path traversal prevention
- Pickle/YAML security checks
- **Model:** Opus
- **Tools:** Read, Grep, Glob, Bash

#### 5. **security-reviewer** (`agents/security-reviewer.md`)
**When to Use:** Security vulnerability scanning (all projects)
- OWASP Top 10 detection
- Hardcoded secrets detection
- Input validation verification
- Authentication/authorization checks
- Financial transaction security
- Blockchain/Solana security
- Database RLS verification
- **Model:** Opus
- **Tools:** Read, Grep, Glob, Bash

#### 6. **database-reviewer** (`agents/database-reviewer.md`)
**When to Use:** PostgreSQL/Supabase database work
- Query optimization (EXPLAIN ANALYZE)
- Schema design review
- Row Level Security (RLS) policies
- Index optimization
- Concurrency and deadlock prevention
- Connection pooling configuration
- **Model:** Opus
- **Tools:** Read, Grep, Glob, Bash

#### 7. **go-reviewer** (`agents/go-reviewer.md`)
**When to Use:** Go language code review
- Go idioms and best practices
- Error handling patterns
- Concurrency safety
- Memory management
- **Model:** Opus
- **Tools:** Read, Grep, Glob, Bash

### Build & Error Resolution Agents

#### 8. **build-error-resolver** (`agents/build-error-resolver.md`)
**When to Use:** TypeScript/Build compilation errors
- TypeScript type errors resolution
- Import/module resolution
- Type inference failures
- Minimal diff changes (no refactoring)
- Next.js 15 + React 19 compatibility
- Supabase/Redis/Solana type fixes
- **Model:** Sonnet (for speed)
- **Tools:** Read, Edit, Bash

#### 9. **go-build-resolver** (`agents/go-build-resolver.md`)
**When to Use:** Go compilation errors
- Go build errors resolution
- Dependency issues
- Import path problems
- **Model:** Sonnet
- **Tools:** Read, Edit, Bash

### Testing & Automation Agents

#### 10. **e2e-runner** (`agents/e2e-runner.md`)
**When to Use:** End-to-end testing with Playwright or Agent Browser
- Vercel Agent Browser integration (primary)
- Playwright automation (fallback)
- Semantic selectors (avoid brittle selectors)
- Test artifact management (screenshots, videos, traces)
- Flaky test handling
- **Model:** Opus
- **Tools:** Read, Write, Bash

#### 11. **tdd-guide** (`agents/tdd-guide.md`)
**When to Use:** Test-Driven Development workflow
- RED: Write failing tests first
- GREEN: Minimal implementation to pass
- REFACTOR: Improve code quality
- 80%+ coverage enforcement
- Test-first methodology
- **Model:** Opus
- **Tools:** Read, Write, Bash

### Maintenance & Documentation Agents

#### 12. **refactor-cleaner** (`agents/refactor-cleaner.md`)
**When to Use:** Dead code elimination and cleanup
- Unused code detection (knip, depcheck, ts-prune)
- Duplicate code consolidation
- Safe refactoring with test verification
- Deletion logging for auditability
- **Model:** Opus
- **Tools:** Read, Edit, Bash

#### 13. **doc-updater** (`agents/doc-updater.md`)
**When to Use:** Documentation and codemap generation
- Codemap generation from codebase
- AST analysis using ts-morph
- Dependency mapping
- README and guide updates
- **Model:** Sonnet
- **Tools:** Read, Write, Bash

---

## ⚡ Commands (User-Invoked Workflows)

Commands are explicit workflows triggered by users for complex operations.

### Code Quality Commands

#### `/code-review` (`commands/code-review.md`)
Comprehensive security and quality review of uncommitted changes
- Runs `git diff --name-only HEAD`
- Checks for security issues (CRITICAL)
- Validates code quality (HIGH)
- Enforces best practices (MEDIUM)
- **Blocks commits** on CRITICAL/HIGH issues

#### `/python-review` (`commands/python-review.md`)
Python-specific code review with static analysis
- Invokes `python-reviewer` agent
- Runs ruff, mypy, pylint, black
- PEP 8 compliance
- Security vulnerability scanning

### Build & Error Commands

#### `/build-fix` (`commands/build-fix.md`)
Fix TypeScript/build compilation errors
- Invokes `build-error-resolver` agent
- Minimal diff approach
- Type inference fixes
- Import resolution

### Maintenance Commands

#### `/refactor-clean` (`commands/refactor-clean.md`)
Dead code elimination workflow
- Invokes `refactor-cleaner` agent
- Runs knip/depcheck/ts-prune
- Safe deletion with tests
- Generates deletion log

#### `/update-docs` (`commands/update-docs.md`)
Update project documentation
- Invokes `doc-updater` agent
- Regenerates codemaps
- Updates README files

#### `/update-codemaps` (`commands/update-codemaps.md`)
Regenerate architectural codemaps
- AST analysis with ts-morph
- Dependency graph generation
- Component relationship mapping

### Development Workflow Commands

#### `/checkpoint` (`commands/checkpoint.md`)
Save current session state for recovery
- Captures conversation context
- Saves work-in-progress
- Creates restore point

#### `/learn` (`commands/learn.md`)
Extract patterns from recent work for framework evolution
- Analyzes recent development patterns
- Identifies reusable behaviors
- Records to instinct system

#### `/evolve` (`commands/evolve.md`)
Cluster instincts into new agents/skills/commands
- Analyzes instinct patterns
- Generates new agent/skill proposals
- Confidence scoring
- Framework self-improvement

### Multi-Mode Commands

#### `/multi-backend` (`commands/multi-backend.md`)
Parallel backend development across multiple services

#### `/multi-frontend` (`commands/multi-frontend.md`)
Parallel frontend development across multiple components

#### `/multi-execute` (`commands/multi-execute.md`)
Execute multiple independent workflows simultaneously

---

## 🎯 Skills (Best Practice Domains)

Skills provide deep reference material for automated behaviors. Always consult relevant skills before implementing code.

### Python Skills

#### `skills/python-patterns/` (17KB)
Comprehensive Pythonic idioms and patterns
- Type hints and modern annotations
- Error handling patterns (`try/except/finally`, custom exceptions)
- Context managers (`with` statement, `__enter__`/`__exit__`)
- Comprehensions and generators
- Data classes and NamedTuples
- Decorators (function, class-based, parameterized)
- Concurrency (threading, multiprocessing, async/await)
- Package organization and imports
- Memory optimization (`__slots__`, generators)
- Performance tips
- **Anti-patterns to avoid**

#### `skills/python-testing/` (19KB)
Python testing strategies with pytest
- TDD methodology (red-green-refactor)
- pytest fundamentals
- Fixtures (scopes: function/class/module/session)
- Parametrization (`@pytest.mark.parametrize`)
- Markers and test selection
- Mocking and patching (`unittest.mock`, `pytest-mock`)
- Async testing (`pytest-asyncio`)
- Exception testing (`pytest.raises`)
- Test organization (directory structure)
- **Coverage requirements: 80%+ mandatory**

### Testing & TDD Skills

#### `skills/tdd-workflow/`
Test-Driven Development process
- RED-GREEN-REFACTOR cycle
- Unit, integration, E2E test patterns
- Jest/Vitest patterns (frontend)
- API integration testing
- Playwright E2E patterns
- Mocking external services (Supabase, Redis, OpenAI)
- Test file organization
- Coverage verification

### Architecture & Patterns Skills

#### `skills/backend-patterns/`
Backend/API development patterns
- REST API design
- Database access patterns
- Error handling strategies
- Authentication/authorization
- Rate limiting
- Caching strategies

#### `skills/frontend-patterns/`
Frontend/UI development patterns
- Component composition
- State management
- Performance optimization
- Accessibility (a11y)
- Responsive design

#### `skills/coding-standards/`
Universal code quality standards
- Naming conventions
- Code organization
- Comment guidelines
- Error handling
- Logging practices

### Advanced Skills

#### `skills/verification-loop/`
Verification and testing loops
- Continuous validation
- Feedback cycles
- Quality gates

#### `skills/strategic-compact/`
Context compaction strategies for long conversations
- Semantic compression
- State preservation
- Context prioritization

#### `skills/iterative-retrieval/`
Iterative code search patterns
- Efficient codebase exploration
- Progressive refinement
- Search optimization

---

## 📏 Rules (Standards & Conventions)

Rules define "what" to do; skills define "how" to do it.

### Common Rules (Language-Agnostic)

Located in `rules/common/`:

1. **`coding-style.md`** - Universal formatting and style standards
2. **`git-workflow.md`** - Git practices and commit conventions
3. **`testing.md`** - Testing standards and coverage requirements
4. **`security.md`** - Security principles (secrets, validation, auth)
5. **`performance.md`** - Performance optimization principles
6. **`patterns.md`** - Common design patterns (SOLID, DRY, KISS)
7. **`agents.md`** - Agent activation and usage guidelines
8. **`hooks.md`** - Claude Code hooks configuration

### Python-Specific Rules

Located in `rules/python/`:

1. **`coding-style.md`** - PEP 8 compliance, Black formatting
2. **`testing.md`** - pytest patterns, 80%+ coverage
3. **`security.md`** - SQL injection, command injection, path traversal
4. **`patterns.md`** - Pythonic idioms, comprehensions, decorators
5. **`hooks.md`** - Python-specific hook configurations

**Rule Application:**
- Common rules apply universally across all languages
- Language-specific rules extend common rules with framework examples
- Rules are **enforced** during code review by respective agents

---

## 🔗 Hooks (Claude Code Integration)

Hooks integrate with Claude Code's tool ecosystem to intercept and enhance tool usage.

### PreToolUse Hooks (Before Tool Execution)

#### 1. **Block Dev Servers Outside tmux**
```json
Matcher: "npm run dev" | "pnpm dev" | "yarn dev" | "bun run dev"
Action: BLOCK with error message
Reason: Ensures log access via tmux sessions
```

#### 2. **Remind tmux for Long Commands**
```json
Matcher: npm install | pytest | cargo build | docker | vitest | playwright
Action: Warning reminder (non-blocking)
Suggestion: "tmux new -s dev" | "tmux attach -t dev"
```

#### 3. **Review Before Git Push**
```json
Matcher: "git push"
Action: Reminder to review changes
Prevents: Accidental push of unreviewed code
```

#### 4. **Block Random .md File Creation**
```json
Matcher: Write tool + *.md (except README/CLAUDE/CONTRIBUTING)
Action: BLOCK creation
Reason: Keeps documentation consolidated
```

#### 5. **Suggest Manual Compaction**
```json
Matcher: Edit | Write tools
Action: Suggest compaction at logical intervals
Prevents: Unnecessary auto-compaction
```

### PostToolUse Hooks (After Tool Execution)

#### 1. **Log PR URL After Creation**
```json
Matcher: "gh pr create"
Action: Extract and log PR URL
Provides: Review command (gh pr review <PR>)
```

#### 2. **Auto-format JavaScript/TypeScript**
```json
Matcher: Successful npm/pnpm/yarn/bun build
Action: Run Prettier formatting
Ensures: Consistent code formatting
```

#### 3. **TypeScript Type Checking**
```json
Matcher: TypeScript file changes
Action: Run tsc --noEmit
Catches: Type errors immediately
```

#### 4. **Warn About console.log**
```json
Matcher: console.log in committed code
Action: Warning (non-blocking)
Suggests: Use proper logging library
```

### Session Hooks

#### **SessionStart**
- Loads previous conversation context
- Detects package manager (npm/pnpm/yarn/bun)
- Restores workspace state

#### **PreCompact**
- Saves state before context compaction
- Creates checkpoint for recovery
- Preserves important conversation history

#### **SessionEnd**
- Persists session state to disk
- Evaluates session for extractable patterns
- Triggers `/learn` command for instinct recording

---

## 🚀 Usage Guide

### How to Invoke Agents

Agents are invoked contextually based on task requirements:

#### Explicit Invocation (Recommended)
```
"@architect, please review the system design for the new payment service"
"@python-reviewer, review the changes in src/api/user.py"
"@security-reviewer, scan for vulnerabilities in the authentication module"
```

#### Implicit Invocation (Automatic)
- Python file changes → `python-reviewer` automatically activated
- Build errors → `build-error-resolver` invoked
- Test writing → `tdd-guide` engaged

#### FRONTLOAD Pattern (Critical Reviews)
For critical reviews, explicitly load agent files in instructions:
```
Read agents/security-reviewer.md and agents/python-reviewer.md,
then review src/auth/ for security issues.
```

### How to Use Commands

Commands are explicit workflows invoked by users:

```bash
# Code review before commit
/code-review

# Fix TypeScript build errors
/build-fix

# Clean up dead code
/refactor-clean

# Update documentation
/update-docs

# Save checkpoint before risky refactor
/checkpoint

# Analyze patterns and evolve framework
/learn
/evolve
```

### How to Apply Skills

Skills are automatically referenced during relevant tasks:

**Automatic Reference:**
- Writing Python code → `python-patterns` consulted
- Writing tests → `python-testing` or `tdd-workflow` referenced
- Backend API → `backend-patterns` applied
- Frontend component → `frontend-patterns` used

**Manual Reference:**
```
"Refer to skills/python-patterns/ and refactor this code to be more Pythonic"
"Use skills/tdd-workflow/ to guide test creation for the new feature"
```

### How Rules Are Enforced

Rules are enforced during agent reviews:

1. **Automatic Enforcement:**
   - Code reviews check rule compliance
   - Build errors trigger rule-based fixes
   - Git hooks enforce commit standards

2. **Manual Verification:**
   ```
   "Check if this code follows rules/python/security.md"
   "Verify compliance with rules/common/testing.md"
   ```

---

## 📖 Development Workflow Examples

### Example 1: New Feature Implementation (TDD)

```
1. User: "Implement a user authentication service with JWT tokens"

2. @planner: Creates detailed implementation plan
   - Identifies files to create/modify
   - Defines API endpoints
   - Plans database schema
   - Estimates complexity

3. @architect: Reviews design
   - Validates scalability
   - Suggests security patterns
   - Recommends JWT library (PyJWT)

4. @tdd-guide: Initiates RED phase
   - Writes failing tests first
   - test_authentication.py created
   - Edge cases covered (expired tokens, invalid signatures)

5. Developer: Implements GREEN phase
   - auth_service.py implementation
   - Tests pass

6. @python-reviewer: Reviews implementation
   - PEP 8 compliance ✓
   - Type hints present ✓
   - No SQL injection ✓

7. @security-reviewer: Security scan
   - Hardcoded secrets ✗ Found in line 45
   - Input validation ✓
   - Recommends: Use environment variables

8. Fix: Move secret to .env file

9. @code-reviewer: Final quality check
   - Function length ✓
   - Error handling ✓
   - Tests present ✓

10. /code-review: Pre-commit review
    - All checks pass ✓
    - Ready to commit

11. Git commit: Hooks auto-format code with Prettier
```

### Example 2: Debugging Build Errors

```
1. User: "Fix the TypeScript errors in src/api/"

2. @build-error-resolver: Analyzes errors
   - Identifies type inference failures
   - Locates missing imports
   - Detects Next.js 15 compatibility issues

3. Fixes applied:
   - Adds explicit type annotations
   - Updates import paths
   - Fixes React 19 prop types

4. Verification: npm run build
   - Build succeeds ✓

5. @code-reviewer: Post-fix review
   - Changes are minimal ✓
   - No refactoring introduced ✓
```

### Example 3: Security Audit

```
1. User: "/code-review before production deployment"

2. @security-reviewer: Comprehensive scan
   - Hardcoded secrets → CRITICAL: API key in config.py:12
   - SQL injection → HIGH: String concatenation in db.py:45
   - XSS vulnerability → HIGH: Unescaped output in template.html:78
   - Missing CSRF token → MEDIUM: forms.py:23

3. Fixes required (BLOCKING):
   - Move API key to environment variable
   - Use parameterized queries
   - Add template auto-escaping
   - Add CSRF protection

4. After fixes: /code-review again
   - All CRITICAL issues resolved ✓
   - All HIGH issues resolved ✓
   - Ready for deployment ✓
```

### Example 4: Dead Code Cleanup

```
1. User: "/refactor-clean to remove unused code"

2. @refactor-cleaner: Analysis
   - Runs knip for dead code detection
   - Runs depcheck for unused dependencies
   - Identifies 47 unused functions
   - Identifies 12 unused imports
   - Identifies 3 unused dependencies

3. Deletion plan with tests:
   - Delete unused functions → Run tests → Pass ✓
   - Remove unused imports → Run tests → Pass ✓
   - Uninstall unused deps → Run tests → Pass ✓

4. Result: Deletion log generated
   - 1,234 lines removed
   - Bundle size reduced by 15%
   - Build time reduced by 8%
```

---

## 🎯 Quick Reference

### When to Use Which Agent

| Task | Agent | Priority |
|------|-------|----------|
| System design | `architect` | Use for architectural decisions |
| Feature breakdown | `planner` | Use for complex features |
| General code review | `code-reviewer` | Use for all projects |
| Python code review | `python-reviewer` | **REQUIRED** for Python |
| Security scan | `security-reviewer` | Use for all projects |
| Database optimization | `database-reviewer` | Use for DB work |
| TypeScript errors | `build-error-resolver` | Auto-invoked on build errors |
| E2E testing | `e2e-runner` | Use for integration tests |
| TDD guidance | `tdd-guide` | Use for test-first development |
| Dead code cleanup | `refactor-cleaner` | Use before releases |
| Documentation | `doc-updater` | Use after major changes |

### Command Cheat Sheet

```bash
# Code Quality
/code-review              # Full review before commit
/python-review            # Python-specific review

# Build & Errors
/build-fix                # Fix TypeScript build errors

# Maintenance
/refactor-clean           # Remove dead code
/update-docs              # Update documentation
/update-codemaps          # Regenerate codemaps

# Workflow
/checkpoint               # Save session state
/learn                    # Extract patterns
/evolve                   # Generate new agents/skills

# Multi-Mode
/multi-backend            # Parallel backend work
/multi-frontend           # Parallel frontend work
/multi-execute            # Parallel workflows
```

### Skill Reference Map

```
Python Development:
  ├─ python-patterns/      → Idioms, decorators, async
  ├─ python-testing/       → pytest, fixtures, mocking
  └─ tdd-workflow/         → RED-GREEN-REFACTOR

Backend Development:
  ├─ backend-patterns/     → REST API, database, auth
  └─ database-reviewer     → Query optimization, RLS

Frontend Development:
  ├─ frontend-patterns/    → Components, state, a11y
  └─ coding-standards/     → Naming, organization

Testing:
  ├─ tdd-workflow/         → Test-first methodology
  ├─ python-testing/       → pytest patterns
  └─ verification-loop/    → Continuous validation

Architecture:
  ├─ architect             → System design
  ├─ backend-patterns/     → API patterns
  └─ frontend-patterns/    → UI patterns
```

---

## 🔧 Configuration & Customization

### Adding New Agents

1. Create `agents/new-agent.md` with frontmatter:
```markdown
---
name: new-agent
description: Brief description of expertise
tools: ["Read", "Grep", "Glob", "Bash"]
model: opus
---

[Agent instructions here]
```

2. Document in `rules/common/agents.md`
3. Reference in `CLAUDE.md` (this file)

### Adding New Commands

1. Create `commands/new-command.md`
2. Define workflow steps
3. Specify which agents to invoke
4. Add to command cheat sheet

### Adding New Skills

1. Create `skills/new-skill/SKILL.md`
2. Provide comprehensive reference material
3. Reference from relevant agents
4. Update skill reference map

### Extending Rules

1. **Common rules:** Add to `rules/common/`
2. **Language-specific:** Add to `rules/<language>/`
3. Update enforcement in relevant agents

### Customizing Hooks

Edit `hooks/hooks.json`:
- **PreToolUse:** Block or warn before tool execution
- **PostToolUse:** Enhance or validate after execution
- **Session:** Lifecycle management

---

## 🎓 Best Practices

### 1. **Always Frontload Critical Agents**
For critical reviews, explicitly load agent files:
```
Read agents/security-reviewer.md and agents/python-reviewer.md
before reviewing authentication code.
```

### 2. **Use TDD for All New Features**
- Write tests first (RED)
- Implement minimally (GREEN)
- Refactor safely (REFACTOR)
- Maintain 80%+ coverage

### 3. **Run `/code-review` Before Every Commit**
- Catches security issues
- Enforces code quality
- Blocks CRITICAL/HIGH issues

### 4. **Leverage Multi-Mode Commands**
For parallel work:
```bash
/multi-backend   # Work on multiple services simultaneously
/multi-frontend  # Work on multiple components in parallel
```

### 5. **Checkpoint Before Risky Operations**
```bash
/checkpoint      # Save state before major refactor
```

### 6. **Evolve the Framework**
As patterns emerge:
```bash
/learn           # Record new patterns
/evolve          # Generate new agents/skills
```

### 7. **Use Semantic Selectors in E2E Tests**
Avoid brittle selectors:
```python
# Bad
driver.find_element_by_xpath("//div[3]/button[2]")

# Good
driver.find_element_by_test_id("submit-button")
```

### 8. **Never Commit with Security Issues**
- Hardcoded secrets → CRITICAL
- SQL injection → CRITICAL
- XSS vulnerabilities → CRITICAL
- **BLOCK COMMIT** until resolved

---

## 🐛 Troubleshooting

### Issue: Agent Not Activating

**Solution:**
- Use explicit invocation: `@agent-name`
- Check agent frontmatter in `agents/` directory
- Verify tools are available

### Issue: Hooks Not Triggering

**Solution:**
- Verify `hooks/hooks.json` syntax
- Check matcher regex patterns
- Ensure Claude Code hooks are enabled

### Issue: Skills Not Referenced

**Solution:**
- Explicitly reference: "Use skills/python-patterns/"
- Check skill file structure (SKILL.md)
- Verify agent is configured to use skill

### Issue: Build Errors Not Auto-Fixing

**Solution:**
- Invoke `@build-error-resolver` explicitly
- Check error logs for TypeScript version compatibility
- Verify model is set to "sonnet" for speed

---

## 📚 Additional Resources

### Project Links
- **Repository:** https://github.com/HorizonHJY/Horizon_agent.git
- **Issues:** Use GitHub Issues for bugs/features

### Related Documentation
- `rules/README.md` - Detailed rule system explanation
- `agents/` - Individual agent documentation
- `skills/` - Deep-dive best practice guides
- `hooks/hooks.json` - Hook configuration reference

### Learning Resources
- **TDD:** `skills/tdd-workflow/`
- **Python:** `skills/python-patterns/` + `skills/python-testing/`
- **Security:** `agents/security-reviewer.md`
- **Architecture:** `agents/architect.md`

---

## 🎯 Key Takeaways

1. **Persona-Based:** Claude adopts expert identities for tasks
2. **Comprehensive:** Covers entire development lifecycle
3. **Enforcement-Focused:** Rules prevent common mistakes
4. **Security-First:** Multiple security review layers
5. **Quality-Enforcing:** 80%+ test coverage mandatory
6. **Scalable:** Supports multiple languages and stacks
7. **Learning-Enabled:** Can evolve from observed patterns
8. **Integration-Rich:** Hooks into Claude Code ecosystem

---

**🎮 Ready to build high-quality, secure software with AI-powered development assistance!**
