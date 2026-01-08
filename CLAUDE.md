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

**Phase:** Testing (Implementation Complete)

**Completed:**
- Agent definition created at `agent/pair-programmer.md` (487 lines with full enforcement logic)
- README.md written with philosophy, usage patterns, and examples
- Install script created and tested (`./install` → `~/.claude/agents/pair-programmer.md`)
- Project structure finalized with pfb submodule for bash utilities
- All four levels fully defined with enforcement rules and response patterns
- Session state tracking implemented (current_level, turn_owner, ai_code_blocks_count, explain_back_pending)

**Ready for Testing:**
The agent is fully implemented and installed. Next phase is real-world usage testing.

## Next Steps

1. **Test with Real Project:** Use the agent on an actual coding task. Test all four levels. Evaluate whether enforcement feels helpful or bureaucratic.
2. **Gather Usage Feedback:** Document what works, what needs adjustment, where flexibility is needed vs where firmness is appropriate.
3. **Iterate on Enforcement:** Adjust tone, prompts, and rules based on actual usage patterns and user feedback.
4. **Evaluate Level Granularity:** Confirm four levels is the right number. Check if users naturally map tasks to levels or if any level goes unused.
5. **Consider Public Release:** If proven valuable, add LICENSE, CONTRIBUTING.md, create GitHub remote, and release as open-source agent.
6. **Document Best Practices:** Based on testing, document which types of projects work best with which levels.

## Notes

- This is meta: building this agent is itself a Level 2 exercise
- Avoid premature architecture—start minimal
- User has existing multi-provider chatbot framework that could be referenced
- Focus on preventing skill atrophy, not just productivity