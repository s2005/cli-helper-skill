# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **CLI Helper Skill** - a Claude Code skill that helps users understand and work with command-line tools by organizing their help documentation into three structured levels of complexity (Basic, Medium, Advanced).

### Purpose

The CLI Helper Skill is particularly valuable for:
- Proprietary or custom internal CLI tools not widely documented
- Complex tools with extensive options
- Rare or specialized CLI utilities where parameter knowledge is limited
- Situations where accurate CLI parameter information is critical

## Core Architecture

### Skill Structure

Claude Code skills follow a progressive disclosure pattern with three resource types:

1. **SKILL.md** (Required) - Main skill configuration with YAML frontmatter
   - Contains `name` and `description` fields that determine when Claude activates the skill
   - Uses imperative/infinitive form (verb-first instructions) throughout
   - Kept lean (<5k words), detailed info moved to references/

2. **scripts/** - Executable code for deterministic, reusable operations
   - Used when the same code is repeatedly rewritten
   - Can be executed without loading into context

3. **references/** - Documentation loaded into context as needed
   - For schemas, API docs, domain knowledge, policies
   - Keeps SKILL.md focused while providing detailed information

4. **assets/** - Files used in output (NOT loaded into context)
   - Templates, images, boilerplate, fonts
   - Copied/modified in the final output

### GitHub Actions Workflow

The repository includes `.github/workflows/release-skill.yml` which automatically:

- Extracts version from VERSION file
- Validates SKILL.md structure (frontmatter with name/description)
- Builds skill distribution ZIP
- Attaches to GitHub releases

## Development Commands

### Testing the Skill Locally

Install skill to Claude Code skills directory:

```bash
# Windows (Git Bash)
cp -r . "$USERPROFILE/.claude/skills/cli-helper"

# Unix/Mac
cp -r . ~/.claude/skills/cli-helper
```

Test activation by asking Claude questions that match the skill description.

### Markdown Linting

The repository uses markdownlint-cli2 with line length checks disabled:

```bash
# Configuration in .markdownlint-cli2.jsonc
# MD013 (line length) is disabled to prevent linter warnings on long lines
```

### Git Configuration

For new repositories, configure git user locally:

```bash
git config --local user.name "your-username"
git config --local user.email "your-email@users.noreply.github.com"
```

### Release Process

1. Update VERSION file with new version (e.g., `1.0.0`)
2. Commit and push: `git commit -m "Release v1.0.0" && git push`
3. Create release: `gh release create v1.0.0 --generate-notes`
4. GitHub Actions automatically builds and attaches skill ZIP

See `docs/tasks/release/how-to-release.md` for detailed instructions.

## Important Files

- **SKILL.md** - Main skill file with three-level organization system
- **VERSION** - Current version (0.0.5)
- **README.md** - User-facing documentation and installation instructions
- **references/template.md** - Template for creating new CLI tool references
- **references/example-tool.md** - Example reference (fictional DataProc tool)
- **.markdownlint-cli2.jsonc** - Markdown linter config (MD013 disabled)
- **docs/tasks/release/how-to-release.md** - Release workflow documentation
- **docs/tasks/tests/how-to-test-skill.md** - Testing framework and test cases

## Skill Development Best Practices

### Three-Level Organization System

When working with CLI tools, options must be categorized into three levels:

**Level 1: Basic**
- Essential options for most common tasks
- Help, version, basic operations
- Simple flags with clear, single purposes
- Examples: `--help`, `--version`, `--output FILE`

**Level 2: Medium (Commonly Used)**
- Options used in typical workflows
- Configuration, formatting, filtering options
- Used regularly but not universally
- Examples: `--format FORMAT`, `--verbose`, `--config FILE`

**Level 3: Advanced (Complex Cases)**
- Specialized options for complex scenarios
- Performance tuning, debugging, edge cases
- Often require multiple parameters or complex syntax
- MUST include concrete usage examples
- Examples: `--parallel NUM`, `--memory-limit SIZE`, `--custom-function`

### Categorization Criteria

Organize options based on:
1. **Usage frequency indicators**: "common", "basic" keywords in help text
2. **Complexity**: Number of parameters, dependencies on other options
3. **Purpose keywords**: "debug", "advanced", "experimental" → Level 3
4. **Common sense**: What typical users need first vs. what specialists need

### Writing Style

- Use imperative/infinitive form (verb-first instructions) throughout SKILL.md
  - Good: "Run the script to process files"
  - Bad: "You should run the script" or "You can run the script"
- Keep SKILL.md focused and concise (<5k words)
- Move detailed documentation to `references/` files
- Provide real examples, not hypothetical ones

### Markdown File Size Constraints

**CRITICAL**: Each markdown file packaged in a skill must adhere to strict size limits:

- **Preferred**: Keep each `.md` file under 500 lines
- **Maximum**: More than 1000 lines is NOT ALLOWED (critical constraint)

This applies to all markdown files in the skill:
- SKILL.md
- files in `references/` directory
- documentation files in `docs/`

If content exceeds these limits:
- Split into multiple smaller files
- Move detailed content to separate reference files
- Use clear cross-references between files
- Consider using scripts for large data/schemas

### Bundled Resources Guidelines

#### When to include scripts/

- Code is repeatedly rewritten by Claude
- Deterministic behavior is critical
- Complex logic that shouldn't be regenerated

#### When to include references/

- Detailed schemas, API docs, policies
- Domain-specific knowledge
- Information that informs Claude's process
- For files >10k words, include grep patterns in SKILL.md

#### When to include assets/

- Templates, images, boilerplate
- Files that will be copied/modified in output
- NOT loaded into context, used in final deliverables

### Testing Approach

Follow the framework in `docs/tasks/tests/how-to-test-skill.md`:

1. Install skill locally
2. Test activation with various phrasings
3. Verify core functionality
4. Test error handling
5. Validate documentation accuracy

Create specific test cases for each skill feature with expected inputs/outputs.

## Common Workflows

### Adding New CLI Tool References

When creating new reference files in `references/`:

1. Use `template.md` as the starting point
2. Follow the three-level structure strictly
3. Include concrete examples for ALL Advanced options
4. Keep files under 500 lines (max 1000 lines)
5. Use clear, scannable headings
6. Note option interactions and warnings

### Updating Documentation

When updating README.md or other docs:
- Keep focus on the three-level organization system
- Emphasize the skill's value for proprietary/complex tools
- Maintain consistency with SKILL.md content
- Avoid duplicating content between files

### Testing the CLI Helper Skill

When testing the skill:

1. **Activation test**: Verify skill activates with queries like:
   - "What options does grep support?"
   - "Parse the help for ffmpeg"
   - "Show me kubectl parameters"

2. **Categorization test**: Ensure options are logically organized:
   - Basic options are truly essential
   - Medium options represent typical usage
   - Advanced options have concrete examples

3. **Reference quality test**: Check that references:
   - Follow the template structure
   - Include all required sections
   - Have clear, actionable examples
   - Stay under line limits

## Troubleshooting

### Skill Doesn't Activate

1. Verify SKILL.md has valid YAML frontmatter: `head -10 SKILL.md`
2. Check description is specific with trigger words
3. Try explicit request: "Use the [skill-name] skill to..."
4. Restart Claude Code (skills loaded on startup)

### GitHub Actions Release Fails

Common issues:

- VERSION file missing or empty
- SKILL.md missing YAML frontmatter
- Invalid frontmatter (missing `name` or `description`)

Check workflow logs: `gh run view --log`

### Reference File Quality Issues

1. Check that Advanced options have concrete examples
2. Verify options are categorized appropriately
3. Ensure files stay under 500 lines (max 1000)
4. Test that reference follows template.md structure

## Documentation Structure

```text
docs/
├── guides/              # Additional documentation (optional)
│   └── README.md
└── tasks/
    ├── release/
    │   └── how-to-release.md    # Release workflow
    └── tests/
        └── how-to-test-skill.md # Testing framework
```

## Version Numbering

Follow semantic versioning (MAJOR.MINOR.PATCH):

- `0.0.1` - Initial development
- `0.1.0` - First feature complete
- `1.0.0` - First stable release
- `1.1.0` - New feature (backward compatible)
- `1.1.1` - Bug fix
- `2.0.0` - Breaking change

## Skill Activation

The skill activates when users ask about:
- CLI tool options or parameters
- Command line help or flags
- How to use specific CLI commands
- Available options for a tool

Trigger phrases:
- "What options does [tool] have?"
- "Parse the help for [tool]"
- "Show me parameters for [command]"
- "How do I use [cli-tool]?"

## Common Pitfalls to Avoid

1. **Over-categorization**: Not every CLI tool needs Advanced section
2. **Missing examples**: Advanced options MUST have concrete examples
3. **Vague descriptions**: Each option should explain WHEN to use it, not just WHAT it does
4. **Copying help text verbatim**: Parse and organize, don't just copy
5. **Ignoring file size**: Keep references under 500 lines

## References

- [Claude Code Skills Documentation](https://docs.claude.com/en/docs/claude-code/skills)
- [Skill Authoring Best Practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices)

---

**Quick Reference**: This skill helps organize CLI tool documentation into Basic, Medium, and Advanced levels. Focus on practical categorization and concrete examples.
