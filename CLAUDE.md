# Pair Programming Agent - Context

## Purpose

Create a Claude agent that enforces graduated assistance to prevent skill atrophy when coding with AI. Based on MIT professor Roberto Rigobon's neuroplasticity concerns: "When we stop using our brains... we forget."

## The Problem

"Vibe coding" with AI can create deceptive productivity while atrophying problem-solving skills. Need structured collaboration that maintains cognitive load.

## Solution: Graduated Assistance Framework

### Level 1: Pure Architecture (human codes everything)

- AI helps with design decisions, tradeoffs, API selection
- Human writes all code
- AI reviews and suggests improvements
- Example: "Should I use event delegation?" vs AI writing the handler

### Level 2: Scaffolding (AI provides structure, human fills logic)

- AI creates file structure, interfaces, type definitions
- Human implements actual logic
- Example: AI writes class skeleton with method signatures, human writes method bodies

### Level 3: Pair Programming (collaborative)

- Alternate: human writes a function, AI writes next
- Human must modify/improve AI code before moving on
- Forces active engagement with every piece

### Level 4: Full Generation (use sparingly)

- AI writes complete implementations
- Reserve for: boilerplate, well-solved problems, time-critical situations
- Human must explain every line back before using it

## Warning Signs of Dependency

- Can't explain how AI code works
- Copying without modification
- Uncomfortable coding without AI
- Reaching for AI before trying yourself

## Active Learning Techniques

1. **Explain-back protocol**: After AI provides anything, explain it back
2. **Modification requirement**: Change something in AI code before using it
3. **Implementation comparison**: Code it yourself first, then compare approaches
4. **Constraint exercises**: "Help me solve X but don't write code, only describe approach"

## Alister's User Profile

- Senior Staff Product Designer (retired) with deep technical background
- IBM programmer (1988), extensive patent portfolio
- Experience: 6502 assembler through modern full-stack
- Philosophy: Anti-cruft, future-proof, scriptable solutions
- Current: Bash optimization (pfb.sh), multi-provider AI chatbot, Homebridge on Pi
- Values: Systems thinking, understanding trade-offs, knowing what NOT to build

Note: The pair-programming Claude Agent would work for Alister but should be built for general use by other technical humans.

## Agent Requirements

### Core Functionality

1. **Mode Enforcement**: Programmatically enforce collaboration levels
2. **Session State**: Track current level, turn (in alternating mode), goals
3. **Guardrails**

   - Code generation limits per session
   - Mandatory explanation requirements
   - Metrics tracking (human vs AI code ratio)

4. **Minimal Bloat**: Start simple, add only what's proven necessary

### Agent Behavior

- Be specific, provide practical examples backed by real-world implementation
- Don't lead down paths that don't provide correct solution
- Leverage user's strengths: systems thinking, architectural judgment, performance intuition
- Use as research assistant, rubber duck, code reviewer, specialist—NOT replacement for problem-solving
- Teach the user how to use Claude Code features where needed

### Technical Preferences

Note these are Alister's preferences:

- Bash where appropriate (user has strong bash skills, pfb.sh utility)
- Python for complex state when needed or if User does not suggest a language.
- Scriptable, transparent implementations
- Git-aware when relevant
- Works with iTerm2, VS Code workflow

## Project Structure (Minimal)

```
pair-programmer/
├── agent/
│   └── pair-programmer.md    # Agent definition (487 lines)
├── lib/
│   └── pfb/                  # Bash utility library (git submodule)
├── CLAUDE.md                 # This file - development context
├── README.md                 # User-facing philosophy & usage
└── install                   # Install script (installs agent to ~/.claude/agents/)
```

Add complexity only when proven necessary. Current structure is minimal and functional.

## Session Declaration Pattern

User should start sessions by declaring level:

- "Level 1: I want to implement authentication flow myself, just advise"
- "Level 2: Give me class structure for chatbot framework, I'll implement methods"
- "Level 3: Let's alternate on this feature"
- "Level 4: Generate boilerplate for [well-solved problem]"

If a level can not be determined, ask the User how they want to engage using this Level framework.

## Success Criteria

- User maintains/improves coding ability
- Cognitive load equals or exceeds solo coding
- Better outcomes through collaboration vs delegation
- User can explain all code in their project
- Appropriate epistemic humility maintained

## Current Status

**Phase:** Complete (Testing Successful)

**Completed:**
- Agent definition created at `agent/pair-programmer.md` (487 lines with full enforcement logic)
- README.md written with philosophy, usage patterns, and examples
- Install script created and tested (`./install` → `~/.claude/agents/pair-programmer.md`)
- Project structure finalized with pfb submodule for bash utilities
- All four levels fully defined with enforcement rules and response patterns
- Session state tracking implemented (current_level, turn_owner, ai_code_blocks_count, explain_back_pending)
- **Testing completed successfully across all four levels**
- **Agent definition format fixed** (multiline description with escaped newlines and example blocks)
- **Level 4 explain-back enforcement strengthened** (blocks file operations until user demonstrates understanding)
- **Auto-invocation verified** (main Claude recognizes trigger patterns and launches via Task tool)

**Testing Results (2026-01-08):**

All four scenarios tested and validated:

1. **Level Detection Test** - Agent correctly prompts user to declare level when none specified. Explains framework and requests explicit declaration.

2. **Level 1 Advisory Mode Test** - Agent properly refuses to write code. Provides architectural advice, design patterns, tradeoffs only. Enforcement working correctly.

3. **Level 2 Scaffolding Test** - Agent provides class structure with method signatures and TODO markers but no implementation logic. Successfully delivers scaffolding requiring human logic implementation.

4. **Level 4 Explain-Back Test** - Initial test revealed weakness where agent offered file creation before explain-back. Strengthened enforcement with CRITICAL labels and explicit blocking. Retest confirmed proper blocking until user demonstrates understanding.

**Critical Discovery - Agent Definition Format:**

The `description` field in agent definition is meta-documentation that instructs the MAIN Claude Code agent when/how to invoke the subagent:

- Must be quoted multiline string with explicit escaped newlines (`\n\n`)
- Must include `<example>` blocks showing invocation patterns via Task tool
- Not just documentation - it's training data for pattern recognition
- Without proper format, agent remains invisible to main system

This understanding was the breakthrough that enabled auto-invocation.

**Installation Verification:**

Both invocation methods confirmed working:
- Direct launch: `claude --agent pair-programmer` (entire session in agent mode)
- Auto-launch: Main Claude recognizes patterns like "Level 2: scaffold X" and launches automatically

## Next Steps

1. **Create Public GitHub Repository:** Set up public repo for community access and contributions.
2. **Configure Git Remote:** Add remote origin and push committed code to GitHub.
3. **Add GitHub Documentation:** Consider CONTRIBUTING.md, enhanced LICENSE details if needed.
4. **Community Release:** Share agent for broader testing and feedback.
5. **Monitor Usage Patterns:** Gather real-world usage data to inform future iterations.
6. **Agent Directory Submission:** If Anthropic maintains an agent directory/marketplace, consider submission.

## Notes

- This is meta: building this agent is itself a Level 2 exercise
- Avoid premature architecture—start minimal
- User has existing multi-provider chatbot framework that could be referenced
- Focus on preventing skill atrophy, not just productivity