freetext-matching-algorithm-lookups
===================================

Lookup tables for the Freetext Matching Algorithm, a natural language processing system for clinical text.

## 2of4brif

A list of British English words from http://wordlist.sourceforge.net/

## alternateterms

Exact synonyms for native or virtual Read terms, which assist in the matching but are not returned as output.

Format: Tab-separated text file with no quotes, sorted by medcode

* medcode -- unique identifier for the term, starting from 600000
* stdterm -- lower case term to match, with one space before and after the term, one space between each pair of words and no punctuation
* attrstring -- a string with as many characters as the number of words in stdterm, stating how each word should be interpreted:
    * T -- true
    * F -- false
    * I -- ignorable
    * O -- option
* linkto -- medcode of the native or virtual Read term that is returned by the algorithm if this term is matched
* comment

## attributes

Patterns of up to 5 words with conditions on punctuation, for detection of context and laboratory results.

Format: Tab-separated text file with no quotes, sorted by order

* order -- sort order (lowest to highest). Any additional entries must have an appropriate sort order, using decimals as needed so that the order of existing entries does not need to change
* w1 -- expression specifying which word to match. A number of options can be supplied separated by |. Examples:
    * * any word
    * thisword -- specific word, 'thisword'
    * this|that|[NUMB] -- either 'this', 'that' or a number
    * 2 -- specific number: 2
    * [CLIN] -- a word which might be part of a Read term
    * [IGNO] -- an ignorable word (a word in the ignore list)
    * [NUMB] -- a number or 'normal' / 'abnormal'
    * [NUMB_70_230] -- a number in a defined range, in this case between 70 and 230
    * [DATE] -- date in any format
    * [DATE_full] -- full date
    * [DATE_year] -- year
    * [DURA] -- duration in any format
    * [DURA_wks_] -- duration in weeks (other options are DURA_days, DURA_mths)
    * [ATTR attribute] -- any word with the specified attribute
* p1 -- one or more characters specifying which punctuation characters (in any order) can be found after the word for it to match. For example, if the pattern is '_:=' then ':', '=', ':=' or no punctuation would be allowed. Special codes:
    * * any punctuation or blank
    * _ no punctuation
* w2 ... p5 -- alternating word and punctuation, to define a pattern of up to 5 words
* a1 ... a5 -- context attribute to set for each word in the pattern. The following special codes can also be used:
    * anon -- anonymise; do not analyse this part of the text (e.g. if it may contain the name of a doctor, patient or hospital)
    * ignore -- ignore
    * normalrange -- ignore any following lab values unless they have their own attribute
    * possiblity -- ignore any following diagnoses unless they have their own attribute
    * _ (underscore) -- Retain current attribute
    * . (full stop) -- set attribute to blank
    * DATATYPE attribute -- set attribute and data type (e.g. LABS inr, DURA_wks_ followup)
* death_only -- TRUE for attributes which are only relevant to texts associated with death, FALSE otherwise
* comment

## checkterms

Phrases which must be present or must not be present in the text for particular medcodes to be valid. This may be used for diagnoses which are commonly stated in the context of screening or immunisation, or for Read terms which are commonly extracted using abbreviations which are only valid in particular contexts. A medcode can only have 'qualifying' or 'dequalifying' phrases; it does not make sense to have both.

Format: Tab-separated text file with no quotes, sorted by medcode

* medcode -- unique identifier for a Read term
* qualify -- lower case comma separated word or phrase fragments which are necessary for the Read term to be valid
* dequalify -- lower case comma separated word or phrase fragments which invalidate the Read term

## ignore

Words or phrases which can be omitted without significantly altering the meaning of most Read terms or clinical text phrases.

Format: lower case words or phrases, with one space between words and no punctuation, sorted alphabetically

## ignorephrase

Verbatim semi-structured text phrases which may appear in free text in Vision systems. START_ is used to match the beginning of the text.

Format: words or phrases with punctuation, case sensitive

## nativeterms

Read terms in the Clinical Practice Research Datalink (www.cprd.com) Read dictionary

Format: Tab-separated text file with no quotes, sorted by medcode

* medcode -- unique identifier for the term, starting from 1
* readcode -- 7-character Read code, unique for each term (for reference, not used by program)
* term -- Read term (for reference, not used by program)
* stdterm -- standardised lower case version of Read term, with one space before and after the term, one space between each pair of words and no punctuation
* attrstring -- a string with as many characters as the number of words in stdterm, stating how each word should be interpreted:
    * T -- true
    * F -- false
    * I -- ignorable
    * O -- option
* include -- TRUE if the program is permitted to map to the term, FALSE otherwise.
* type -- a single character or blank, denoting the category of Read term in order to trigger the appropriate analysis mode:
    * D -- death; allow detection of cause of death
    * L -- laboratory result
    * M -- Read diagnosis term
    * N -- test result which may be qualitative; the result may be 'normal' or 'abnormal'
    * P -- pregnancy term; numbers such as 28/40 are interpreted as gestational age
    * S -- sick note; duration may be state
    * T -- date or time
* comment

## synonyms

Words or phrases which may be matched in Read terms and the original free text

Format: Tab-separated text file with no quotes, sorted by text, then read, then priority

* text -- word or phrase in the free text
* read -- word or phrase in a Read term
* priority -- a number between 1 and 5:
    1 -- loosely associated (s2 wider than s1) e.g. foot (is a part of) = lower limb
    2 -- non-standard abbreviation or distorted form; possible one-way match (read phrase broader than text phrase)
        e.g. rsi = repetitive strain injury
    3 --  moderate match e.g. b pne = bronchopneumonia; carcinoma (is a type of) = malignant neoplasm
    4 -- almost exact match e.g. cancer = malignant neoplasm
    5 -- exact match e.g. chronic obstructive pulmonary disease = copd
    -100 -- opposites e.g. left / right
* comment

## virtualterms

Terms created to code useful concepts in the output for which there are no current Read terms

Format: Tab-separated text file with no quotes, sorted by medcode

* medcode -- unique identifier for the term, starting from 500000
* term -- term description
* stdterm -- standardised lower case version of term, with one space before and after the term, one space between each pair of words and no punctuation
* attrstring -- a string with as many characters as the number of words in stdterm, stating how each word should be interpreted:
    * T -- true
    * F -- false
    * I -- ignorable
    * O -- option
* comment
