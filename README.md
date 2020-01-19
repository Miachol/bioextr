<img src="https://img.shields.io/badge/lifecycle-experimental-orange.svg" alt="Life cycle: experimental"> <a href="https://godoc.org/github.com/openbiox/bioextr"><img src="https://godoc.org/github.com/openbiox/bioextr?status.svg" alt="GoDoc"></a>

## bioextr

[bioextr](https://github.com/openbiox/bioextr) is a simple command line tool to extract information from text or json files.

## Installation

```bash
# windows
wget https://github.com/openbiox/bioextr/releases/download/v0.1.0/bioextr.exe

# osx
wget https://github.com/openbiox/bioextr/releases/download/v0.1.0/bioextr_osx
mv bioextr_osx bioextr
chmod a+x bioextr

# linux
wget https://github.com/openbiox/bioextr/releases/download/v0.1.0/bioextr_linux64
mv bioextr_linux64 bioextr
chmod a+x bioextr

# get latest version
go get -u github.com/openbiox/bioextr
```

## Usage

### Text mining

- support calculate correlations between any keywords at the sentence level (PubMed)
- support extract URLs from PubMed and SRA abstract

```bash
# extract from pubmed abstract
bget api ncbi -q "Galectins control MTOR and AMPK in response to lysosomal damage to induce autophagy OR MTOR-independent autophagy induced by interrupted endoplasmic reticulum-mitochondrial Ca2+ communication: a dead end in cancer cells. OR The PARK10 gene USP24 is a negative regulator of autophagy and ULK1 protein stability OR Coordinate regulation of autophagy and the ubiquitin proteasome system by MTOR." | bioctl cvrt --xml2json pubmed - | bioextr --mode pubmed -w 'MTOR,AMPK,autophagy' --call-cor - > final.json

bget api ncbi -q "Galectins control MTOR and AMPK in response to lysosomal damage to induce autophagy OR MTOR-independent autophagy induced by interrupted endoplasmic reticulum-mitochondrial Ca2+ communication: a dead end in cancer cells. OR The PARK10 gene USP24 is a negative regulator of autophagy and ULK1 protein stability OR Coordinate regulation of autophagy and the ubiquitin proteasome system by MTOR." | bioctl cvrt --xml2json pubmed - > test0.json

for i in {1..100}
do
cp test0.json test${i}.json
done

bioextr test*json --mode pubmed -w 'MTOR,AMPK,autophagy' --call-cor -t 30 > final2.json

rm final.json final2.json test*json
	
# extract from sra json
bget api ncbi -d 'sra' -q PRJNA527714 | bioctl cvrt --xml2json sra - | bioextr --mode sra --call-cor -w "Chromatin,mouse" -
```

## Maintainer

- [@Jianfeng](https://github.com/Miachol)

## License

Academic Free License version 3.0

