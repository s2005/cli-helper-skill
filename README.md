# CLI Helper Skill

A Claude Code skill that helps you understand and work with command-line tools by organizing their help documentation into three structured levels of complexity.

## Overview

The CLI Helper Skill provides systematic guidance for working with command-line interface (CLI) tools by parsing and organizing their help documentation. It's particularly valuable for:

- **Proprietary or custom internal CLI tools** that aren't widely documented
- **Complex tools** with extensive options that are difficult to navigate
- **Rare or specialized CLI utilities** where parameter knowledge is limited
- **Any situation** where accurate CLI parameter information is critical

The skill organizes CLI help information into three levels of complexity (Basic, Medium, Advanced), making it easier to find the right options for any task.

## Features

- **Three-level organization system**: Categorizes CLI options by usage frequency and complexity
- **Systematic help parsing**: Extracts and structures information from `--help` output
- **Reference library**: Build a collection of pre-parsed CLI documentation for frequently-used tools
- **Smart categorization**: Automatically suggests appropriate complexity levels based on option characteristics
- **Example generation**: Creates concrete usage examples for advanced options

## Installation

### Using Claude Code

Copy the skill to your Claude Code skills directory:

```bash
# Windows (Git Bash)
cp -r cli-helper-skill "$USERPROFILE/.claude/skills/cli-helper"

# Unix/Mac
cp -r cli-helper-skill ~/.claude/skills/cli-helper
```

### From GitHub Release

1. Download the latest release ZIP from [Releases](https://github.com/s2005/cli-helper-skill/releases)
2. Extract to your Claude skills directory:

```bash
# Windows
unzip cli-helper-skill-v1.0.0.zip -d "$USERPROFILE/.claude/skills/"

# Unix/Mac
unzip cli-helper-skill-v1.0.0.zip -d ~/.claude/skills/
```

3. Restart Claude Code

## Usage

### Basic Usage

Simply ask Claude about a CLI tool:

```
"What options are available for ffmpeg?"
"How do I use the dataproc command?"
"Show me the parameters for kubectl get"
```

Claude will automatically:
1. Check for existing reference documentation
2. Execute the tool's help command if needed
3. Parse and organize the options into three levels
4. Present the structured information

### Three Complexity Levels

**Level 1: Basic** - Essential options for common tasks
- Help, version, basic operations
- Simple flags with clear purposes
- Minimal dependencies on other options

**Level 2: Medium (Commonly Used)** - Options for typical workflows
- Configuration and customization options
- Formatting and filtering
- Regular but not universal usage

**Level 3: Advanced** - Specialized options for complex scenarios
- Performance tuning parameters
- Advanced filtering and transformations
- Edge cases and specialized features
- Always includes concrete usage examples

### Creating Reference Files

For frequently-used tools, you can create reference files:

1. Ask Claude to parse a tool's help output
2. Request to save it: "Save this to references/ for future use"
3. Claude will create a structured markdown file in `references/`

You can also manually create reference files following the template in `references/template.md`.

### Working with Proprietary Tools

For internal or proprietary tools:

1. Ensure the tool is accessible in your environment
2. Ask Claude about the tool (it will execute `--help`)
3. Optionally save the parsed output to `references/` for faster future access

## Examples

### Example 1: Quick lookup

```
User: "What are the basic options for grep?"

Claude: # grep - Search for patterns in files

## Basic Options
- `-h, --help` - Display help information
- `--version` - Show version number
- `-i, --ignore-case` - Case insensitive matching
- `-r, --recursive` - Search directories recursively
- `-n, --line-number` - Show line numbers

## Medium Options (Commonly Used)
[continues with organized output...]
```

### Example 2: Creating a reference

```
User: "Parse the help for our internal 'dataproc' tool and save it to references"

Claude: [Executes dataproc --help, parses output, creates references/dataproc.md]

I've created references/dataproc.md with organized documentation for the dataproc tool.
The file includes:
- 8 basic options for common operations
- 12 medium-level options for typical workflows
- 10 advanced options with performance tuning
- Usage examples for complex scenarios
```

### Example 3: Finding the right option

```
User: "I need to process a large file with dataproc. What options should I use?"

Claude: For large file processing with dataproc, I recommend these options:

**From Medium level:**
- `--chunk-size SIZE` - Process in chunks to manage memory
- `--log-level info` - Monitor progress

**From Advanced level:**
- `--parallel NUM` - Enable parallel processing
  Example: `dataproc -i large.csv --parallel 8 --chunk-size 100M -o output.csv`
- `--memory-limit SIZE` - Prevent out-of-memory errors
  Example: `dataproc -i large.csv --memory-limit 4G --chunk-size 50M`

[provides additional context and recommendations]
```

## Repository Structure

```
cli-helper-skill/
├── SKILL.md                    # Main skill file with instructions
├── VERSION                     # Version number (0.0.1)
├── README.md                   # This file
├── references/                 # Pre-parsed CLI documentation
│   ├── template.md             # Template for creating new references
│   └── example-tool.md         # Example reference (fictional DataProc tool)
├── scripts/                    # (Currently empty - no scripts needed)
├── assets/                     # (Currently empty - no assets needed)
├── examples/                   # Example usage scenarios
│   └── README.md
└── docs/
    ├── tasks/
    │   ├── release/
    │   │   └── how-to-release.md
    │   └── tests/
    │       └── how-to-test-skill.md
    └── guides/
        └── README.md
```

## How It Works

1. **Check for existing references**: The skill first searches `references/` for pre-parsed documentation
2. **Execute help command**: If no reference exists, executes the tool's help command (`--help`, `-h`, `help`, or `man`)
3. **Parse and categorize**: Analyzes the output and organizes options into three complexity levels based on:
   - Usage frequency indicators in help text
   - Complexity (number of parameters, dependencies)
   - Purpose keywords (debug, advanced, experimental, etc.)
4. **Present structured information**: Displays the organized options with descriptions and examples
5. **Optional reference creation**: Can save parsed documentation for future use

## Contributing Reference Files

You can contribute reference files for common tools:

1. Use the template in `references/template.md`
2. Follow the three-level organization system
3. Include concrete examples for advanced options
4. Submit a pull request

## Best Practices

### When Creating References

- **Be objective**: Base categorization on typical usage patterns
- **Provide context**: Explain what options do and when to use them
- **Include examples**: Advanced options should always have concrete examples
- **Note interactions**: Mention when options work together or conflict
- **Warn about dangers**: Clearly mark destructive operations

### Markdown File Size

Keep reference files under 1000 lines (preferably under 500):
- Split very large tools into multiple reference files if needed
- Focus on most commonly-used options
- Link to official documentation for exhaustive details

## Limitations

- Requires the CLI tool to be installed and accessible
- Help text formats vary widely; some tools may need manual interpretation
- Some proprietary tools may have limited or poorly formatted help output
- Man pages provide more detail but may not always be available

## Version History

See [CHANGELOG.md](CHANGELOG.md) for version history and release notes.

## License

MIT License - See [LICENSE](LICENSE) file

## Support

- **Issues**: [GitHub Issues](https://github.com/s2005/cli-helper-skill/issues)
- **Discussions**: [GitHub Discussions](https://github.com/s2005/cli-helper-skill/discussions)
- **Documentation**: See SKILL.md for detailed usage instructions

## Acknowledgments

This skill follows best practices from:
- Claude Code official documentation
- Anthropic's skill-creator guidelines
- Community feedback on CLI tool documentation

---

**Quick Start**: Copy this skill to `~/.claude/skills/cli-helper` and ask Claude "What options does [your-cli-tool] support?"
