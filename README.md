# CursoEngBio


Arquivos para baixar:


Fastq File
https://www.drive5.com/downloads/ex_miseq_reads.tar.gz

Banco de dado para baixar genomas:
https://www.ncbi.nlm.nih.gov/


![As ômicas](https://blog.varsomics.com/wp-content/uploads/2022/03/Fatores-ambientais-1024x670.jpg.webp) 

curl -L https://ndownloader.figshare.com/files/16197626 -o genomics_de_novo_temp.tar.gz

tar -xzvf genomics_de_novo_temp.tar.gz

rm genomics_de_novo_temp.tar.gz

fastqc B_cepacia_raw_R1.fastq.gz B_cepacia_raw_R2.fastq.gz -t 6

trimmomatic PE B_cepacia_raw_R1.fastq.gz B_cepacia_raw_R2.fastq.gz \
            BCep_R1_paired.fastq.gz BCep_R1_unpaired.fastq.gz \
            BCep_R2_paired.fastq.gz BCep_R2_unpaired.fastq.gz \
            LEADING:20 TRAILING:20 SLIDINGWINDOW:5:20 MINLEN:151 \
            -threads 6
            
spades.py -1 BCep_R1_err_corr.fq.gz -2 BCep_R2_err_corr.fq.gz \
          -o spades-default-assembly/ -t 6 --only-assembler


megahit -1 BCep_R1_err_corr.fq.gz -2 BCep_R2_err_corr.fq.gz \
  -o megahit-default-assembly -t 6
  

quast -o quast-B-cep-out -r reference_genome/BCep_ref.fna \
      -g reference_genome/BCep_ref.gff -t 6 -m 1000 \

