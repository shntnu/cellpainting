# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the nf-core/cellpainting pipeline - a Nextflow-based bioinformatics pipeline for processing cell painting data. The pipeline is built using the nf-core framework and follows DSL2 syntax.

## Development Commands

### Running the Pipeline

```bash
# Basic run with test profile
nextflow run main.nf -profile test

# Run with Docker/Singularity
nextflow run main.nf -profile docker --input samplesheet.csv --outdir results

# Run with specific container engines
nextflow run main.nf -profile singularity --input samplesheet.csv --outdir results
nextflow run main.nf -profile conda --input samplesheet.csv --outdir results
```

### Testing

```bash
# Run nf-test for module/workflow testing
nf-test test modules/local/cytotable/tests/main.nf.test
nf-test test modules/local/cellprofiler/illuminationcorrection/tests/main.nf.test

# Run all tests
nf-test test
```

### Linting and Code Quality

```bash
# Run nf-core linting (checks pipeline structure and standards)
nf-core lint

# Check Nextflow syntax
nextflow run main.nf -profile test --validate_params false -stub
```

## Architecture Overview

### Main Components

1. **Entry Point**: `main.nf` - Contains the main workflow orchestration

   - Imports the CELLPAINTING workflow from `workflows/cellpainting.nf`
   - Handles pipeline initialization and completion

2. **Workflows**: Located in `workflows/`

   - `cellpainting.nf`: Main workflow logic for the cell painting pipeline

3. **Modules**: Located in `modules/`

   - `local/cytotable/`: Converts CellProfiler output to Parquet format
   - `local/cellprofiler/illuminationcorrection/`: Performs illumination correction using CellProfiler
   - `nf-core/multiqc/`: Standard nf-core module for generating MultiQC reports

4. **Configuration**:
   - `nextflow.config`: Main configuration file with profiles and parameters
   - `conf/base.config`: Base configuration for resources
   - `conf/modules.config`: Module-specific configuration
   - `conf/test.config`: Test profile configuration
   - `nextflow_schema.json`: Parameter validation schema

### Key Pipeline Features

- **Container Support**: Supports Docker, Singularity, Conda, and other container engines
- **nf-schema Plugin**: Uses nf-schema v2.2.0 for parameter validation
- **Wave Integration**: Supports Wave containers for dependency management
- **MultiQC Integration**: Generates comprehensive QC reports (currently commented out in workflow)

### Current Pipeline State

The pipeline is in early development (v1.0.0dev). Key modules implemented:

- Illumination correction using CellProfiler
- Data conversion using Cytotable
- Basic workflow structure following nf-core standards

The MultiQC reporting is currently commented out but framework is in place.

## Important Notes

- The pipeline follows nf-core standards and conventions
- Uses DSL2 syntax (requires Nextflow >=24.04.2)
- Test data is available through nf-core test datasets
- Pipeline is designed for cell painting image analysis workflows
