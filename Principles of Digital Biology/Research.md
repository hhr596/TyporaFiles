# Current Goals

1. What is the topic
2. What exactly is the topic
3. What obstacles in this area



Word List:

axiomatic [adj.] 公理的，不证自明的

counterexample [n.] 反例

entry 条目

> 戚书豪论文：
>
> 考虑到标签的影响，用的三篇顶会，deep work, 

# First - Read through the material

> DNA makes RNA makes Protein

yeast 酵母

Eukaryote 真核[/juː'kærɪəʊt/](cmd://Speak/_uk_/eukaryote)

Three main classes of organisms: Bacteria, Archaea（古菌）[/a(r)'keɪə/](cmd://Speak/_uk_/eukaryote), Eukaryotes

Feeding-Growth-Reproduction

<center>Tissue</center>

![image-20220216233657469](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202162336824.png)

Eukaryotic cell 真核细胞

![image-20220216233753910](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202162337043.png)

All the DNA of the cell sits within the nuclear. The energy from the cell come from the mitochondria.



Prokaryotic cell 原核细胞 ( the bacteria ): simpler cell structure

![image-20220216234018472](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202162340595.png)

99.9% identical between humans. 0.1% sequence is responsible for genetically determined variability among humans.

![image-20220217003532701](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170035859.png)

chromosome 染色体

genome 基因组（染色体组）

genomic database: provide frequency information

threshold 门槛

![image-20220217003740278](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170037382.png)

pathogenic 引起疾病的

![image-20220217003801685](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170038803.png)

 contiguous 毗邻的

copy number variation （CNV 拷贝数编译）

![image-20220217005241311](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170052452.png)

inversion 倒置

translocation 迁移，置换

epigenetic modification 表观遗传

> 表型（phenotype），又称性状，是指一个生物体（或细胞）可以观察到的性状或特征，是特定的基因型与环境相互作用的结果。包括个体形态、功能等各方面的表现，如身高、肤色、血型、酶活力、药物耐受力乃至性格等。经典遗传学（genetics）是指由于基因序列改变（如基因突变等）所引起的基因功能的变化，从而导致表型发生可遗传的改变；而表观遗传学（epigenetics）则是指在基因的DNA序列没有发生改变的情况下，基因功能发生了可遗传的变化，并最终导致了表型的变化。
>
> https://baike.baidu.com/item/表观遗传/3662107?fr=aladdin



# Week2

Computational approaches we use with biological data. (to try and understand a little bit more about things like protein structure protein function)

**Bioinformatics** 生物信息学

theoretical technique

caputure of data & interpretation of data

axiom 公理，格言

### Task List

- [ ] watch the lecture videos 

- [ ] read the examples (two example individual work)
- [ ] schedule the discussion this week
- [ ] arrange the assignments go to each individual

### Question List

1. What is Docker?



2. What is ENA entry?



3. What is gene ontology?

># 基因本体 
>
>随着生物技术的发展越来越快，人们得到的数据越来越多。需要寻找一种方法来组织整理这些信息。GO（gene ontology）基因本体论提供了一个省时省力的解决方案，基因产物在数据库中被赋上GO的词条，进而科学家们可以到数据库中去查询这些生物学的相关信息。
>
>基因本体（Gene Ontology，GO）是一个在[生物信息学](生物信息学.html)领域中广泛使用的[本体](本体.html)。它主要包括三个分支：细胞组件、分子功能和生物过程。
>
>基因本体是一个[有向无环图](有向无环图.html)（DAG）型的本体。目前，GO中使用了is_a、part_of和regulates三种关系。

## Bioinformatics in research

Managing post-genome data (types of RNAs etc.)

1. sequence databases
2. data repositories and standards
3. web technology (docker)

Working with data - Tools for interpreting genomic data

1. Gene prediction
2. Gene Annotation(ENSEMBL, a piece of software)

Hypothesis generation (假说生成)

## Typical examples for geometric work

things to do with the data

![image-20220217032055385](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170320576.png)

## Problems of Biology

1. Data scaling fast
2. Done at an international level?



## Types of data in biology

![image-20220217032216546](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170322716.png)

sequence, structure, secondary data



## 2 key words

##### Annotaion(descriptions about the sequences), Sequence

The annotation matters at least as much as the sequence.

Questions:

1. Whose annotation
2. Is it right(trust)
3. who does it
4. automatically annotated or done by the curator
5. making formats explicit



## Examples

![image-20220217032918933](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170329049.png)

![image-20220217032851867](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170328056.png)

notice the depth and completeness of the annotation.

![image-20220217033106426](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170331576.png)

![image-20220217033126241](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170331361.png)

original database: data of genes

secondary database: data of patterns we find

![image-20220217033435075](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170334245.png)



## Capture information

compute over knowledge base

### String matching

The basic tool

> In biology we only have one theory - evolution

homology 相同，异体同形 （homologous)

be homologous to (同源的)

1. Molecules with a common ancestor can share a function (homology)
2. We can therefore predict function if we could identify homologues
3. String matching with added evolution

> Given a sequence, look for the best matching

Four stages

1. How do I score a match
2. How do I identify the best match
3. How do I find the best match against a database
4. How do I know if it is a real homologue?

Solution: Scoring Matrix ( the higher the score, the more homologous)

**Dynamic programming** is the most used algorithm for matching

### Multiple sequence alignment

compare multiple sequences to see which part of genes are tolerated to change, and which part is not tolerated.



## Capture knowledge with an ontology

Gene ontology: A common language for annotation of Genes.(From yeast, flies, mice, plants, worms, humans)

It provides a common agreed vocabulary for gene description.

spreadsheet 电子数据表

enzyme 酶

![image-20220217060733575](https://cdn.jsdelivr.net/gh/AppleisTasty/PicGarage/tmp/202202170607698.png)

















