---
title: "Tools in MicroData"
teaching: 0
exercises: 0
questions:
- ""
objectives:
- "Join a unique ID to a raw .csv with different input types."
- ""
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

## Use

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



 

