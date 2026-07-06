# Molecular Docking Study of Antibiotic Adjuvant Candidates Against Bacterial Resistance Targets

**A virtual screening study evaluating repurposed drug candidates against three serine beta-lactamase structures and the AcrB RND efflux pump from *E. coli*, benchmarked against ceftriaxone as a structural control.**

---

## Overview

Antibiotic resistance in Gram-negative bacteria arises through multiple parallel mechanisms. Beta-lactamases enzymatically inactivate beta-lactam antibiotics, while RND-family efflux pumps such as AcrAB-TolC actively expel a broad range of antibiotics before they can reach their intracellular targets. Both mechanisms are clinically relevant in carbapenem-resistant organisms and often co-occur in the same isolate.

This study uses molecular docking to evaluate whether five clinically available small molecules could act as adjuvant inhibitors against these two distinct resistance mechanisms — potentially restoring the efficacy of antibiotics like meropenem. Three beta-lactamase structures and the AcrB transporter subunit were selected to probe both resistance strategies simultaneously.

Ceftriaxone, a third-generation cephalosporin and known beta-lactamase substrate, was used as a structural binding control to benchmark relative affinity scores across all four targets.

---

## Targets

| PDB ID | Protein | Class | Relevance |
|--------|---------|-------|-----------|
| [4HBU](https://www.rcsb.org/structure/4HBU) | Beta-lactamase (CTX-M-type) | Class A | Extended-spectrum resistance |
| [3OPR](https://www.rcsb.org/structure/3OPR) | Beta-lactamase | Class A | Extended-spectrum resistance |
| [1JWZ](https://www.rcsb.org/structure/1JWZ) | TEM-64 beta-lactamase | Class A | Cephalosporin-resistant mutant |
| [7OUK](https://www.rcsb.org/structure/7OUK) | AcrB (RND efflux pump transporter) | Efflux pump | Primary multidrug efflux transporter of AcrAB-TolC in *E. coli* |

---

## Ligands

| PubChem CID | Compound | Role | Rationale |
|-------------|----------|------|-----------|
| [5479530](https://pubchem.ncbi.nlm.nih.gov/compound/5479530) | Ceftriaxone | **Control** | 3rd-gen cephalosporin; known beta-lactam substrate |
| [2353](https://pubchem.ncbi.nlm.nih.gov/compound/2353) | Berberine | Test | Natural alkaloid with reported antimicrobial synergy |
| [4594](https://pubchem.ncbi.nlm.nih.gov/compound/4594) | Omeprazole | Test | Proton pump inhibitor; MBL inhibitory activity reported |
| [2520](https://pubchem.ncbi.nlm.nih.gov/compound/2520) | Verapamil | Test | Calcium channel blocker; efflux pump inhibitor candidate |
| [16682734](https://pubchem.ncbi.nlm.nih.gov/compound/16682734) | Bismuth subsalicylate | Test | Anti-diarrheal with reported MBL/virulence inhibitory activity; known bismuth-based antimicrobial |
| [12035](https://pubchem.ncbi.nlm.nih.gov/compound/12035) | Acetylcysteine | Test | Antioxidant/mucolytic; biofilm disruption properties |

---

## Methods

- **Docking software:** AutoDock Vina
- **Ligand preparation:** MMFF94 force field minimization via RDKit/Open Babel (energies embedded in filenames)
- **Protein preparation:** Structures retrieved from RCSB PDB; waters removed, hydrogens added, Gasteiger charges assigned using MGLTools
- **Output:** 9 binding poses per ligand-protein pair ranked by binding affinity (kcal/mol); RMSD upper/lower bounds reported relative to best pose
- **Analysis:** Best pose (mode 1) and pose distribution examined per compound per target

---

## Results Summary

### Best Binding Affinity by Target (kcal/mol, Mode 1)

| Compound | 4HBU | 3OPR | 1JWZ | 7OUK |
|----------|------|------|------|------|
| **Ceftriaxone (control)** | **-8.0** | **-7.6** | -7.1 | -6.2 |
| **Berberine** | -7.2 | -6.9 | **-7.6** | **-7.2** |
| Omeprazole | -7.0 | -7.0 | -7.3 | -6.0 |
| Verapamil | -6.2 | -5.7 | -6.5 | -5.5 |
| Bismuth subsalicylate* | -6.0 | -5.4 | -6.1 | -5.6 |
| Acetylcysteine | -4.6 | -4.5 | -4.8 | -4.3 |

*Bold = strongest binder per target. More negative = stronger predicted binding.*
*\* Bismuth subsalicylate docked as salicylate scaffold only (CID 338); bismuth ion absent from prepared ligand — see Limitations.*

### Key Findings

- **Berberine** is the top-performing test compound, equalling or exceeding ceftriaxone on 2 of 4 targets (1JWZ, 7OUK/AcrB) and competing closely on the remaining two. Its compact, planar, rigid scaffold appears well-suited to both the beta-lactamase active sites and the AcrB transmembrane binding pocket — consistent with its known substrate-like behaviour in RND pumps reported in the literature.
- **Omeprazole** consistently ranked second or third across all targets, remaining within ~0.5–1.0 kcal/mol of ceftriaxone on 4HBU and 3OPR — a notable result for a proton pump inhibitor with reported MBL-inhibitory properties in the literature.
- **Verapamil** is a known efflux pump inhibitor (EPI) candidate; its moderate affinity on 7OUK (-5.5 kcal/mol best pose) is consistent with its reported interaction with RND transporters, though it did not distinguish itself here relative to the other test compounds.
- **Bismuth subsalicylate** showed moderate affinity, falling 1.5–2.5 kcal/mol below the control on most targets. Note that the docked ligand (PubChem CID 338) corresponds to the salicylate organic scaffold only — the bismuth ion is likely to have been stripped during MMFF94 preparation, meaning the docking results reflect the salicylate moiety rather than the intact organometallic compound (see Limitations).
- **Acetylcysteine** was the weakest binder on all four targets (best: -4.8 kcal/mol), consistent with its small molecular size and high flexibility.
- **7OUK (AcrB)** represents a mechanistically distinct target from the three beta-lactamases. The AcrAB-TolC pump is responsible for broad-spectrum efflux of antibiotics including carbapenems, so inhibiting AcrB directly complements beta-lactamase inhibition as a resistance-breaking strategy. All test compounds showed weaker absolute affinity on AcrB relative to the beta-lactamase targets, likely reflecting the large, hydrophobic transmembrane binding pocket geometry compared to the serine active site cleft.
- **Pose convergence:** 4HBU and 1JWZ showed well-converged binding modes (low inter-pose RMSD for top poses). 7OUK showed high RMSD scatter for several ligands (verapamil, omeprazole up to ~25 Å), indicating multiple competing binding regions within AcrB's large multi-domain structure — a known challenge when docking to RND pumps without explicit pocket definition.
- **Ranking was consistent across the three beta-lactamase targets**, supporting the reliability of the relative affinities; AcrB results should be interpreted in a separate biological context given its distinct binding mechanism.

---

## Repository Structure

```
.
├── data/
│   ├── 1JWZ.csv         # Docking results: TEM-64 beta-lactamase
│   ├── 3OPR.csv         # Docking results: Class A beta-lactamase
│   ├── 4HBU.csv         # Docking results: CTX-M-type beta-lactamase
│   └── 7OUK.csv         # Docking results: AcrB RND efflux pump
└── README.md
```

---

## Limitations

- Binding affinity scores from AutoDock Vina are predicted estimates and do not account for solvation, protein flexibility (rigid receptor docking), or entropic effects.
- **Bismuth subsalicylate ligand:** PubChem standardises bismuth subsalicylate to its organic salicylate component and returns CID 338 (salicylic acid) as the downloadable 3D conformer. As a result, the docked structure represents the salicylate scaffold only. The bismuth ion — which is thought to be responsible for much of bismuth subsalicylate's reported antimicrobial activity, including Bi³⁺ coordination to MBL zinc centres — is absent from the docking run. Results for this compound should be interpreted accordingly.
- No MD simulation or MM-GBSA re-scoring was performed to validate pose stability.
- Larger ligands (e.g. ceftriaxone) may accumulate favorable Vina interaction terms due to size, independent of specificity — berberine's competitiveness at smaller MW is therefore more notable, not less.
- 7OUK (AcrB) is a mechanistically distinct target from the three beta-lactamases; direct comparison of affinity scores across these two target classes should be done cautiously. AcrB's large multi-domain transmembrane architecture means that blind docking without explicit pocket definition risks identifying non-functional binding sites — the high inter-pose RMSD for several ligands on this target reflects this.
- Verapamil's reported EPI activity in AcrAB-TolC operates at the membrane level; docking alone cannot fully capture this mechanism.
- Results require wet-lab validation (enzyme inhibition assays, MIC/checkerboard assays, efflux assays) before any biological conclusions can be drawn.

---

## Future Work

- [ ] Re-docking of berberine and omeprazole with tighter grid box centered on the catalytic serine (Ser70) of beta-lactamase targets
- [ ] Re-docking against AcrB with grid box explicitly centered on the known transmembrane inhibitor-binding pocket (as defined in the BDM88855 co-crystal structure, PDB 7OUK)
- [ ] ADMET profiling of top candidates (SwissADME, ADMETlab)
- [ ] MD simulation of top-ranked poses for pose stability validation
- [ ] Checkerboard assay design (berberine/omeprazole + meropenem against CRKP)

---

## Author

**Alaa Hamid**  
Bioengineering Graduate | Computational Drug Discovery Research Intern @ Bactrix

[LinkedIn](https://www.linkedin.com/in/) · [GitHub](https://github.com/)

---

## Tools & References

- Trott O, Olson AJ. *AutoDock Vina: improving the speed and accuracy of docking.* J Comput Chem. 2010;31(2):455–461.
- RCSB Protein Data Bank: [rcsb.org](https://www.rcsb.org)
- PubChem: [pubchem.ncbi.nlm.nih.gov](https://pubchem.ncbi.nlm.nih.gov)
- MGLTools / AutoDockTools: [ccsb.scripps.edu](https://ccsb.scripps.edu/mgltools/)
