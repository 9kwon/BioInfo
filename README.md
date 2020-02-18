(다음은 코네티컷 대학의 computational biology 페이지에 있는 파일 포맷 튜토리얼을 한국어로 정리한 것입니다. 출처: https://bioinformatics.uconn.edu/resources-and-events/tutorials-2/file-formats-tutorial/#)

File Formats Tutorial
생물정보학에서 일반적으로 많이 쓰이는 다음의 파일에 대한 설명

FASTA
FASTQ
SAM
BAM
VCF
GFF
GTF
1. FASTA
File format : FASTA
File extensions : file.fa, file.fasta, file.fsa

Example :

XR_002086427.1 Candida albicans SC5314 uncharacterized ncRNA (SCR1), ncRNA

TGGCTGTGATGGCTTTTAGCGGAAGCGCGCTGTTCGCGTACCTGCTGTTTGTTGAAAATTTAAGAGCAAAGTGTCCGGCTCGATCCCTGCGAATTGAATTCTGAACGCTAGAGTAATCAGTGTCTTTCAAGTTCTGGTAATGTTTAGCATAACCACTGGAGGGAAGCAATTCAGCACAGTAATGCTAATCGTGGTGGAGGCGAATCCGGATGGCACCTTGTTTGTTGATAAATAGTGCGGTATCTAGTGTTGCAACTCTATTTTT



Fasta 형식은 핵산 및 단백질의 뉴클레오티드 또는 아미노산 서열을 나타내는 간단한 방법으로 두 개의 최소 행이 있는 매우 기본적인 형식.
주석 줄이라고 하는 첫 번째 줄은 ‘>’로 시작하고 순서에 대한 기본 정보를 제공. 주석 행에 설정된 형식은 없음. 주석 행 이후, 핵산 또는 단백질의 서열은 표준 1 문자 코드에 포함되며, 순서대로 모든 표 작성기, 공백, 별표 등은 무시됨


2. FASTQ
File format : FASTQ
File extensions : file.fastq, file.sanfastq, file.fq



Example :

@K00188:208:HFLNGBBXX:3:1101:1428:1508 
2:N:0:CTTGTAATAATAGGATCCCTTTTCCTGGAGCTGCCTTTAGGTAATGTAGTATCTNATNGACTGNCNCCANANGGCTAAAGT
+
AAAFFJJJJJJJJJJJJJJJJJFJJFJJJJJFJJJJJJJJJJJJJJJJ#FJ#JJJJF#F#FJJ#F#JJJFJJJJJ


Fastq 형식은 서열과 품질 점수 (Q : phred quality score)를 그룹화하기 위해 Sanger Institute에서 개발했으며, fastq 파일에서 각 항목은 4 줄과 연결됨.


1 행: ‘@’문자로 시작하며 시퀀스 식별자 및 선택적 설명
2 행: 표준 1 문자 코드의 시퀀스
3 행: "+"문자로 시작하며 선택적으로 동일한 시퀀스 식별자 (및 추가 설명)가 다시 옴
4 행: 2 행의 시퀀스에 대한 품질 값을 인코딩하며 시퀀스의 문자와 동일한 수의 기호를 포함해야 함



fastq 형식에 대한 자세한 설명 :


1 행 : @ K00188 : 208 : HFLNGBBXX : 3 : 1101 : 1428 : 1508 2 : N : 0 : CTTGTA



fastq_table



2 행 : DNA 서열



3 행 : +



4 행 : 각 기본 쌍에 대한 품질 평가 점수 (PHRED 척도). 베이스가 올바르게 시퀀싱되고 식별되었다는 것을 얼마나 확신할 수 있는지 나타냄
Q = -10log­10 (p)
여기서 p는 해당 기준 통화가 올바르지 않을 확률


Fastq-sanger는 0-93에서 PHRED 점수를, fastq-Illumina는 0-62에서 PHRED 점수를 나타냄. PHRED 점수의 숫자 값을 제공하는 대신 33에서 126 사이의 ASCII 문자 코드로 제공되며, 단일 문자는 33-126 코드이므로 단일 문자로 점수를 표시 할 수 있음 (아래 표 참고)


기본 문자 (PHRED 점수 0을 나타내는 문자)를 기준으로 PHRED 스케일은 FHRED + 33 (ASCII 문자) 또는 FHRED + 64 (ASCII 문자). 아래 그림은 다양한 시퀀싱 표기법에 따른 PHRED 사용량을 보여줌.


.fastq 파일에 사용 된 PHRED 점수 유형을 처리하기 전에 파악해야 함. 현재 Illumina .fastq 파일의 PHRED 점수는 +33. 
자세한 내용은 https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2847217/ 을 참조





3. SAM (Sequence Alignment Map)
File format :     SAM

File extensions :     file.sam

Example : 

1:497:R:-272+13M17D24M 113 1 497 37 37M 15 100338662 0 CGGGTCTGACCTGAGGAGAACTGTGCTC
CGCCTTCAG 0;==-==9;>>>>>=>>>>>>>>>>>=>>>>>>>>>> XT:A:U NM:i:0 SM:i:37 AM:i:0 X0:i:1 X1:i:0 XM:i:0 XO:i:0 XG:i
:0 MD:Z:37 
19:20389:F:275+18M2D19M 99 1 17644 0 37M = 17919 314 TATGACTGCTAATAATACCTACACATGTTAGAACCA
T >>>>>>>>>>>>>>>>>>>><<>>><<>>4::>>:<9 RG:Z:UM0098:1 XT:A:R NM:i:0 SM:i:0 AM:i:0 X0:i:4 X1:i:0 XM:i:0 XO:i
:0 XG:i:0 MD:Z:37 
19:20389:F:275+18M2D19M 147 1 17919 0 18M2D19M = 17644 -314 GTAGTACCAACTGTAAGTCCTTATCTTC
ATACTTTGT ;44999;499<8<8<<<8<<><<<<><7<;<<<>><< XT:A:R NM:i:2 SM:i:0 AM:i:0 X0:i:4 X1:i:0 XM:i:0 XO:i:1 XG:i
:2 MD:Z:18^CA19 
9:21597+10M2I25M:R:-209 83 1 21678 0 8M2I27M = 21469 -244 CACCACATCACATATACCAAGCCTGGCTGTGTCTTC
T <;9<<5><<<<><<<>><<><>><9>><>>>9>>><> XT:A:R NM:i:2 SM:i:0 AM:i:0 X0:i:5 X1:i:0 XM:i:0 XO:i:1 XG:i:2 MD:Z
:35
- SAM 형식은 탭으로 구분된 ASCII 열에 시퀀스 데이터를 저장하기 위한 텍스트 형식.

- 보통 자매 BAM 형식의, 사람이 읽을 수있는 버전으로 생성되며, 동일한 데이터를 압축 색인화된 이진 형식으로 저장 
- SAM 형식 파일은 read를 참조 시퀀스에 매핑 한 후 생성 되며, 헤더와 본문이 있는 탭으로 구분 된 텍스트 형식임.

- 머리말 줄은‘@’로 시작하지만 맞춤 줄은 그렇게 시작하지 않음.

- 헤더는 파일이 정렬 된 경우 버전 정보, 참조 순서 정보 등 SAM 파일에 대한 일반 정보를 보유합

- 정렬 레코드는 파일의 본문을 구성하며, 각 정렬 라인 / 레코드에는 필수 정렬 정보를 설명하는 11 개의 필수 필드가 있음



* sequence alignment: DNA, RNA 또는 단백질의 서열을 배열하여 서열 사이의 기능적, 구조적 또는 진화 적 관계의 결과 일 수있는 유사성의 영역을 확인하는 방법



* SAM 설명서에 사용 된 몇 가지 용어 :
Template : 측정된 DNA 조각

Reads : 방법에 따라 템플릿이 하나 이상의 read를 생성할 수 있고, 이러한 read는 전체 템플릿 또는 해당 하위 섹션을 포괄할 수 있음. 동일한 템플릿에서 시작된 read는 템플릿의 다른 부분을 다루며, 템플릿 자체 또는 템플릿의 역보완(reverse complement)을 나타낼 수 있음
Segments : 각 read는 segment라고 불리는 영역을 할당받는 하나 이상의 정렬을 생성할 수 있음. 이러한 segment로 원본 템플릿의 크기를 유추 할 수 있음


source: http://samtools.github.io/hts-specs/SAMv1.pdf
Fields: 
Col. 1 QNAME :
Query NAME. QNAME이 동일한 reads/segments는 동일한 템플릿에서 가져온 것으로 간주됨.

QNAME ‘*’ 는 정보를 사용불가를 나타며, SAM 파일에서 alignment 키메라(하나의 생물체 안에 유전 형질이 다른 세포가 함께 존재하는 경우)인 경우 read는 여러 alignment 라인을 차지할 수 있음



Col. 2 FLAG: bit단위 플래그의 조합


Col. 3 RNAME : 
참조 순서의 이름. 일반적으로 염색체 수를 나타냄



Col. 4 POS:

read에서 첫 번째로 일치하는 베이스의 가장 왼쪽 매핑 위치. 1-based 인덱싱. pos가 0으로 설정되면 매핑되지 않은 read임. 하나의 read에 대해 READ1/1, READ1/2, 단일 Read2

Reference:    GTACGACTGACTAGACGATAC**GTAACGATCAGTCTCGATAGCGATAGGCTAGCTAGCAGCTAGCAG       
              12345678901234567890123456789012345678901234567890123456789012345678          
Read1/1         ACGACTGA   
-Read1/2                                         CGATAGC 
Read2       ccccGATACTAGTAA*GAT..GTCT             
Pos values    3                                38


Col. 5 MAPQ: 

매핑 품질.  MAPQ = -10log10 (매핑 위치가 잘못됐을 가능성). MAPQ = 255는 매핑 품질을 사용 불가.



Col. 6 CIGAR:

alignment를 설명하는 문자열


H와 S의 차이점은, 불일치 시퀀스가 정렬 파일에서 read 시퀀스의 일부로 보고 되면 소프트 클리핑이라는 것. 불일치 영역은 종종 참조 시퀀스의 다른 곳과 일치하며, 이 경우 불일치 영역은 정렬된 상태로 보고된 read 시퀀스에서 제거되며 하드 클리핑 (hard clipping)으로 지칭됨

Reference:    GTACGACTGACTAGACGATAC**GTAACGATCAGTCTCGATAGCGATAGGCTAGCTAGCAGCTAGCAG    
              12345678901234567890123456789012345678901234567890123456789012345678          
Read2                    ccccGATACTAGTAA*GAT..GTCT
POS 예제에서 Read2의 CIGAR 값은 다음과 같음
cccc는 소프트 클리핑과 관련하여 다른 곳에서는 일치하지 않음

, 5 (GATAC) 일치, 2 (TA) 삽입, 4 (GTAA) 일치, 1 (*) 삭제, 3 (GAT) 일치, 2 (..) 참조에서 건너 뛴 영역 (N), 4 (GTCT) 일치 
시가 문자열 : 
Read 2 : 5S2M2I4M1D3M2N4M



Col. 7 RNEXT , Col. 8 PNEXT:

RNEXT 및 PNEXT는 시각화 도구를 위한 paired end read 쌍(partner)의 참조 및 위치를 파악하기 위한 것.

RNEXT는 a pair align에서 다음 템플렛에 있는 염색체 또는 콘티그(서로 겹치면서 연속되어 있는 DNA 절편들의 집합)의 이름. ‘=’값의 RNEXT는 동일한 참조에 align됨을 의미하고 ‘*’는 사용 가능한 정보가 없음을 나타냄 (single end sequencing). 쌍의 다른 read가 정렬되는 PNEXT (정보를 사용할 수 없음 = 0, 그렇지 않으면 POS 값)

Reference:    GTACGACTGACTAGACGATAC**GTAACGATCAGTCTCGATAGCGATAGGCTAGCTAGCAGCTAGCAG
              12345678901234567890123456789012345678901234567890123456789012345678          
Read1/1         ACGACTGA   
-Read1/2                                         CGATAGC 
Read2                    ccccGATACTAGTAA*GAT..GTCT  
Read1/1 과 Read1/2 가 쌍이고, Read 3 는 쌍이 없음. 그러므로 RNEX 및 PNEXT 값은 다음과 같음

READ                        RNEXT                PNEXT              TLEN

Read1/1                        =                     38                   42

Read1/2                        =                      3                   -42

Read3                           *                      0                     0



Col. 9 TLEN : Observed Template LENgth

pair end read로 커버되는 참조 길이. 쌍으로 된 read에서 가장 왼쪽 매핑된 베이스와 가장 오른쪽 매핑된 베이스 사이의 거리로, 페어링되지 않은 read는 0



Col. 10 SEQ: read나 segment의 서열(sequence)


Col. 11 QUAL: read의 PHRED score values.  ‘*’는 저장된 값이 없음을 의미

Example:




4. BAM (Binary Alignment / Map)
File format :     BAM

File extensions :     file.bam

BAM (Binary Alignment / Map) 파일은 압축된 이진 버전의 Sequence Alignment / Map (SAM)이며, 뉴클레오티드 서열 정렬의 컴팩트하고 색인 가능한 표현. SAM과 BAM 간의 데이터는 정확히 동일. 이진 BAM 파일은 크기가 작으며 정렬 파일을 저장하는데 이상적. 파일을 보려면 samtools가 필요함





5. VCF (Variant Calling Format / File)
File format :     VCF

File extensions :     file.vcf

Example:

##fileformat=VCFv4.2 
##fileDate=20090805 
##source=myImputationProgramV3.1 
##reference=file:///seq/references/1000GenomesPilot-NCBI36.fasta 
##contig=<ID=20,length=62435964,assembly=B36,md5=f126cdf8a6e0c7f379d618ff66beb2da,species="Homo sapiens",taxonomy=x> 
##phasing=partial 
##INFO=<ID=NS,Number=1,Type=Integer,Description="Number of Samples With Data"> 
##INFO=<ID=DP,Number=1,Type=Integer,Description="Total Depth"> 
##INFO=<ID=AF,Number=A,Type=Float,Description="Allele Frequency"> 
##INFO=<ID=AA,Number=1,Type=String,Description="Ancestral Allele"> 
##INFO=<ID=DB,Number=0,Type=Flag,Description="dbSNP membership, build 129"> 
##INFO=<ID=H2,Number=0,Type=Flag,Description="HapMap2 membership"> 
##FILTER=<ID=q10,Description="Quality below 10"> 
##FILTER=<ID=s50,Description="Less than 50% of samples have data"> 
##FORMAT=<ID=GT,Number=1,Type=String,Description="Genotype"> 
##FORMAT=<ID=GQ,Number=1,Type=Integer,Description="Genotype Quality"> 
##FORMAT=<ID=DP,Number=1,Type=Integer,Description="Read Depth"> 
##FORMAT=<ID=HQ,Number=2,Type=Integer,Description="Haplotype Quality"> 
#CHROM POS ID REF ALT QUAL FILTER INFO FORMAT NA00001 NA00002 NA00003 
20 14370 rs6054257 G A 29 PASS NS=3;DP=14;AF=0.5;DB;H2 GT:GQ:DP:HQ 0|0:48:1:51,51 1|0:48:8:51,51 1/1:43:5:.,. 
20 17330 . T A 3 q10 NS=3;DP=11;AF=0.017 GT:GQ:DP:HQ 0|0:49:3:58,50 0|1:3:5:65,3 0/0:41:3 
20 1110696 rs6040355 A G,T 67 PASS NS=2;DP=10;AF=0.333,0.667;AA=T;DB GT:GQ:DP:HQ 1|2:21:6:23,27 2|1:2:0:18,2 2/2:35:4 
20 1230237 . T . 47 PASS NS=3;DP=13;AA=T GT:GQ:DP:HQ 0|0:54:7:56,60 0|0:48:4:51,51 0/0:61:2 
20 1234567 microsat1 GTC G,GTCT 50 PASS NS=3;DP=9;AA=G GT:GQ:DP 0/1:35:4 0/2:17:2 1/1:40:3
VCF는 헤더(정보 VCF 버전, 샘플 등)가있는 텍스트 파일 형식이며, 데이터 라인이 파일 본문을 구성함



HEADER: 메타 정보가 포함되며 ‘##’ 문자열 뒤에 포함됨.

            데이터 필드에 대한 자세한 설명을 위해 INFO, FILTER 및 FORMAT 항목을 포함하는 것이 좋음

메타 데이터 형식 :

##INFO=<ID=ID,Number=number,Type=type,Description="description",Source="source",Version="version"> 
##FILTER=<ID=ID,Description="description">##FORMAT=<ID=ID,Number=number,Type=type,Description="description">
alternate allele, assembly field, Contig field, sample field, pedigree field와 같은 다른 정보도 포함 가능함



DATA FIELD: 데이터 라인은 8개의 필수 열을 가짐 (#CHROM, POS, ID, REF, ALT, QUAL, FILTER, INFO)

VCF 포맷은 다음 문서에서 상세히 설명하고 있음  https://samtools.github.io/hts-specs/VCFv4.2.pdf





6. GFF (General Feature Format or Gene Finding Format)
File format :     GFF

File extensions :     file.gff2, file. gff3, file.gff

Example : 

GFF2

browser position chr22:10000000-10025000 
browser hide all 
track name=regulatory description="TeleGene(tm) Regulatory Regions" 
visibility=2 
chr22 TeleGene enhancer 10000000 10001000 500 + . touch1 
chr22 TeleGene promoter 10010000 10010100 900 + . touch1 
chr22 TeleGene promoter 10020000 10025000 800 - . touch2
GFF3

GFF2와 같은 처음 8 개의 필드가 있지만 속성 지정에서 필드 9가 다른데, 여기에 2가 강조 표시됨 



(a) GFF3는 nesting feature에 더 나음. 부모 태그에 대한 Link가 특징화됨

##gff-version 3 
ctg123 . mRNA           1300 9000 . + . ID=mrna0001;Name=sonichedgehog 
ctg123 . exon           1300 1500 . + . ID=exon00001;Parent=mrna0001 
ctg123 . exon           1050 1500 . + . ID=exon00002;Parent=mrna0001 
ctg123 . exon           3000 3902 . + . ID=exon00003;Parent=mrna0001 
ctg123 . exon           5000 5500 . + . ID=exon00004;Parent=mrna0001 
ctg123 . exon           7000 9000 . + . ID=exon00005;Parent=mrna0001
(b) 단백질 코딩 유전자를 나타내는 가장 일반적인 방법은 소위 "three-level gene"임. 최상위 수준은 유전자의 전사물(transcript)과 조절 인자(regulatory elements)를 묶는 "유전자" 유형의 feature이며, 이 수준 아래에는 "mRNA" 유형의 하나 이상의 전사물이 있음. 이 수준은 프로모터 및 다른 시스 조절 인자(cis-regulatory elements)를 수용 할 수 있음.

세 번째 수준에는 mRNA 전사체의 구성 요소, 가장 일반적으로 CDS 코딩 세그먼트 및 UTR이 있음.

아래 예는 3개의 대안적으로 스플라이싱된 mRNA 전사체를 갖는 "EDEN"이라는 유전자를 나타내는 방법을 보여줌

ctg123 example gene           1050 9000 . + . ID=EDEN;Name=EDEN;Note=protein kinase 
ctg123 example mRNA           1050 9000 . + . ID=EDEN.1;Parent=EDEN;Name=EDEN.1;Index=1 
ctg123 example five_prime_UTR 1050 1200 . + . Parent=EDEN.1 
ctg123 example CDS             1201 1500 . + 0 Parent=EDEN.1 
ctg123 example CDS             3000 3902 . + 0 Parent=EDEN.1 
ctg123 example CDS             5000 5500 . + 0 Parent=EDEN.1 
ctg123 example CDS             7000 7608 . + 0 Parent=EDEN.1 
ctg123 example three_prime_UTR 7609 9000 . + . Parent=EDEN.1 
ctg123 example mRNA           1050 9000 . + . ID=EDEN.2;Parent=EDEN;Name=EDEN.2;Index=1 
ctg123 example five_prime_UTR 1050 1200 . + . Parent=EDEN.2 
ctg123 example CDS             1201 1500 . + 0 Parent=EDEN.2 
ctg123 example CDS             5000 5500 . + 0 Parent=EDEN.2 
ctg123 example CDS             7000 7608 . + 0 Parent=EDEN.2 
ctg123 example three_prime_UTR 7609 9000 . + . Parent=EDEN.2 
ctg123 example mRNA           1300 9000 . + . ID=EDEN.3;Parent=EDEN;Name=EDEN.3;Index=1 
ctg123 example five_prime_UTR 1300 1500 . + . Parent=EDEN.3 
ctg123 example five_prime_UTR 3000 3300 . + . Parent=EDEN.3 
ctg123 example CDS             3301 3902 . + 0 Parent=EDEN.3 
ctg123 example CDS             5000 5500 . + 1 Parent=EDEN.3 
ctg123 example CDS             7000 7600 . + 1 Parent=EDEN.3 
ctg123 example three_prime_UTR 7601 9000 . + . Parent=EDEN.3
GFF는 염기 서열, 엑손, 인트론, 프로모터, 3 'UTR, 반복 요소 등의 모든 기능에 사용될 수 있지만 GTF는 주로 유전자 / 전사에 사용됨. GFF3은 최신 버전이며 GFF2 형식보다 개선됨. 그러나 많은 데이터베이스에는 여전히 GFF3 버전을 처리 할 수있는 기능이 없음. 


GFF 형식에는 9 개의 필수 열이 있으며 탭으로 구분됨. 9 열은 다음과 같음

Col. 1 Reference Sequence: 주석 좌표 시스템을 설정하는 데 사용되는 참조 시퀀스의 ID. 염색체 이름 또는 번호



Col. 2 Source: 기능 주석이 파생되는 방법에 대한 설명. 소스는 이 기능을 생성한 알고리즘 또는 운영 절차를 설명하기 위한 자유 텍스트 qualifier임. 보통 "Genescan"과 같은 소프트웨어 또는 "Genbank"와 같은 데이터베이스 이름.실제로 소스는 유형 열에 유형의 서브 클래스인 새 구성 유형(composite type)을 작성하여 qualifier를 유형에 추가하여 feature 온톨로지를 확장하는 데 사용됨. 소스를 지정할 필요는 없으며, 출처가 없으면 필드에 “.”을 입력



Col. 3 Feature: "gene" 또는 "exon"과 같은 feature 이름. 잘 구성된 GFF 파일에서 모든 자식(엑손, 인트론 등) feature는 항상 부모(전사물) feature 라인을 따르며, 이런 식으로 단일 블록의 일부가 됨



Col. 4 Start: feature의 유전자적 시작



Col. 5 End: feature의 유전자적 끝



Col. 6 Score: 주석이 달린 피쳐에서 소스의 신뢰도를 일반적으로 나타내는 숫자 값. "."의 값 (점)은 null 값을 정의하는 데 사용. 점수의 semantics는 잘 정의되어 있지 않음(ill-defined). GFF3 형식에서는 E- 값을 서열 유사성 특징에 사용하고 P- 값을 초기 유전자 예측 특징에 사용하는 것이 좋으며, 점수가 없으면 필드에 “.”을 입력



Col. 7 Strand: 피처의 감지 가닥을 나타내는 필드

“+ ': Watson strand

‘-’: Crick stran

‘?’는 관련성이 있지만 알려지지 않은 피쳐



Col. 8 Frame (GFF2 and GTF) or Phase (GFF3):

"CDS" 유형의 피쳐에서 위상(phase)은 피처가 read 프레임을 참조하여 시작되는 위치를 나타냄. 위상은 정수 0, 1 또는 2 중 하나이며, 이 피쳐의 시작에서 제거되어 다음 코돈의 첫 번째 염기에 도달해야 하는 염기의 수를 나타냄.

즉, "0"의 위상은 다음 코돈이 현재 라인에 의해 기술된 영역의 첫 번째 염기에서 시작함을 나타내고,

"1"의 위상은 다음 코돈이 이 영역의 두 번째베이스에서 시작됨을 나타내고,

"2"의 위상은 코돈이 이 영역의 세 번째 염기에서 시작 함을 나타냄.

이것은 단순히 모듈로 3을 시작하는 프레임과 혼동되어서는 안되며, 위상이 없으면 필드에 “.” 

 
정방향 스트랜드 피쳐에서 위상은 시작 필드부터 계산됨. 리버스 스트랜드 피처의 경우, 위상은 끝 필드에서 계산됨.

위상(phase)은 모든 CDS 피쳐에 대해 필수적(required).



### and ***는 연속적인 엑손을 나타내며, CTG  C는 첫번째 base (0), T는 두번째 base (1), G는 세번째 base (2) 

Previous exon               Phase value                next Exon   
5’                                                           3’ 
…###***###***###                0                      ***###***###***#… 
…##***###***###*                1                      **###***###***##… 
…#***###***###**                2                      *###***###***###…


Col. 9  Attribute or Group field: 동일한 그룹을 가진 모든 라인은 단일 항목으로 연결됨. 그룹 분야는 어려운데, 다음과 같은 다양한 독특한 방식으로 사용됨. 
- 갭 정렬과 같이 불연속 범위에 걸쳐있는 단일 시퀀스 피처를 그룹화하기 위해

- 이름으로 검색 할 수 있도록 피쳐의 이름을 지정하기 위해

- 주석에 하나 이상의 메모를 추가하기 위해

- 대체 이름을 추가하기 위해



GFF2의 문제점 : 
1. 피쳐의 중첩 레벨을 하나만 나타낼 수 있다는 것. 대체로 접합된 전사체가 여러 개인 유전자를 다룰 때 주로 문제가 되는데, GFF2는 유전자 → 전사체 → 엑손의 3 단계 계층 구조를 처리 할 수 ​​없음



보통 일련의 전사물을 선언하고 동일한 유전자에서 유래했음을 나타내는 유사한 이름을 부여함으로써 이 문제를 해결 
2. GFF2를 사용하여 스크립트 → 엑손과 같은 2 단계 계층 구조를 만들 수 있지만 계층 구조의 방향에 대한 개념이 없음. 따라서 엑손이 전사물의 하위 기능인지 또는 그 반대인지는 알 수 없음. 이것은 관계자를 정리하기 위해 “aggregator”를 사용해야한다는 것을 의미함. 이것은 큰 제한점이므로, GFF2 형식은 GFF3 형식 데이터베이스를 위해 더 이상 사용되지 않음





7. GTF (Gene Transfer format)
File format :     GTF

File extensions :     file.gtf

Example : 

AB000381 Twinscan  exon         150   200   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         300   401   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          380   401   .   +   0  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         501   650   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          501   650   .   +   2  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         700   800   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          700   707   .   +   2  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         900  1000   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  start_codon  380   382   .   +   0  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  stop_codon   708   710   .   +   0  gene_id "AB000381.000"; transcript_id "AB000381.000.1";
GTF는 GFF 파일과 형식이 동일하며, 유전자 / 전사 관련 기능을 설명하는 동일한 9 개의 필드가 있음.

그룹 / 속성 필드가 속성 목록으로 확장되었으며, 각 속성은 유형 / 값 쌍으로 구성됨. 속성은 세미콜론으로 끝나야하며 다음 속성과 정확히 하나의 공백으로 구분해야 함. 속성 목록은 두 가지 필수 속성으로 시작함



gene_id value : 서열의 유전자 소스에 대한 전역 고유 식별자 
transcript_id value : 예측된 전사물의 전역 고유 식별자
GTF 파일에 대한 설명은 다음에 잘 설명되어 있음 http://mblab.wustl.edu/GTF2.html  





