# Pair Programming Agent - Context

## Purpose

Create a Claude agent that enforces graduated assistance to prevent skill atrophy when coding with AI. Based on MIT professor
Roberto Rigobon's neuroplasticity concerns: "When we stop using our brains... we forget."

## The Problem

"Vibe coding" with AI can create deceptive productivity while atrophying problem-solving skills. Need structured collaboration
that maintains cognitive load.

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

```text
pair-programmer/
├── agents/
│   └── coach.md              # Agent definition (agent ID: pair-programmer:coach)
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest (name, version, description)
├── CLAUDE.md                 # This file - development context
├── README.md                 # User-facing philosophy & usage
└── install                   # Deprecation notice (replaced by plugin system)
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

**Phase:** Complete (v1.1.0 Released — 2026-04-03)

**v1.0.0 — Plugin Framework Migration:**

- Migrated to Claude Code plugin framework (`pair-programmer` plugin, `coach` agent)
- Agent ID: `pair-programmer:coach`; agent file: `agents/coach.md`
- Added `.claude-plugin/plugin.json`, `.markdownlint.json`
- Added to `ali5ter/claude-plugins` marketplace
- All four levels fully defined with enforcement rules and response patterns
- Session state tracking implemented
- Testing completed across all four levels
- GitHub release v1.0.0: <https://github.com/ali5ter/pair-programmer/releases/tag/v1.0.0>

**v1.1.0 — Agent Quality Pass (2026-04-03):**

All 11 open GitHub issues resolved across four grouped PRs:

- **#1, #3 (PR #12):** Fixed typo "refering" → "referring"; updated `description` examples to use
  current delegation language (no "Task tool" narration) and consistent `pair-programmer:coach` agent ID
- **#7, #9 (PR #13):** Added quantitative Level 3 substantive-modification rubric; generalised
  Alister-specific content (experience-level inference, simplicity as a question not a mandate,
  language-agnostic tool preferences)
- **#2, #8, #10 (PR #14):** Added name-elicitation step to initialization flow; added Session Wrap-up
  retrospective section; added `maxTurns: 40` frontmatter field
- **#4, #5, #6, #11 (PR #15):** Added `tools: Read, Glob, Grep, Bash` (least privilege); added
  `memory: user` with guidance on what to persist; added `initialPrompt` for automatic greeting and
  level declaration; enriched `plugin.json` with agents manifest and `minVersion: 2.0.0`

**Agent definition format note:**

The `description` field is meta-documentation for the main Claude Code instance. It must be a quoted
single-line string with `\n\n` escaped newlines and `<example>` blocks. Examples should model current
delegation language — no "Task tool" narration. The examples are pattern-recognition training data,
not just docs.

**Invocation methods:**

- Direct launch: `claude --agent pair-programmer:coach` — agent greets automatically via `initialPrompt`
- Auto-delegation: Main Claude recognises level declarations and delegates to `pair-programmer:coach`

## Next Steps (Ongoing)

1. **Monitor Usage Patterns:** Gather real-world usage data to inform future iterations.
2. **Watch Plugin Framework Updates:** Adapt to any Anthropic plugin framework changes.
3. **Evaluate Additional Agents:** Consider whether a `reviewer` or other role agent adds value under the
   `pair-programmer` plugin namespace.
4. **Agent Directory Submission:** If Anthropic publishes an official plugin/agent directory, consider submitting.

## Notes

- This is meta: building this agent is itself a Level 2 exercise
- Avoid premature architecture—start minimal
- User has existing multi-provider chatbot framework that could be referenced
- Focus on preventing skill atrophy, not just productivity
