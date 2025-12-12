# RegiSci: Registry of Scientific Instances

**A structured, type-safe, open registry for scientific data provenance, reproducibility, and interoperability**

---

Reproducibility requires knowing what happened, when, how, and with what. Yet most laboratories still track experiments in spreadsheets and paper notebooks. Standards like RO-Crate, W3C PROV, and ISA-Tab serve archival purposes well, but they assume finished work, semantic web infrastructure, and expertise foreign to working scientists.

RegiSci takes a different approach: markdown files, UUIDv8 identifiers, and Git workflows. Human-readable records. Meaningful diffs. Offline creation without central coordination. Provenance captured as work happens, not reconstructed afterward.

## The Problem

Current provenance standards optimize for the wrong moment. RO-Crate packages completed research beautifully but requires JSON-LD fluency. W3C PROV offers rigorous semantics but demands triple stores and SPARQL endpoints. ISA-Tab works for repository submissions but fights against version control. None were designed for real-time capture during active research.

A postdoc logging yesterday's gel results shouldn't need to deploy RDF infrastructure. A confocal microscope mid-experiment can't generate RO-Crate metadata. Scientists need provenance tools that work the way they already work.

## The Solution

RegiSci defines four instance classes that describe any scientific activity:

| Class | Purpose | Examples |
|-------|---------|----------|
| **Object** | Things that exist or result from work | Samples, datasets, trained models, reagent batches |
| **Instrument** | Tools that produce or modify objects | Microscopes, sequencers, pipetting robots, software |
| **Method** | How something is done | Protocols, algorithms, parameter configurations |
| **Workflow** | Execution records linking everything | Input objects → method + instrument → output objects |

Every instance validates against a versioned type schema. Types are governed through community review. Instance creation is completely open.

## Core Design Principles

**Markdown for the Long Haul** Instance files are plain markdown, readable on any computer from any era. Git diffs show meaningful scientific changes. No proprietary software required.

**Distributed Creation** UUIDv8 identifiers let anyone generate globally unique IDs offline. Field researchers, BSL-3 labs, air-gapped clusters: all create valid instances independently.

**Governance Where It Matters** Type schemas undergo strict review in [regisci-types](https://github.com/RegiSci/regisci-types). Once released, a type definition is immutable. But any scientist, instrument, or pipeline can generate instances freely.

**Built for Operation** Instruments and analysis software generate instances during work, capturing exact parameters, timestamps, and lineage in real time.

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| [RegiSci-guidelines](https://github.com/RegiSci/regisci-guidelines) | Architecture, specifications, and documentation |  Private (development) |
| [RegiSci-types](https://github.com/RegiSci/regisci-types) | Community-governed type schemas |  Private (development) |
| [RegiSci-API](https://github.com/RegiSci/regisci-api) | Python reference implementation and CLI |  Private (development) |

All repositories will be made public upon initial release.

## Quick Example

A workflow instance connecting sample preparation to processed output:

```yaml
---
uuid: "019abc12-3def-8180-b012-3456789abcde"
created: "2025-12-10T14:32:00Z"
created_by:
  orcid: 0000-0002-1234-5678

inputs:
  - "019abc12-1111-8000-a000-000000000001"  # Raw micrograph stack
  
method: "019abc12-2222-8002-a000-000000000002"      # Motion correction parameters
instrument: "019abc12-3333-8001-a000-000000000003"  # MotionCor2 v1.6.4

outputs:
  - "019abc12-4444-8000-a000-000000000004"  # Corrected micrograph

started_at: "2025-12-10T14:30:00Z"
completed_at: "2025-12-10T14:32:00Z"
status: "completed"
---

# Motion Correction Run

Dose weighting applied. 5x5 patch alignment with 150 iterations.
Output shows reduced beam-induced motion artifacts.
```

The workflow links to typed object, method, and instrument instances. Each has its own file with full metadata. Together they form a complete provenance chain.

## Origins

RegiSci builds on [TOMOMAN](https://github.com/wan-lab-vanderbilt/TOMOMAN), which established structured metadata workflows for cryo-electron tomography. TOMOMAN's "minimal project" format enabled exact reconstruction of preprocessing states across 35TB of community datasets deposited to EMPIAR, including the 1,829-tomogram [EMPIAR-11830](https://www.ebi.ac.uk/empiar/EMPIAR-11830/) dataset that the CZ Imaging Institute portal directly ingested for automated analysis.

This demonstrated that structured metadata enables automated workflows across institutions. RegiSci extends these patterns to all scientific domains.

## Roadmap

**Current Phase: Core Development**
- UUIDv8 generation and validation
- Markdown schema validation engine  
- Python reference implementation
- Initial type schemas for cryo-EM/ET workflows

**Next: Integration & Community**
- Instrument adapters (microscopy formats first)
- Migration tools from Excel, ISA-Tab, TOMOMAN
- Export bridges to RO-Crate and W3C PROV
- Documentation and tutorials

**Future: Ecosystem Growth**
- Web-based instance creation and browsing
- Federated registry support
- Provenance graph visualization

## Playing Well With Others

RegiSci is not replacing RO-Crate, PROV, or ISA-Tab. It's the layer where scientists actually work (Git-native, markdown-based, offline-capable) with bridges to formal publication and archival systems when needed.

## Get Involved

RegiSci is in active early development. We welcome:

- **Domain experts** interested in defining type schemas for their field
- **Instrument developers** looking to integrate structured provenance
- **Software tool builders** who want to emit or consume RegiSci instances

Contact: @cryosagar

## License

MIT License (pending final decision)

---

*RegiSci*

