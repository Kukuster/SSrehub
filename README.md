# SSrehab

## how to run
run `SSrehab.py` with `python3`. It accepts 3 arguments:
 1. Path to GWAS summary statistics file in tsv format, that has a corresponding config file (suffixed \".json\") with column indices. Use `sample/29559693.tsv.gz.json` as a template. No columns are required to specify. If you don't specify a column, `SSrehab` will attempt to fully restore it, when possible.
 2. Path to the output fixed GWAS SS file
 3. Path to a dbSNP file of build that corresponds to the input GWAS SS file
 4. Path to a dbSNP file of build that corresponds to the input GWAS SS file, previously sorted by rsID using `lib/sort_SNPs_by_rsID.py`

e.g.:
```python
python3 SSrehab.py "sample/29559693.tsv.gz" "sample/29559693_fix.tsv" "/media/$USER/exFAT_share/SelfDecode/dbSNP151_GRCh37.vcf.gz" "/media/$USER/exFAT_share/SelfDecode/dbSNP151_GRCh37_rsID-sorted.vcf.gz"
# this implies that config file exists at: "sample/29559693.tsv.gz.json"
```

## main dependencies:
 - python3
 - Linux system with bash v4 or 5


## NOTES

### "standard" format
 - file is in tsv format, i.e. tabular tab-separated format (bare, zipped, or gzipped)
 - there's one-line header in the file on the first line. All other lines are the data entries
 - the file has precisely columns defined as `STANDARD_COLUMN_ORDER` in `lib/standard_column_order.py`.
    - file has exactly these columns, exactly this number of columns, and no other columns
    - columns are in this exact order
    - if the original file was missing a column, an empty column should be taking its place (entries are *the empty string*)




### BACKLOG
 - add requirements.txt and things to easily recreate the environment
 - improve interface. Use argparse or something like that for convenient CLI arguments. Add commands for preprocessing dbSNP, and separate commands: `diagnose` and `sort`.
 - add a resolver for MAF, and a liftover resolver (from build 37 to build 38)
 - a config file has to be generated with all the names of the intermediary files (or does it). This will improve refactoring into the actual pipeline.
 - (maybe) improve restoring alleles by adding checks for exact match of flipped alleles, if other checks didn't help. This requires having all SNPs for a particular ChrBP in the memory, and is relevant only for restoring alleles by looping through file sorted by Chr and BP.
 - add ability to specify additional columns from the GWAS SS file that user wants to include in the end file. This would be an array in the the json config file for the input GWAS SS file.

