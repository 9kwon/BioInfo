## NGS를 위한 통상적인 pipeline 및 그 결과 파일 형식에 대한 정리 
##### 각 파일 포맷에 대한 구체적인 예시와 설명은 ["여기"](https://ssene.tistory.com/4 "생물 정보 파일 포맷 형식")를 클릭   


- FASTA (raw data generation)
- FASTQ (raw data generation, FASTA + quality score 또는 error rate)
- SAM (참고 염기 서열에 read alignment)
- BAM (이진 표현으로 축약된 SAM)
- VCF (유전 변이 추출)
- GFF (정보 표현. 염기 서열, 엑손, 인트론, 프로모터, 3 'UTR, 반복 요소 등의 모든 기능에 사용)
- GTF (정보 표현. 유전자 및 전사물 기록)



#### NGS data processing and variant calling PipeLine   

![pipeline의 예시](/pipeline.PNG)

* NGS data processing 과정에서 생성되는 파일이 FASTAQ 및 SAM/BAM 파일이고,
* variant discovery에서 생성되는 파일이 VCF 파일임   



### * FASTA
- 핵산 및 단백질의 뉴클레오티드 또는 아미노산 서열을 나타내는 간단한 방법으로 두 개의 최소 행이 있는 매우 기본적인 형식       


### * FASTAQ
- 서열과 품질 점수 (Q : phred quality score)를 그룹화하기 위해 Sanger Institute에서 개발했으며, fastq 파일에서 각 항목은 4 줄과 연결됨.

1 행: ‘@’문자로 시작하며 시퀀스 식별자 및 선택적 설명
2 행: 표준 1 문자 코드의 시퀀스
3 행: "+"문자로 시작하며 선택적으로 동일한 시퀀스 식별자 (및 추가 설명)가 다시 옴
4 행: 2 행의 시퀀스에 대한 품질 값(PHRED 척도)을 인코딩하며 시퀀스의 문자와 동일한 수의 기호를 포함해야 함 

~~~
@K00188:208:HFLNGBBXX:3:1101:1428:1508 
2:N:0:CTTGTAATAATAGGATCCCTTTTCCTGGAGCTGCCTTTAGGTAATGTAGTATCTNATNGACTGNCNCCANANGGCTAAAGT
+
AAAFFJJJJJJJJJJJJJJJJJFJJFJJJJJFJJJJJJJJJJJJJJJJ#FJ#JJJJF#F#FJJ#F#JJJFJJJJJ
~~~      


### * SAM
- read를 참조 시퀀스에 매핑 한 후 생성 되며, 헤더와 본문이 있는 탭으로 구분 된 텍스트 형식
- 헤더는 파일이 정렬 된 경우 버전 정보, 참조 순서 정보 등 SAM 파일에 대한 일반 정보를 보유함
- 정렬 레코드는 파일의 본문을 구성하며, 각 정렬 라인 / 레코드에는 필수 정렬 정보를 설명하는 11 개의 필수 필드가 있음
- 11개의 필드 값
![11개 필드](/field.png)

- 용어 정리
  - Template : 측정된 DNA 조각
  - Reads : 방법에 따라 템플릿이 하나 이상의 read를 생성할 수 있고, 이러한 read는 전체 템플릿 또는 해당 하위 섹션을 포괄할 수 있음
  동일한 템플릿에서 시작된 read는 템플릿의 다른 부분을 다루며, 템플릿 자체 또는 템플릿의 역보완(reverse complement)을 나타낼 수 있음
  - Segments : 각 read는 segment라고 불리는 영역을 할당받는 하나 이상의 정렬을 생성할 수 있음 
  
~~~
1:497:R:-272+13M17D24M 113 1 497 37 37M 15 100338662 0 CGGGTCTGACCTGAGGAGAACTGTGCTCCGCCTTCAG 0;==-==9;>>>>>=>>>>>>>>>>>=>>>>>>>>>> XT:A:U NM:i:0 SM:i:37 AM:i:0 X0:i:1 X1:i:0 XM:i:0 XO:i:0 XG:i:0 MD:Z:37 

19:20389:F:275+18M2D19M 99 1 17644 0 37M = 17919 314 TATGACTGCTAATAATACCTACACATGTTAGAACCAT >>>>>>>>>>>>>>>>>>>><<>>><<>>4::>>:<9 RG:Z:UM0098:1 XT:A:R NM:i:0 SM:i:0 AM:i:0 X0:i:4 X1:i:0 XM:i:0 XO:i:0 XG:i:0 MD:Z:37 

19:20389:F:275+18M2D19M 147 1 17919 0 18M2D19M = 17644 -314 GTAGTACCAACTGTAAGTCCTTATCTTCATACTTTGT ;44999;499<8<8<<<8<<><<<<><7<;<<<>><< XT:A:R NM:i:2 SM:i:0 AM:i:0 X0:i:4 X1:i:0 XM:i:0 XO:i:1 XG:i:2 MD:Z:18^CA19 

9:21597+10M2I25M:R:-209 83 1 21678 0 8M2I27M = 21469 -244 CACCACATCACATATACCAAGCCTGGCTGTGTCTTCT <;9<<5><<<<><<<>><<><>><9>><>>>9>>><> XT:A:R NM:i:2 SM:i:0 AM:i:0 X0:i:5 X1:i:0 XM:i:0 XO:i:1 XG:i:2 MD:Z:35
~~~        


### * BAM
- BAM (Binary Alignment / Map) 파일은 압축된 이진 버전의 Sequence Alignment / Map (SAM)
- 뉴클레오티드 서열 정렬의 컴팩트하고 색인 가능한 표현 
- SAM과 BAM 간의 데이터는 정확히 동일 
- 이진 BAM 파일은 크기가 작으며 정렬 파일을 저장하는데 이상적      


### * VCF
- VCF는 헤더(정보 VCF 버전, 샘플 등)가있는 텍스트 파일 형식이며, 데이터 라인이 파일 본문을 구성함
- HEADER: 메타 정보가 포함되며 ‘##’ 문자열 뒤에 포함됨.데이터 필드에 대한 자세한 설명을 위해 INFO, FILTER 및 FORMAT 항목을 포함하는 것이 좋음
  alternate allele, assembly field, Contig field, sample field, pedigree field와 같은 다른 정보도 포함 가능함
- DATA FIELD: 데이터 라인은 8개의 필수 열을 가짐 (#CHROM, POS, ID, REF, ALT, QUAL, FILTER, INFO) 

~~~
ileformat=VCFv4.2 
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
~~~        


### * GFF
- GFF2 -> GFF 3 (3가 nesting 구조에 적합한 최신 버전, 부모 태그에 대한 link가 특징)
- 단백질 코딩 유전자를 나타내는 가장 일반적인 방법은 소위 "three-level gene"임
최상위 수준은 유전자의 전사물(transcript)과 조절 인자(regulatory elements)를 묶는 "유전자" 유형의 feature이며, 이 수준 아래에는 "mRNA" 유형의 하나 이상의 전사물이 있음
이 수준은 프로모터 및 다른 시스 조절 인자(cis-regulatory elements)를 수용 할 수 있음
세 번째 수준에는 mRNA 전사체의 구성 요소, 가장 일반적으로 CDS 코딩 세그먼트 및 UTR이 있음
아래 예는 3개의 대안적으로 스플라이싱된 mRNA 전사체를 갖는 "EDEN"이라는 유전자를 나타내는 방법을 보여줌

~~~
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
~~~

- GFF의 9개 필수 열 (required field)
* Col. 1 Reference Sequence: 주석 좌표 시스템을 설정하는 데 사용되는 참조 시퀀스의 ID. 염색체 이름 또는 번호
* Col. 2 Source: 기능 주석이 파생되는 방법에 대한 설명
* Col. 3 Feature: "gene" 또는 "exon"과 같은 feature 이름
* Col. 4 Start: feature의 유전자적 시작
* Col. 5 End: feature의 유전자적 끝
* Col. 6 Score: 주석이 달린 피쳐에서 소스의 신뢰도를 일반적으로 나타내는 숫자 값
* Col. 7 Strand: 피처의 감지 가닥을 나타내는 필드 (watson, Crick, ?)
* Col. 8 Frame(GFF2 and GTF) or Phase(GFF3): "CDS" 유형의 피쳐에서 위상(phase)은 피처가 read 프레임을 참조하여 시작되는 위치(0, 1, 2)를 표현
* Col. 9  Attribute or Group field: 동일한 그룹을 가진 모든 라인은 단일 항목으로 연결됨      


### * GTF
- GTF는 GFF 파일과 형식이 동일하며, 유전자 / 전사 관련 기능을 설명하는 동일한 9 개의 필드가 있음
- 그룹 / 속성 필드가 속성 목록으로 확장되었으며, 각 속성은 유형 / 값 쌍으로 구성됨
- 속성은 세미콜론으로 끝나야하며 다음 속성과 정확히 하나의 공백으로 구분해야 함. 속성 목록은 두 가지 필수 속성으로 시작
- gene_id value : 서열의 유전자 소스에 대한 전역 고유 식별자 
- transcript_id value : 예측된 전사물의 전역 고유 식별자

~~~
AB000381 Twinscan  exon         150   200   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         300   401   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          380   401   .   +   0  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         501   650   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          501   650   .   +   2  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  exon         700   800   .   +   .  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
AB000381 Twinscan  CDS          700   707   .   +   2  gene_id "AB000381.000"; transcript_id "AB000381.000.1"; 
~~~




