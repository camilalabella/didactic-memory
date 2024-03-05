# Homework for week 1
## My github website:

[this is my brand new github site and you can see my homework, summary of lessons and learning plans on it](https://github.com/camilalabella/didactic-memory)


## Linux: basic commands

0. 打開Docker和文件

```
PS C:\Users\86199> docker exec -it zhangjiaying_linux bash
test@bioinfo_docker:~$ cd share
test@bioinfo_docker:~/share$ cat test_command.gtf
chr_IV  ensembl gene    1802    2953    .       +       .      gene_id "YDL248W"; gene_version "1";
chr_IV  ensembl transcript      802     2953    .       +      .gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl exon    1802    2953    .       +      .gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl CDS     1802    950     .       +      0gene_id "YDL248W"; gene_version "1";
chr_IV  ensembl start_codon     1802    1804    .       +      0gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl stop_codon      2951    2953    .      +0       gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl gene    762     3836    .       +      .gene_id "YDL247W-A"; gene_version "1";
chr_IV  ensembl transcript      3762    836     .       +      .gene_id "YDL247W-A"; gene_version "1";
```


1. 統計行數和字符數

```
test@bioinfo_docker:~/share$ wc -l test_command.gtf
8 test_command.gtf
test@bioinfo_docker:~/share$ wc -c test_command.gtf
636 test_command.gtf
```


2. grep篩選出chr_開始的YDL248W基因

```
test@bioinfo_docker:~/share$ grep 'chr_' test_command.gtf | grep '"YDL248W"'
chr_IV  ensembl gene    1802    2953    .       +       .      gene_id "YDL248W"; gene_version "1";
chr_IV  ensembl transcript      802     2953    .       +      .gene_id "YDL248W"; gene_version "1";
chr_IV  ensembl start_codon     1802    1804    .       +      0gene_id "YDL248W"; gene_version "1";
```


3. sed 替換chr_為chromosome，并輸出1，3，4，5行

```
test@bioinfo_docker:~/share$ sed 's/chr_/chromosome_/g' test_com
mand.gtf | sed -n '1p;3,5p'
chromosome_IV   ensembl gene    1802    2953    .       +      .gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl exon    1802    2953    .       +      .gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl CDS     1802    950     .       +      0gene_id "YDL248W"; gene_version "1";
chromosome_IV   ensembl start_codon     1802    1804    .      +0       gene_id "YDL248W"; gene_version "1";
```


4. awk命令 替換2，3列，sort排序并輸出到result

```
test@bioinfo_docker:~/share$ awk '{temp=$2; $2=$3; $3=temp; print}' test_command.gtf | sort -k4,4n -k5,5n > result.gtf
test@bioinfo_docker:~/share$ cat result.gtf
chromosome_IV gene ensembl 762 3836 . + . gene_id "YDL247W-A"; gene_version "1";
chr_IV transcript ensembl 802 2953 . + . gene_id "YDL248W"; gene_version "1";
chromosome_IV CDS ensembl 1802 950 . + 0 gene_id "YDL248W"; gene_version "1";
chr_IV start_codon ensembl 1802 1804 . + 0 gene_id "YDL248W"; gene_version "1";
chr_IV gene ensembl 1802 2953 . + . gene_id "YDL248W"; gene_version "1";
chromosome_IV exon ensembl 1802 2953 . + . gene_id "YDL248W"; gene_version "1";
chromosome_IV stop_codon ensembl 2951 2953 . + 0 gene_id "YDL248W"; gene_version "1";
chr_IV transcript ensembl 3762 836 . + . gene_id "YDL247W-A"; gene_version "1";
```


5. 更改示例文件的權限，使文件所有者及其組可讀寫執行，其他用戶只可讀

```
test@bioinfo_docker:~/share$ chmod ug=rwx test_command.gtf
test@bioinfo_docker:~/share$ chmod o=r test_command.gtf
test@bioinfo_docker:~/share$ ls -hl
total 16K
-rwxrwxrwx 1 test test   0 Mar  4 16:06 new_file
-rwxrwxrwx 1 test test 636 Mar  4 16:09 new_file.gtf
-rwxrwxrwx 1 test test 636 Mar  5 03:34 result.gtf
-rwxrwxr-- 1 test test 636 Mar  3 16:00 test_command.gtf
-rwxrwxrwx 1 test test 592 Mar  4 13:04 test.gtf
```
