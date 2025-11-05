# Changelog

All notable changes to the CLI Helper Skill will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.0.10] - 2025-11-05

### Fixed
- Fixed skill name validation error by changing name from 'CLI Helper' to 'cli-helper' (lowercase with hyphens only)

## [0.0.9] - 2024-11-05

### Added
- Initial skill setup with three-level organization system
- SKILL.md with comprehensive workflow for parsing CLI help
- Reference template (template.md) for creating CLI tool documentation
- Example reference (example-tool.md) demonstrating DataProc fictional tool
- Comprehensive README with usage examples
- Examples directory with usage scenarios
- GitHub Actions workflow for automated releases

### Changed
- Customized from template repository to cli-helper specific skill

## [0.0.5] - 2024-11-05

### Added
- Repository initialized from claude-code-skill-template
- Core skill structure established
- Three-level organization system defined (Basic, Medium, Advanced)
- Workflow for parsing and categorizing CLI tool options

### Notes
- Development version
- Not yet ready for production use
- Building toward 1.0.0 release

## Version History

- **0.0.5** - Current development version
- **1.0.0** (planned) - First stable release with complete documentation and tested workflow

## Upcoming Features

Consider for future releases:
- Pre-built references for common CLI tools (grep, find, ffmpeg, kubectl, docker)
- Scripts for automated help parsing (if pattern emerges)
- Extended examples for complex tool categories
- Integration with man page parsing
