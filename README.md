# ScSmOP installation

## 1. Successful installation

A successful installation check list:

**1. Unzipped configuration files under `ConfigFiles`**
```
    $ ls ConfigFiles
        10x_scarc-atac_config.json  10x_spatial-rna_config.json                OriginalConfigFile_rdSPRITE.json          chia-drop_config.json
        10x_scarc-rna_config.json   OriginalConfigFile.json                    OriginalConfigFile_scARC-scATAC-seq.json  dropseq_scrna_config.json
        10x_scatac_v2_config.json   OriginalConfigFile_ChIA-Drop.json          OriginalConfigFile_scARC-scRNA-seq.json   rdsprite_config.json
        10x_scrna_v2_config.json    OriginalConfigFile_SPRITE.json             OriginalConfigFile_scATAC-seq.json        scsprite_config.json
        10x_scrna_v3_config.json    OriginalConfigFile_Spatial-scRNA-seq.json  bgi_scrna-seq_config.json                 sprite_config.json
```

**2. Unzipped barcode whitelist files under `BarcodeBucket`**
```
    $ ls BarcodeBucket
        3M-february-2018.txt            SPRITE.EVEN.txt      rdSPRITE.ODD.txt             scSPRITE_Y_Barcode.txt     visium-v4.txt
        4M-with-alts-february-2016.txt  SPRITE.ODD.txt       rdSPRITE.RPM.txt             visium-v1.txt              visium-v4_coordinates.txt
        737K-arc-v1-scatac.txt          SPRITE.Y.txt         rdSPRITE.Y.txt               visium-v1_coordinates.txt  visium-v5.txt
        737K-arc-v1-scrna.txt           dpm96.fasta          scSPRITE_DPMPRE_Barcode.txt  visium-v2.txt              visium-v5_coordinates.txt
        737K-august-2016.txt            rdSPRITE.DPM.txt     scSPRITE_DPM_Barcode.txt     visium-v2_coordinates.txt
        737K-cratac-v1.txt              rdSPRITE.EVEN.txt    scSPRITE_EVEN_Barcode.txt    visium-v3.txt
        SPRITE.DPM.txt                  rdSPRITE.LIGTAG.txt  scSPRITE_ODD_Barcode.txt     visium-v3_coordinates.txt
```
**3. Executable pipeline (*-rwxrwxrwx*) scripts files under `PipelineScript`**
```
    $ ls -l PipelineScript/
        -rwxrwxrwx 1 kasenjing kasenjing  1117 Sep 25 23:37 10x_scrna-v2.sh
        -rwxrwxrwx 1 kasenjing kasenjing  7075 Sep 25 20:19 BarcodeIdentification.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1518 Sep 25 20:19 ChIA-Drop.sh
        -rwxrwxrwx 1 kasenjing kasenjing 16915 Oct 11 16:33 GroupAndDataRefine.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1438 Oct  9 19:54 HiC.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1423 Sep 25 20:19 Lanuch_ChIA-Drop.sh
        -rwxrwxrwx 1 kasenjing kasenjing 14937 Sep 25 20:19 QualityAssessment.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1784 Sep 25 20:19 SPRITE.sh
        -rwxrwxrwx 1 kasenjing kasenjing 10753 Oct 11 22:58 SequenceAlignment.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1119 Sep 25 23:37 dropseq_scrna.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1682 Sep 25 20:19 rdSPRITE.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1418 Sep 25 20:19 scATAC.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1140 Oct 23 18:13 scRNA.sh
        -rwxrwxrwx 1 kasenjing kasenjing  1293 Sep 25 20:19 scSPRITE.sh
        -rwxrwxrwx 1 kasenjing kasenjing  2858 Sep 25 23:37 scarc.sh
```
**4. Executable bioinformatic tools under `Tools`**
```
    $ ls Tools
        BARP    
        Rscript  
        STARM.tar.gz      
        bedtools  
        cutadapt                  
        macs2      
        pigz     
        samtools
        FastQC  
        STAR     
        TrimGalore-0.6.6  
        bwa       
        juicer_tools_1.19.01.jar  
        pairtools  
        python3  
        trim_galore
```
Some of these tools are used in processing all kinds of data while some of these don't ([Detail](#2-tools)).

## 2. Tools 
|Tool|Version|Used in|URL|
|---|:---:|:---:|:---:|
|BARP|0.0.1|All|This hub|
|samtools|1.18|All|https://github.com/samtools/samtools|
|trim_galore|0.6.6|SPRITE, scSPRITE, RD-SPRITE|https://github.com/FelixKrueger/TrimGalore|
|cutadapt|4.5|SPRITE, scSPRITE, RD-SPRITE|https://github.com/marcelm/cutadapt/|
|STAR*|2.7.10|RNA data of All technologies|This Hub|
|bedtools|2.31.0|SPRITE, scARC-seq ATAC part, scATAC-seq|https://github.com/arq5x/bedtools2|
|macs2|2.2.9.1|scARC-seq ATAC part, scATAC-seq|https://github.com/macs3-project/MACS/wiki/Install-macs2|
|bwa|0.7.17|Technologies with DNA fragment|https://github.com/lh3/bwa|
|Rscript|4.3.1|ChIA-Drop, scARC-seq ATAC part, scATAC-seq|https://www.r-project.org/|
|pairtools|1.0.2|scAIR-seq|https://github.com/open2c/pairtools|
|pigz|2.4|scAIR-seq|https://github.com/madler/pigz|

\* *Modified STAR source code to make it capable of processing BARP produced FASTQ files while retaining exact other functions.*

## 3. What if some tools failed to install

There are two kinds of reminders if some tools failed to install:

#### 1. Tools installed with conda: *samtools macs2 bedtools Rscript bwa pairtools*
```
    Installation of [Tool] failed, you may need to reinstall them with

            conda install [Tool] -n ScSmOP -y

    or you can link one of your previously installed  to the directory of ScSmOP/Tools
```
Reinstall Tools, for example: macs2:
```
    conda install macs2=2.2.9.1 -n ScSmOP -y
```

#### 2. Tools compiled locally: *BARP STAR*
```
    Installation of  failed, it may caused by the failed installation of "gcc", "g++", reinstall these with
            conda install -c conda-forge/label/cf202003 cxx-compiler -y -n ScSmOP
            conda install make -n ScSmOP -y -c conda-forge
    and then recompile it.
```
These tools need gcc and g++ to compile them. 

After install gcc and g++, recompile ***BARP*** as follow (suppose you are under directory **ScSmOP**):
```
    cd BARP-prog
    make
    cd ..
    ln -s BARP-prog/BARP Tools/BARP
```

Recompile ***STAR*** as follow (suppose you are under directory **ScSmOP**):
```
    cd Tools
    tar -zxvf STARM.tar.gz
    cd STARM/source
    make STAR
    cd ../..
    mv STARM/source/STAR .
    rm -r STARM
```

