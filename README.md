# Demultiplex_practice
A Python script for demultiplexing sequencing reads, implemented as a learning project.

Note: The efficiency of the implementation could be significantly lower than that of widely used software.

## What is demultiplexing?
It is the process of separating mixed sequencing reads from a single file into separate files for each individual sample, using unique index sequences attached to each sample to assign reads to their original source.

## Installation
1. Install dependencies

I used some pre-built libraries for convenience rather than building everything from scratch, such as Biopython and RapidFuzz. These libraries help a lot with tasks like reading raw reads and matching index.
```sh
pip install -r requirements.txt
```

2. Local package installs
```sh
pip install -e .
```

## Usage

### Single-end
```python
from demux import SingleEndDemux

demux = SingleEndDemux(
    index_path = "/path/to/index.txt",
    raw_path = "/path/to/rawdata.fastq.gz",
    save_dir = "/path/to/save/dir/",
    pr = "PRIMER",
    allow_mismatch = 0,
    threads = None,
    read_direction = "forward",
    dry = False
)
```
`index_path`: Path to index .TXT file, format: `SAMPLE_ID<tab>INDEX`

`raw_path`: Path to raw .FASTQ.GZ file.

`save_dir`: The directory to save demultiplexed .FASTQ.GZ file.

`pr`: The primer sequence after the index. Default is `"GTCGGTAAAACTCGTGCCAGC"`(MiFish-UF).

`allow_mismatch`: Allow mismatch for barcode matching. Default is 0.

`threads`: Number of CPU cores to be used for processing. If not specified, maximum number of available cores will be used. Default is `None`.

`read_direction`: `forward` or `reverse`. Default is `"forward"`.

`dry`: Dry run. If True, no files will be written; only a demultiplexed report will be output. Default is `False`.

### Paired-end
```python
from demux import PairedEndDemux

demux = PairedEndDemux(
    index_path = "/path/to/index.txt",
    for_raw_path = "/path/to/rawdata_R1.fastq.gz",
    rev_raw_path = "/path/to/rawdata_R2.fastq.gz",
    save_dir = "/path/to/save/dir/",
    pr_5 = "FORWARD_PRIMER",
    pr_3 = "REVERSE_PRIMER",
    allow_mismatch = 0,
    threads = None,
    dry = False
)
```
`index_path`: Path to index .TXT file, format: `SAMPLE_ID<tab>FORWARD_INDEX<tab>REVERSE_INDEX`

`for_raw_path`: Path to raw _R1.FASTQ.GZ file.

`rev_raw_path`: Path to raw _R2.FASTQ.GZ file.

`pr_5`: The forward primer sequence after the forward index. Default is `"GTCGGTAAAACTCGTGCCAGC"`(MiFish-UF).

`pr_3`: The reverse primer sequence after the reverse index. Default is `"CATAGTGGGGTATCTAATCCCAGTTTG"`(MiFish-UR).

### Example
You can use the `example.ipynb` notebook and the materials in the [`example`](/example) folder to practice.
