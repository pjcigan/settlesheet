# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project attempts to adhere to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-07-19
- Improved CLI: Added argparse-based command-line interface for spreadsheet generation.
- Default exchange rates: Uses 5-year average USD rates for select common currencies if native currency is USD and no rates are specified; otherwise defaults to 1.0.
- CLI warnings/info messages clarify when defaults are used.
- Packaging fix: Renamed main module to `settlesheet.py` (lowercase) and updated entry point for pip install compatibility.
- Removed unnecessary root __init__.py.
- Updated version to 1.1.

## [1.0.0] - 2025-06-19

### Added
- Generate group expense spreadsheets for Excel/LibreOffice/Google Sheets with automatic calculations
- Support for multiple participants and customizable names
- Multi-currency support with user-defined exchange rates
- Optimized settlements to minimize the number of transactions
- Direct settlements matrix for full transparency and double-checking
- Six color themes and customizable backgrounds
- Smart formulas for real-time updates and subgroup splits
- No installation required for templates; script can generate custom sheets
- Compatible with Excel, Google Sheets, LibreOffice

### Technical Details
- Script-based: no installation required for templates, but can be installed as a script for custom generation
- Requires Python 3.7 or later and the `openpyxl` library for new sheet generation
- Compatible with Excel, Google Sheets, and LibreOffice (xlsx format)
- No external web dependencies; all calculations/formulas are handled in the generated spreadsheet

[1.0.0]: https://github.com/pjcigan/settlesheet/releases/tag/v1.0.0
