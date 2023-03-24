# Running Alphafold2 version 2.3.1
The following container and bash script are inherited from NUS HPC IT group. For more information, please check out this [powerpoint](https://nusu-my.sharepoint.com/:p:/r/personal/ccekwk_nus_edu_sg/Documents/Workshop/Alphafold/2023_03_23_alphafold2/Alphafold%202.3%20on%20NUS%20HPC-AI%20System.pptx?d=w81edaa03535a4fe9950f09e3d08db5b6&csf=1&web=1&e=XfhPIZ).

For detailed information about parameter settings, please check out Alphafold2 official github page.<br>

Our current HPC resources:
2 nodes * 2 NVIDIA A100 40G <br>

Currently we have restrictions of 1 gpu per job submission. If you need more resources, please contact us.

### How much resources do you need for your protein modeling?
- **For protein with less than 1000 amino acids**,
- ncpus=10:mem=100gb:ngpus=1
- walltime=6:00:00
- **For protein with 1000 aa. or longer**,
- ncpus=10:mem=160gb:ngpus=1
- walltime=12:00:00
### What preset to use?
- If you want to exclude a certain known structure in PDB from your modeling, check the release date of the PDB structure and use the date after `--max_template_date=`
- If not, you can use the recent date or completely remove the line `--max_template_date=`

## Example
- Login to the server
- An example batch job submission file is located in `/data/rozen/home/e0833634/distributed_containers/alphafold_2.3.1_container/examples`, named `run_alphafold_example.sh`
- The input and output directory structures will be the same as shown in the example folder.
- Copy a copy to your own directory if needed
- Example input: actin.fasta
- Example output: Output will be stored under the folder looks like `/data/rozen/home/e0833634/distributed_containers/alphafold_2.3.1_container/examples/output/504688_af231_monomer_full_dbs_o`
- Example log: modify `.sh` files line 75 if you want to change the location of your log. The log of prediction should look like this file: `executing.504688.hn-10-03` <br>
![image](https://user-images.githubusercontent.com/89775211/227446652-4bcbc37c-1b29-4639-919a-d5e351dadaab.png)
