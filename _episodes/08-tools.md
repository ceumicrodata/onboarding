---
title: "Tools in MicroData"
teaching: 0
exercises: 0
questions:
- ""
objectives:
- "Join a unique ID to a raw .csv with different input types."
- "Choose the right cut offs and good matches"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

{% include links.md %}

# The problem

There are lots of occasions when we don’t have a unique ID for a raw input data. 
An input data could be firm name, person name, governmental institution, foundation, association .etc. 
Firm and person names also could be foreign ones. 

We are continuously developing tools to identify these inputs and join a unique ID to them.  

# Firm name search tool

Firm name search tool merges the eight-digit registration number (first 8 digits of tax number) to a Hungarian firm name.
You can find, among others, the building and installing methods on github:

<https://github.com/ceumicrodata/firm_name_search>

## Use of the tool

Requirements:
- Python2 and the tool must be available on the PATH
- a proprietary database index file (available only to members of CEU MicroData)

```
name-to-taxids-YYYY-MM-DD "firm name" input.csv output.csv
```

where "firm name" is the field name for firm name in `input.csv` and there is an index file in the current directory with name `complex_firms.sqlite`.

The tool provides command line help, so for further details run 

```
name-to-taxids-YYYY-MM-DD -h
```
`FirmFinder.find_complex()` expects a single unicode firm name parameter which it will resolve to a match object with at least these attributes:
- `org_score`
- `text_score`
- `found_name`
- `tax_id`

### An example how to run firm name search tool in python2

```
$ python name-to-taxids-20161004 name temp/distinct_firms.csv temp/distinct_firms_fname.csv --index 'input/firm-name-index/complex_firms.sqlite'
```
{: .bash}

You can see that you have to add the whitelist path manually. 

## The meaning of the outcome and how to choose the proper cut off scores

The tool outcomes and scoring system are based on Hungarian legal forms. If an input data has valid legal form then more likely a Hungarian company that not.

<https://www.ksh.hu/gfo_eng_menu>

A good match is very much dependent on how good the input data is. 
If we pre-filter the data and for example drop person names before we run the tool we can get good matches on lower text_scores.

```
        Score meaning	 
   org_score  text_score     meaning
   -20	        -20        No results.
   -10	        -10        Too much results. 
    -1	     0 <= x < 1	   The legal form doesn’t match, but the input and found names have one. 
    -1	          1        The firm name matches but the legal form doesn’t match. 
     0	     0 <= x < 1	   Only the input data have legal form.  (Input misspelling error)
     0	          1        Only the input data have legal form but the firm name matches. 
     1	     0 <= x < 1	   Only the found name have legal form.
     1	          1        In the input data NO legal form but the firm name matches. 
     2	     0 <= x < 1	   The legal forms are matching but the firm names not. 
     2	          1        Perfect match.
```

Can be said generally that most of the possible matches will be in `org_score==2 and text_score 0 <= x < 1` category. 
If a data is not very dirty usually matches bigger than `0.8` org_score could be possible good ones. 
You must have to adjust the good match cut offs in every category, every time when you run the tool on a new input. 

# PIR name search tool

Pir name search tool is developed for identify Hungarian state organizations by name. 
Pir number is the registration number of budgetary institutions in the Financial Information System at Hungarian State Treasury.

There is an online platform to find the PIR numbers one by one. 

http://www.allamkincstar.gov.hu/hu/ext/torzskonyv

The PIR search command line tool requires Python 3.6+.
Input: utf-8 encoded CSV file
Output: utf-8 encoded CSV file, same fields as in input with additional fields for "official data"

https://github.com/ceumicrodata/pir_search/releases/tag/v0.8.0

This release is the first, that requires an external index file to work with. You can find this index.json file in the pir-index beads.
The index file was separated, because it enables match quality to improve without new releases.

The match precision can be greatly improved by providing optional extra information besides organization name:

- settlement
- date

An extra tuning parameter is introduced with --idf-shift which tweaks the matcher's sensitivity to rare trigrams.
Its default value might not be optimal, it changes match quality.
Attached files are binary releases for all 3 major platforms: pir_search.cmd is for Windows, pir_search (without extension) is for unix-like systems (e.g. Linux and Mac)

## An example how to run pir name search tool in python3

```
Run from python3 with settlement option

python3 pir_search-0.8.0 input/pir-index/index.json name temp/distinct_firms.csv temp/distinct_firms_pname.csv --settlement settlement --hun-stop-words \
--pir pir_d --score pir_score_d --match_error pir_err_d --taxid pir_taxid_d --pir-settlement pir_settlement_d \
--name pir_name_d --keep-ambiguous

Run from python3 with settlement option and idf-shift 100 and extramatches

python3 pir_search-0.8.0 input/pir-index/index.json name temp/distinct_firms.csv temp/distinct_firms_pname_extra.csv--settlement settlement --hun-stop-words \
--idf-shift 100 --extramatches
```
{: .bash}

Pir_score==1 and pir_err==0 is a perfect match. 
The pir_score output could be between 0 <= x < 1.

The bigger the pir_err the match is more likely wrong. 
`Pir score bigger than 0.8 and pir_err<0.8 are potentially good matches`. 

You must have to adjust the good match cut offs in every category, every time when you run the tool on a new input. 

# Complexweb

The Complexweb is and internal searchable version of the raw Complex Registry Court database.

You can find downloadable official balance and income statements from e-beszámolo.hu:

https://e-beszamolo.im.gov.hu/oldal/kezdolap

You can easily find firm is you change the tax_id or ceg_id in the html column.

```
Example pages by tax_id

http://complexweb.microdata.servers.ceu.hu/cegs_by_tax_id/12345678 to 
http://complexweb.microdata.servers.ceu.hu/cegs_by_tax_id/12345679

Example pages by ceg_id

http://complexweb.microdata.servers.ceu.hu/ceg/0101234567 to
http://complexweb.microdata.servers.ceu.hu/ceg/0101234568
```
{: .bash}

You can write Postgre SQL queries to join tables and search in Complexweb.

<https://www.postgresql.org/docs/13/index.html>

```
Examples

* Count not null ceg_id from rovat 109 which is KFT

select count(distinct(ceg_id)) from rovat_109-- where cgjsz is not null

* Select a string part from a rovat 

select * from rovat_99 where szoveg like '%%Összeolvadás%%'
select ceg_id from rovat_3 where nev like '%%nyrt%%' or nev like '%%NYRT%%' or nev like '%%Nyrt%%'

* Select a string part from a rovat order and limit

select ceg_id from rovat_99 where szoveg like '%%átalakulás%%' and szoveg not like '%%való átalakulását határozta el%%' order by random() limit 20

* Select different variables from different rovats with join. 
where a tax_id is xxx 
AND létszám is xxx or datum is somethin 
-- means that line is not executing

-- explain
SELECT ceg_id, letsz, rovat_0.adosz, nev, datum, tkod08 -- * 
FROM
  rovat_0
  join rovat_99003 using (ceg_id)
  join rovat_99018 using (ceg_id)
  join rovat_8     using (ceg_id)
where 
--   rovat_0.adosz like '11502583%%'
--   rovat_0.adosz like '1150%%'
--   rovat_99003.letsz ~ '^(1[1-5]|23)$' 
     rovat_99003.letsz ~ '^13..$'
 AND rovat_8.alrovat_id = 1
 AND left(coalesce(rovat_8.datum, ''), 4) = '2006'
 AND rovat_99018.tkod08 like '77%%'


* Select rovats and join by ceg_id by the help of with

-- explain
with
    all_firms as (select left(adosz, 8) taxid8, ceg_id from rovat_0),
    more_than_one_ceg as (select taxid8 from all_firms group by taxid8 having count(*) > 1),
    ignored_taxid8 as (select distinct taxid8 from more_than_one_ceg join all_firms using (taxid8) join rovat_93 using (ceg_id)),
    hirdetmeny as (select distinct taxid8 from more_than_one_ceg join all_firms using (taxid8) join rovat_99 using (ceg_id))
 
(select taxid8 from more_than_one_ceg) intersect (select taxid8 from hirdetmeny) except (select taxid8 from ignored_taxid8 ) 
limit 10
;
```
