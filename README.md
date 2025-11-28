# Strain Tracking in the Microbiome

## Data download

1. Download read data
2. Download assembly data
3. Download E. coli reference data

## Introductory lecture

Bacterial species and strains

1. Define species ANI, 95% threshold
2. Universal bacteria genes, species core genome, species accessory genome
3. Introduce key species: E. coli, E. faecalis, K. pneumoniae, M. gnavus, B. longum, V. parvula

The infant growth and microbiome (IGRAM) study

1. Original idea: obesity and weight gain
2. Meconium paper
3. Other papers: antibiotics, C. difficile
4. Introduce subjects 104 and 285

## Read-based approaches to strain tracking

### Introduce E. coli species-specific marker genes from StrainPhlAn

```bash
less reference_data/ecoli_marker_ids.txt
```

```bash
wc -l reference_data/ecoli_marker_ids.txt
```

Try looking up a marker in UniRef. Go to [uniprot.org](https://www.uniprot.org/). Choose the UniRef database and paste in the part of the identifier before the first pipe, for example "UniRef90_P33924".

Try searching for the marker nucleotide sequence on [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/).

### Align reads to E. coli marker genes

Index the E. coli marker genes for search.

```bash
bwa-mem2 index ecoli_db/ecoli_markers.fna
```

Align 1d samples to E. coli genes with bwa-mem

```bash
bwa-mem2 mem ecoli_db/ecoli_markers.fna igram_reads/s285.STL.V01.1.4d_1.fastq.gz > s285.STL.V01.1.4d_1_ecoli.sam
```

4. Compare the set of E. coli genes in each sample
5. Investigate SNVs in E. coli gene alignments. For a given gene, show edit distance (NM) and mismatched bases (MD).

## Assembly-based approaches to strain tracking

1. Review E. coli genome. Genome size, GC content, number of genes.
2. Tour of contigs and annotation files. Contig length (.fna), gene location on contigs (inference.tsv), gene annotations (.ffn).
3. Taxonomic annotation of contigs (Kraken assignment file). Look at species from 1d and 1m samples.
4. Use vsearch to align ORFs between samples.
5. BONUS: Point out phage tail proteins
