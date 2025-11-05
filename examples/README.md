# CLI Helper Examples

This directory contains example usage scenarios and sample CLI tool help outputs that demonstrate the CLI Helper skill in action.

## Purpose

These examples show how the CLI Helper skill:
- Parses real CLI tool help output
- Organizes options into three complexity levels
- Creates structured documentation from unstructured help text

## Example Conversations

### Example 1: Parsing a Simple CLI Tool

**User:** "What options are available for the grep command?"

**Claude (using CLI Helper skill):**
```
Let me check if there's a reference file for grep...

I'll execute `grep --help` to get the available options.

# grep - Search for patterns in files

## Basic Options
- `-h, --help` - Display help information
- `--version` - Show version number
- `-i, --ignore-case` - Case insensitive pattern matching
- `-n, --line-number` - Prefix output with line numbers
- `-r, --recursive` - Read all files under each directory recursively

## Medium Options (Commonly Used)
- `-v, --invert-match` - Select non-matching lines
- `-c, --count` - Print count of matching lines instead of normal output
- `-l, --files-with-matches` - Print only names of files with matches
- `-o, --only-matching` - Print only matched parts of matching lines
- `-A NUM, --after-context=NUM` - Print NUM lines of trailing context
- `-B NUM, --before-context=NUM` - Print NUM lines of leading context
- `-C NUM, --context=NUM` - Print NUM lines of output context

## Advanced Options
- `-P, --perl-regexp` - Interpret pattern as a Perl regular expression
  Example: `grep -P '(?<=@)\w+' emails.txt` (match domain names in emails)
- `--color=WHEN` - Use markers to highlight matching strings
  Example: `grep --color=always "error" logfile.txt | less -R`
- `-z, --null-data` - Treat input as null-separated records
  Example: `find . -print0 | grep -z pattern`
```

### Example 2: Understanding a Complex Proprietary Tool

**User:** "Parse the help output for our internal 'dataproc' tool"

**Claude (using CLI Helper skill):**
```
I'll execute `dataproc --help` and organize the options...

[Creates the structured documentation found in references/example-tool.md]

I've organized the dataproc tool documentation into:
- 5 basic options for common operations
- 7 medium-level options for typical workflows
- 8 advanced options for performance tuning and specialized use cases

Would you like me to save this to references/dataproc.md for faster access in the future?
```

### Example 3: Finding the Right Option

**User:** "I need to process a 5GB CSV file with dataproc. What options should I use?"

**Claude (using CLI Helper skill):**
```
For processing a 5GB file with dataproc, I recommend combining these options:

**Essential (from Basic):**
- `--input FILE, -i FILE` - Specify your input file
- `--output FILE, -o FILE` - Specify output destination

**Performance (from Medium):**
- `--format parquet` - More efficient than CSV for large datasets

**Optimization (from Advanced):**
- `--parallel NUM` - Enable parallel processing
  Example: `dataproc -i large.csv --parallel 8 -o output.parquet`

- `--chunk-size BYTES` - Process in chunks to manage memory
  Example: `dataproc -i large.csv --chunk-size 100M --parallel 8 -o output.parquet`

- `--memory-limit SIZE` - Prevent out-of-memory errors
  Example: `dataproc -i large.csv --memory-limit 6G --chunk-size 100M --parallel 8 -o output.parquet`

Complete recommended command:
```bash
dataproc -i large-file.csv \
  --parallel 8 \
  --chunk-size 100M \
  --memory-limit 6G \
  --format parquet \
  -o processed.parquet
```

This configuration will:
- Process the file in manageable 100MB chunks
- Use 8 parallel threads (adjust based on your CPU cores)
- Stay within 6GB memory limit
- Output to efficient Parquet format
```

## Creating Your Own Examples

When documenting CLI tools with this skill:

1. **Start with help command**: Let Claude execute `toolname --help`
2. **Review the organization**: Check that options are categorized appropriately
3. **Refine if needed**: Ask Claude to move options between levels if needed
4. **Save for reuse**: Request to save to references/ for future access

## Tips for Using the Skill

- **Be specific**: "Parse ffmpeg help" is clearer than "help with ffmpeg"
- **Save frequently-used tools**: Build up your references/ library over time
- **Focus on your needs**: When creating references, emphasize options relevant to your workflows
- **Provide context**: If looking for specific functionality, mention your goal (e.g., "I need to process large files")

## Contributing Examples

If you have examples of the CLI Helper skill working well with specific tools, consider:

1. Creating a reference file in `references/`
2. Adding a usage example in this directory
3. Sharing via pull request to help others

## Example Files Structure

Future examples might be organized as:

```
examples/
├── README.md                    # This file
├── simple-tools/               # Simple CLI tools (grep, find, etc.)
│   └── grep-example.md
├── complex-tools/              # Complex tools with many options
│   └── ffmpeg-example.md
└── proprietary-tools/          # Company-specific tools
    └── dataproc-example.md     # Example already in references/
```

## Notes

- Examples should demonstrate real-world usage scenarios
- Focus on tools that benefit from structured organization
- Keep examples concise and practical
- Update examples if CLI tools change significantly
