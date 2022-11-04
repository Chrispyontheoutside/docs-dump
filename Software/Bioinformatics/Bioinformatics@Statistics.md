# NGS: Statistics

[Back to Bioinformatics Main
Menu](/kb3/Software/Bioinformatics/Bioinformatics/)

## Fasta Stats

### Mothur

This is designed for fasta nucleotide sequences

    module load Mothur/1.39.5-intel-2017A-Python-2.7.12
    mothur "#summary.seqs(fasta=my_seqs.fasta)"

Sample output:

``` 
        Start   End NBases  Ambigs  Polymer NumSeqs
Minimum:    1   422 422 0   4   1
2.5%-tile:  1   436 436 0   4   3
25%-tile:   1   507 507 1   5   25
Median:     1   530 530 3   5   50
75%-tile:   1   961 961 6   6   74
97.5%-tile: 1   973 973 15  8   96
Maximum:    1   978 978 20  9   98
Mean:   1   678.235 678.235 4.54082 5.44898
# of Seqs:  98
```

### Seqkit

`module load SeqKit/0.5.5-linux-x86_64`  
`seqkit stats my_seqs.fasta`

Sample output:

    file           format  type  num_seqs  sum_len  min_len  avg_len  max_len
    my_seqs.fasta  FASTA   DNA        555  217,443      201    391.8    2,114

### Trinity

    module load Trinity/2.4.0-intel-2015B-Perl-5.20.0
    $TRINITY_HOME/util/TrinityStats.pl Trinity.fasta
