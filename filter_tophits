#!/bin/bash

#SBATCH --job-name=tophit_count
#SBATCH --time=0-10
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=64G
#SBATCH --partition=high-capacity
#SBATCH --qos=hc-concurrent-jobs
#SBATCH -o /home/doan0033/sawshark_results/atavide_lite_out/tophit-%A_%a.out
#SBATCH -e /home/doan0033/sawshark_results/atavide_lite_out/tophit-%A_%a.err

to_be_searched="f__Tepidibacteraceae"

# Create an output file to store the final results
output_file="filtered_${to_be_searched}.tsv"
#output_file="filtered_taxa_results.tsv"
echo -e "Taxa\tSample" > "$output_file"

# Loop through all the files in the directory
for file in *tophit_report_subsystems_taxa; do
  # Extract the sample name (everything before '_S')
  sample_name=$(basename "$file" | sed -E 's/_S[0-9]+.*//')

  # Process each file: filter rows containing 'f__Halococcaceae' use zcat for .gz
  cat "$file" | awk -F '\t' '{for (i=9; i<=NF; i++) printf "%s%s", $i, (i==NF ? ORS : FS)}' | perl -ne 'print unless (/^\s+/)' | \
  grep "$to_be_searched" | awk -v sample="$sample_name" '{print $0 "\t" sample}' >> "$output_file"

done

# Sort the final output file for better readability
sort "$output_file" -o "$output_file"

echo "Processing complete. Results saved to $output_file"
