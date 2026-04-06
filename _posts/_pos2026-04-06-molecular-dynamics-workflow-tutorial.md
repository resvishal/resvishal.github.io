---
layout: post
title: "A Beginner's Guide to Molecular Dynamics: From PDB to Analysis"
date: 2026-04-05
description: "Complete workflow for protein-ligand MD simulations using GROMACS"
tags: [molecular-dynamics, gromacs, tutorial, drug-discovery]
categories: [tutorials]
featured: true  # This will show as featured post
thumbnail: /assets/img/md-tutorial-cover.jpg  # Optional: add a cover image
---

&gt; **Target audience:** Computational biologists new to MD  
&gt; **Software:** GROMACS, PyMOL, VMD  
&gt; **Time required:** ~3-4 hours (depending on system size)

---

## Overview

Molecular Dynamics (MD) simulations let us watch proteins dance in slow motion. We see how they breathe, how they bind drugs, where they hide their secrets.

This tutorial walks through my standard workflow for **protein-ligand systems** — the same approach I use for TB drug discovery at CSIR-IHBT.

---

## Step 0: What You Need

| Component | Purpose |
|-----------|---------|
| Protein structure (PDB) | Starting coordinates |
| Ligand structure (SDF/MOL2) | Drug molecule |
| Force field | Parameters for atoms (CHARMM36, OPLS-AA, Amber) |
| Water model | Solvation (TIP3P, SPC/E) |
| Ions | Neutralize system |

---

## Step 1: Prepare the Protein

### 1.1 Download from PDB
Go to [RCSB PDB](https://www.rcsb.org/), search your protein. Download the `.pdb` file.

### 1.2 Clean the Structure
Remove:
- Water molecules (unless they're structurally important)
- Ligands (we'll add our own)
- Alternative conformations (keep chain A usually)

**PyMOL commands:**
```bash
# In PyMOL
fetch 1ABC          # Download PDB
remove solvent      # Delete waters
remove organic      # Delete ligands
save protein_clean.pdb, all
