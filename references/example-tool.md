# DataProc CLI Reference

**Brief Description:** DataProc is a proprietary data processing tool for ETL operations, data transformation, and validation workflows. It processes structured data files and applies configurable transformation pipelines.

**Installation/Access:** Available on internal company network. Access via `dataproc` command after loading the data-tools module.

---

## Basic Options

Essential options for common data processing tasks.

### `--help`, `-h`
Display help information showing all available commands and options.

**Usage:**
```bash
dataproc --help
```

### `--version`
Show version information including build number and release date.

**Usage:**
```bash
dataproc --version
```

### `--input FILE`, `-i FILE`
Specify input data file to process. Required for most operations.

**Supported formats:** CSV, JSON, XML, Parquet

**Usage:**
```bash
dataproc -i data.csv
```

### `--output FILE`, `-o FILE`
Specify output file path. If not provided, outputs to stdout.

**Usage:**
```bash
dataproc -i data.csv -o processed.csv
```

### `--validate`
Validate input data against schema without processing. Useful for quick checks.

**Usage:**
```bash
dataproc --validate -i data.csv
```

---

## Medium Options (Commonly Used)

Options used in typical data processing workflows.

### `--format FORMAT`, `-f FORMAT`
Specify output format for processed data.

**Available formats:** csv, json, xml, parquet, avro

**Usage:**
```bash
dataproc -i data.csv --format json -o output.json
```

### `--schema FILE`, `-s FILE`
Use custom schema file for validation and type inference.

**Usage:**
```bash
dataproc -i data.csv --schema company-schema.json -o validated.csv
```

### `--filter EXPRESSION`
Apply filter expression to select rows. Uses SQL-like syntax.

**Usage:**
```bash
dataproc -i sales.csv --filter "amount > 1000 AND region = 'EMEA'" -o filtered.csv
```

### `--transform CONFIG`
Apply transformation pipeline defined in configuration file.

**Usage:**
```bash
dataproc -i raw-data.csv --transform etl-pipeline.yaml -o transformed.csv
```

### `--log-level LEVEL`
Set logging verbosity.

**Levels:** error, warn, info, debug

**Usage:**
```bash
dataproc -i data.csv --log-level debug
```

### `--dry-run`
Preview operations without writing output files. Shows what would be processed.

**Usage:**
```bash
dataproc -i data.csv --transform pipeline.yaml --dry-run
```

### `--ignore-errors`
Continue processing when encountering non-critical errors in data.

**Usage:**
```bash
dataproc -i messy-data.csv --ignore-errors -o cleaned.csv
```

---

## Advanced Options

Complex options for specialized use cases and performance optimization.

### `--parallel NUM`
Enable parallel processing with specified number of worker threads.

**Default:** Single-threaded processing

**Usage:**
```bash
dataproc -i large-dataset.csv --parallel 8 -o processed.csv
```

**Notes:**
- Recommended for files larger than 100MB
- Memory usage scales with thread count
- Best results with NUM equal to CPU core count

### `--chunk-size BYTES`
Set chunk size for streaming large files.

**Default:** 10MB

**Usage:**
```bash
dataproc -i huge-file.csv --chunk-size 50M --parallel 4 -o output.csv
```

**Notes:**
- Larger chunks reduce I/O overhead but increase memory usage
- Use with --parallel for optimal performance on large files
- Accepts suffixes: K (kilobytes), M (megabytes), G (gigabytes)

### `--cache-dir PATH`
Specify directory for intermediate cache files during multi-stage processing.

**Default:** System temp directory

**Usage:**
```bash
dataproc -i data.csv --transform complex-pipeline.yaml --cache-dir /fast-ssd/cache -o final.csv
```

**Notes:**
- Recommended to use fast storage (SSD) for cache directory
- Cache is automatically cleaned after successful processing
- Use --keep-cache to retain for debugging

### `--keep-cache`
Retain cache files after processing completes for debugging purposes.

**Usage:**
```bash
dataproc -i data.csv --transform pipeline.yaml --cache-dir ./debug-cache --keep-cache
```

**Notes:**
- Useful for debugging transformation pipelines
- Remember to manually clean cache directory
- Cache can consume significant disk space

### `--profile`
Enable performance profiling with detailed timing metrics.

**Usage:**
```bash
dataproc -i data.csv --transform pipeline.yaml --profile -o output.csv
```

**Output:** Creates profiling report in `dataproc-profile-<timestamp>.json`

**Notes:**
- Adds minimal overhead (typically less than 5%)
- Profile report includes per-stage timing and memory usage
- Use to identify bottlenecks in complex pipelines

### `--custom-function MODULE:FUNCTION`
Load and apply custom transformation function from Python module.

**Usage:**
```bash
dataproc -i data.csv --custom-function mymodule:clean_addresses -o cleaned.csv
```

**Notes:**
- Module must be in Python path or current directory
- Function signature: `def function(dataframe) -> dataframe`
- Can be combined with --transform for complex pipelines

### `--memory-limit SIZE`
Set maximum memory usage limit for processing operations.

**Default:** 80% of available system memory

**Usage:**
```bash
dataproc -i huge-file.csv --memory-limit 4G --chunk-size 20M -o output.csv
```

**Notes:**
- Forces streaming mode if file exceeds limit
- Accepts suffixes: M (megabytes), G (gigabytes)
- Processing may be slower with strict limits

### `--sql QUERY`
Execute SQL query directly on input data file.

**Usage:**
```bash
dataproc -i sales.csv --sql "SELECT region, SUM(amount) FROM data GROUP BY region" -o summary.csv
```

**Notes:**
- Input data is available as table named "data"
- Supports most standard SQL syntax (SELECT, WHERE, GROUP BY, JOIN)
- For complex queries, consider using --transform with SQL transformation stage

---

## Common Usage Examples

### Example 1: Basic data validation
```bash
dataproc --validate -i daily-sales.csv --schema sales-schema.json
```
Validates the daily sales file against the company schema without processing.

### Example 2: Format conversion with filtering
```bash
dataproc -i sales.csv --filter "amount > 5000" --format json -o high-value-sales.json
```
Converts CSV to JSON while filtering for high-value transactions.

### Example 3: ETL pipeline processing
```bash
dataproc -i raw-data.csv --transform etl-pipeline.yaml --schema target-schema.json --log-level info -o processed.parquet
```
Processes raw data through a transformation pipeline, validates against schema, and outputs as Parquet.

### Example 4: High-performance processing of large files
```bash
dataproc -i huge-dataset.csv --parallel 16 --chunk-size 100M --memory-limit 8G --cache-dir /fast-ssd/cache --format parquet -o optimized.parquet
```
Optimized processing of very large files using parallel processing, chunking, and SSD caching.

### Example 5: Custom transformation with profiling
```bash
dataproc -i data.csv --custom-function transforms:clean_and_dedupe --transform enrichment.yaml --profile -o final.csv
```
Applies custom Python function, runs enrichment pipeline, and profiles performance.

---

## Important Notes

- **Memory considerations:** Files larger than 1GB should use --chunk-size and --memory-limit options
- **Schema validation:** Always validate against schema in production workflows using --schema option
- **Error handling:** Use --ignore-errors cautiously; it may skip critical data quality issues
- **Transformation pipelines:** Complex pipelines can be tested with --dry-run before execution
- **Performance:** For files over 500MB, use --parallel with NUM equal to CPU core count
- **Custom functions:** Must be thread-safe if using --parallel option

---

## Common Error Messages

### "Schema validation failed: Missing required field 'customer_id'"
Input data is missing a required field. Check schema definition and input file structure.

### "Memory limit exceeded during processing"
File is too large for available memory. Use --chunk-size and --memory-limit options, or increase system memory.

### "Cannot parse input file: Invalid CSV format at line 1234"
Input file has formatting errors. Use --ignore-errors to skip problematic rows, or fix source data.

---

## Related Commands

- `dataproc-schema` - Tool for creating and validating schema definitions
- `dataproc-monitor` - Monitor running dataproc jobs and view processing statistics
- `dataproc-convert` - Quick format conversion utility (subset of dataproc functionality)
