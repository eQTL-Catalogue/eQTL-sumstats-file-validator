# Summary Statistics TSV file Validator

A file validator for validating eQTL summary statistics TSV files prior to conversion to HDF5. The validator uses [pandas_schema](https://tmiguelt.github.io/PandasSchema/). 

## Installation
- `git clone https://github.com/eQTL-Catalogue/eQTL-sumstats-file-validator.git`
- `pip install -r requirments.txt`
- `pip install .`

## Running the validator
To run the validator on a file:
- `ss-validate -f <file_to_validate.tsv> --logfile <logfile_name>`

Information and errors are logged to the console and errors logged to the file specified. A console output might look like:
```
(INFO): Filename is good!
(INFO): Validating file...
(ERROR): Length of row 7 is: 16 instead of 15
(ERROR): Please fix the table. Some rows have different numbers of columns to the header
(INFO): Rows with different numbers of columns to the header are not validated
(ERROR): {row: 1, column: "p_value"}: "-99" was not in the range [0, 1)
```
The errors from the output tell us that row seven has too many columns and row one does not have a valid pvalue. If these rows are not fixed, they will later be dropped and not converted to HDF5. 

### Addional options
- `--linelimit` : _int, default 1000_

   Once this number of erroneous rows has been reached, stop looking for more.
- `--drop-bad-lines` : _bool, default False_
