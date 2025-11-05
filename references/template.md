# [Tool Name] CLI Reference

**Brief Description:** One or two sentences describing what this tool does.

**Installation/Access:** (Optional) How to install or access this tool if relevant.

---

## Basic Options

Essential options for common tasks. These are the first options users should know.

### `--help`, `-h`
Display help information.

**Usage:**
```bash
toolname --help
```

### `--version`, `-v`
Show version information.

**Usage:**
```bash
toolname --version
```

### `--output FILE`, `-o FILE`
Specify output file path.

**Usage:**
```bash
toolname -o results.txt
```

### `[Add other basic options here]`
- Use the full syntax (short and long forms)
- Keep descriptions brief
- Include simple usage example

---

## Medium Options (Commonly Used)

Options used in typical workflows for configuration and customization.

### `--format FORMAT`, `-f FORMAT`
Specify output format.

**Available formats:** json, xml, csv, text

**Usage:**
```bash
toolname --format json -o output.json
```

### `--verbose`, `-v`
Enable verbose output for detailed information.

**Usage:**
```bash
toolname --verbose
```

### `--config FILE`, `-c FILE`
Use custom configuration file.

**Usage:**
```bash
toolname --config /path/to/config.yaml
```

### `[Add other medium-level options here]`
- Include information about typical usage scenarios
- Explain what problems these options solve
- Show how options work together

---

## Advanced Options

Complex options for specialized use cases, performance tuning, and debugging.

### `--threads NUM`
Set number of worker threads for parallel processing.

**Default:** Auto-detect CPU cores

**Usage:**
```bash
toolname --threads 8 --input large-dataset.dat
```

**Notes:**
- Higher thread counts may increase memory usage
- Optimal value depends on system resources and workload

### `--debug-level LEVEL`
Set debugging verbosity level.

**Levels:** 0 (none), 1 (errors), 2 (warnings), 3 (info), 4 (debug), 5 (trace)

**Usage:**
```bash
toolname --debug-level 4 --log-file debug.log
```

**Notes:**
- Higher levels significantly increase output volume
- Use with --log-file to avoid console spam

### `[Add other advanced options here]`
- Always include concrete examples showing real usage
- Explain performance implications where relevant
- Note any interactions with other options
- Warn about potentially dangerous operations

---

## Common Usage Examples

### Example 1: Basic operation
```bash
toolname --input data.txt --output results.txt
```
Description of what this does.

### Example 2: Common workflow
```bash
toolname --input data.txt --format json --verbose -o results.json
```
Description of this more complex workflow.

### Example 3: Advanced usage
```bash
toolname --input large-data.txt --threads 16 --memory-limit 8G --format binary -o optimized.bin
```
Description of this advanced scenario.

---

## Important Notes

- **[Note 1]:** Special behavior or gotcha to be aware of
- **[Note 2]:** Compatibility considerations
- **[Note 3]:** Common pitfalls or error messages

---

## Related Commands

- `related-tool` - Brief description of how it relates
- `another-tool` - Brief description of complementary functionality
