# AWK Table Reshape — Long-to-Wide Profile Table Pipeline

An AWK shell pipeline that reshapes a long, stacked GMT cross-section profile table into a wide, analysis-ready table. It extracts the depth values, splits out individual trench-profile segments by regular-expression ranges, and joins them side by side into a single multi-column table. The output feeds the trench-profile stacking and regression analyses; the example data are cross-section profiles of the Kuril-Kamchatka Trench.

## What the script does

- create safe temporary files with mktemp
- select the needed columns (distance and depth) from the raw GMT table (awk, FS/OFS)
- extract the depth column for all profiles, then slice out ten individual profiles by regex address ranges (awk /start/,/end/)
- paste the ten profile columns side by side onto the distance column (paste, tee)
- strip header/tail marker rows that do not belong to the data (awk with a negated regex)
- verify row counts before and after (awk END{print NR})
- remove all auxiliary and temporary files (rm)

Result: an initial 12726-row x 5-column table becomes a 201-row x 11-column table (column 1 = cross-section distance -200..200 km; columns 2-11 = the ten profiles).

## Files

- AWK_script_table_reshape.sh: the reshaping pipeline
- AWK_to-do.sh: short notes / to-do snippet
- table2.txt: the raw long input table (stacked GMT profiles)
- table_10KKT.csv: the reshaped wide output table

## Requirements

- A POSIX shell (sh/bash) with awk, paste, tee, mktemp and rm (standard on Unix-like systems)

## Usage

Place the raw table in the working directory, then run:

    bash AWK_script_table_reshape.sh

Adjust the profile regex ranges (-L0-NN) and column selections to match your own table.

## Author

Polina Lemenkova
ORCID: https://orcid.org/0000-0002-5759-1089

## License

See the LICENSE file in this repository.
