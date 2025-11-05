# CLI Helper Skill Guides

This directory is reserved for additional documentation and guides specific to the CLI Helper skill.

## Purpose

Guides can provide:
- Extended examples of organizing specific CLI tools
- Advanced techniques for categorizing complex options
- Tips for working with different types of CLI tools
- Troubleshooting common parsing challenges

## Potential Guides

### Tool-Specific Guides

For commonly-requested CLI tools that benefit from detailed guidance:

- `ffmpeg-guide.md` - Organizing ffmpeg's extensive options
- `kubectl-guide.md` - Kubernetes CLI tool reference
- `docker-guide.md` - Docker CLI command organization

### Technique Guides

- `parsing-strategies.md` - Strategies for parsing different help output formats
- `categorization-tips.md` - Tips for deciding between Basic/Medium/Advanced levels
- `dealing-with-manpages.md` - How to work with man page output vs --help

## Current Status

This directory is currently empty but reserved for future guides as the skill evolves and common use cases emerge.

## Contributing Guides

If you create guides for specific CLI tools or techniques:

1. Follow the three-level organization system (Basic, Medium, Advanced)
2. Include concrete examples from real help output
3. Keep each guide focused on a single tool or technique
4. Reference the guide from SKILL.md if it becomes essential
5. Ensure guides stay under 500 lines (max 1000)

## Guide Template

When creating a new guide:

```markdown
# [Tool Name] CLI Guide

Brief description of the tool and why it benefits from this guide.

## Tool Overview

- What the tool does
- Why organizing its options is valuable
- Common use cases

## Basic Options

List and explain basic options with examples.

## Medium Options (Commonly Used)

List and explain medium options with usage scenarios.

## Advanced Options

List advanced options with concrete usage examples.

## Common Workflows

Show how to combine options for typical tasks.

## Related Resources

- Official documentation links
- Related tools or guides
```

## Notes

- Guides are optional but can be valuable for complex CLI tools
- Focus on tools that users frequently ask about
- Keep content practical and example-driven
- Update guides as tools evolve
