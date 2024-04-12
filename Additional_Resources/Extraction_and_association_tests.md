# Running Association Tests with PLink from Bacterial VCF Data
To run an association test with PLINK focusing on specific genes and their regions, first extract the variants from the needed regions of your VCF file. BAM files are typically used for mapping and variant calling processes; since you already have a VCF file, we'll focus on using that for your association test with PLINK. Here’s a step-by-step guide to achieve this:

## Installing the necessary software with conda
Creating a conda environment with both PLINK (a whole genome association analysis toolset) and BCFtools (for variant calling and manipulating VCFs and BCFs) can be quite straightforward. Here's how you can do it from your macOS Terminal. This guide assumes you have Anaconda or Miniconda installed on your macOS system. If not, you'll need to install one of those first.

1. **Open Terminal**: You can find Terminal in your Applications > Utilities folder.

2. **Create a New Conda Environment**: You'll start by creating a new environment. Let's name it `genomics_tools` for this example. You can specify the Python version if necessary; however, since PLINK and BCFtools are not Python packages, the Python version might not be critical unless you plan to use Python tools as well. To create the environment, use the following command:

```bash
conda create -n genomics_tools
```

3. **Activate the Environment**: Before installing any packages, you need to activate the newly created environment.

```bash
conda activate genomics_tools
```

4. **Install PLINK**: PLINK might not be available through the default channels in Anaconda. However, it is available through Bioconda or conda-forge. If you haven't added Bioconda and conda-forge to your channels, you should do so. Bioconda depends on conda-forge. The commands below add these channels (if you haven't already) and install PLINK:

BCFtools and tabix are also available through conda.

```bash
conda config --add channels bioconda
conda config --add channels conda-forge
conda install plink bcftools tabix
```

5. **Verify Installation**: After installation, you can verify that PLINK and BCFtools are correctly installed by checking their versions. This step is not strictly necessary but is good practice to ensure everything is working as expected.

```bash
plink --version
bcftools --version
tabix --version
```

6. **Use Your Tools**: With these tools installed, your environment is set up! You can now start using PLINK, BCFtools, and tabix for your genomics analysis. Remember, whenever you want to use these tools, you should first activate the `genomics_tools` environment.

This setup should provide a basic but functional environment for genomics analysis. Depending on your specific needs, you might want to install additional tools or libraries within the same environment.


## Creating a Fam File for Phenotypes
A `.fam` file is a text file used by PLINK, typically in association studies, to define the individuals (or in your case, bacterial strains) being studied. It has a specific format with six fields per line, no header, and each field separated by whitespace (spaces or tabs). The fields are:

1. Family ID (`FID`)
2. Individual ID (`IID`)
3. Paternal ID
4. Maternal ID
5. Sex (1 = male; 2 = female; other = unknown)
6. Phenotype

In microbial studies or cases where the concept of family and parents does not apply, you can use arbitrary or placeholder values for the `FID`, paternal, maternal, and sex fields. The phenotype field is typically used to denote the disease state or any trait of interest, with -9 or 0 often used for missing or unknown phenotypes, 1 for unaffected/control, and 2 for affected/cases, although this can vary based on your study design.

Here's a step-by-step guide to creating a simple `.fam` file for your bacteria and their disease states:

1. **Decide on the Coding for Phenotypes**: For instance, 1 for not diseased (control) and 2 for diseased (case).

2. **Prepare Your Data**: Organize your bacteria names and their disease states. For example, let's say you have:

```
Bacteria1, Diseased
Bacteria2, Not Diseased
Bacteria3, Diseased
```

3. **Format Your Data**: Since family ID, paternal ID, maternal ID, and sex are not applicable, you might use placeholders. Individual ID will be your bacteria name, and phenotype will be coded based on the disease state. Assuming you use "0" for the placeholders and code "1" for Not Diseased and "2" for Diseased, your data would look like:

```
0 Bacteria1 0 0 0 2
0 Bacteria2 0 0 0 1
0 Bacteria3 0 0 0 2
```

4. **Write to a .fam File**: You can easily create this file using any text editor (like Notepad on Windows, TextEdit on macOS set to plain text mode, or nano/vim on Linux/macOS terminal). Copy your formatted data into the editor and save the file with a `.fam` extension, for example, `bacteria.fam`.

If you have a list of bacteria and their states in a spreadsheet, you can also generate this format using spreadsheet software (like Excel or Google Sheets) by arranging the data in the correct columns and then saving or exporting the data as a text file. Just make sure to replace any commas with spaces or tabs and remove any headers for PLINK compatibility.


## Extracting the genes


### Step 1: Prepare Your Gene Regions List

Ensure your list of specific gene regions is in a format compatible with tools for extracting regions from VCF files, such as BED format. A BED file is a tab-delimited text file that includes information about genomic regions. It has at least three columns:

1. **Chromosome**: The name of the chromosome (e.g., chr1, chr2, ..., chrX, chrY).
2. **Start Position**: The starting position of the gene region (0-based).
3. **End Position**: The ending position of the gene region (1-based).

Example of a BED file content for gene regions:

```
chr1    150000  250000
chr1    500000  600000
```

### Step 2: Extract Variants from Specific Regions

Use a tool like `bcftools` to extract variants from your VCF file that fall within the specified gene regions in your BED file:

```bash
bcftools view -R regions.bed input.vcf -Oz -o filtered.vcf.gz
```

- `regions.bed` is your BED file with the gene regions.
- `input.vcf` is your original VCF file.
- `filtered.vcf.gz` is the output compressed VCF file with variants from the specified regions.

### Step 3: Convert the Filtered VCF to PLINK Format

Before you convert your VCF file to a format that PLINK can use, make sure you have indexed your compressed VCF file with `tabix`:

```bash
tabix -p vcf filtered.vcf.gz
```

Then, use PLINK to convert your filtered VCF to PLINK format:

```bash
plink --vcf filtered.vcf.gz --make-bed --out mydata
```

This command converts the VCF to binary PLINK format (`--make-bed`), creating `.bed`, `.bim`, and `.fam` files prefixed with `mydata`.

### Step 4: Prepare Your Phenotype Data

Your `.fam` file contains information about your samples, including their phenotypes. You'll need to ensure this file correctly reflects your phenotype data for the association test. The phenotype data is in the last column of the `.fam` file. You may need to edit this file manually or prepare it separately and then use it with the `--pheno` flag.

### Step 5: Run the Association Test with PLINK

Now, with your data in PLINK format and your phenotype information ready, you can run the association test:

```bash
plink --bfile mydata --assoc --out results
```

This command performs a basic association test and outputs the results to a file named `results.assoc`.

### Additional Steps

Depending on your specific needs, you might want to filter your data further, adjust for multiple testing, or perform more complex statistical analyses. PLINK provides a wide range of options for association testing, including logistic regression (`--logistic`), which is often used for case-control studies, and linear regression (`--linear`) for quantitative traits.

Make sure to consult the PLINK documentation for more details on these options and to understand the best practices for association testing in your specific research context.
