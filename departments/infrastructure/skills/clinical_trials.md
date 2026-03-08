---
title: Clinical Trials
department: infrastructure
version: 1.0
triggers: [clinical trial, NCT, phase, modality, CAR-T, cell therapy]
---

# Clinical Trial Intelligence

Track and analyze clinical trials in cell & gene therapy.

## Database Tables (Transfer DB — synced from Hub)

| Table | Purpose |
|-------|---------|
| `clinical_trials` | Trial records with NCT ID |
| `clinical_trial_sponsors` | Sponsor companies |

## Modalities Tracked

Cell Therapy, MSC, CAR-T, CAR-NK, Gene Therapy, Stem Cell, AAV, TCR-T, Exosome, iPSC

## Data Source

- ClinicalTrials.gov API v2

## App Page

- `/clinical-trials` — Trial search and analytics

## MADE AI Module

- Clinical Trial Intelligence System
