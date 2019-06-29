
The Hindi Parsing Shared Task (HPST) is being held along with the COLING workshop on Machine Translation and Parsing in Indian Languages (MTPIL-2012). As part of the shared task, a part of the dependency annotated Hindi Treebank (HTB) will be released to the participants for training, development and final evaluation. 

TASK
----
The Hindi parsing shared task is to assign labeled dependency structures by means of a fully automatic dependency parser. Some gold standard dependency structures against which systems are evaluated will be non-projective. A system that produces only projective structures will nevertheless be evaluated against the partially non-projective gold standard data itself. 

There are two evaluation tracks (gold standard and automatic) in the shared task and all the partcipating systems must participate in both the tracks. In these two tracks the information available in the input to the systems vary. In the gold standard track, the input to the system consists of sentence tokens with gold standard morphological analysis, part-of-speech tags, chunks and the additional features listed above. In the automatic track, the input to the system contains only the sentence token and the part-of-speech tags from an automatic tagger. In both the tracks, the parser must output the head and the corresponding dependency relation for each token in the input sentence. 

The teams are provided with training and development data containing gold standard morphological analysis (lemma, coarse POS tag, gender, number, person, vibhakti, tense-aspect-modality), part-of-speech tags, chunks, labeled dependency structures along with some additional features such as sentence type, sentence voice etc. Versions of training and development data containing gold standard dependency structures along with just the automatic POS tags for the tokens are also provided. 

The participants are free to use which ever version of the training and development data they want to build the parsers for both the tasks. The parser should be the same in both the tracks i.e. a team can not use a parser/algorithm/learner for one track and a different parser/algorithm/learner for the second track. Only the training data could change between the two tracks. 

The evaluation metrics are labeled attachment score and unlabeled attachment score reported separately for the two tracks. After the final evaluation in which scores of the systems on the test data are released, the teams must submit a report (6 page in COLING format) describing their approach and results. The papers with the interesting approaches and an informative error analysis are given a chance to present their work in the MTPIL-2012 workshop. The rest of the teams get their chance to present their work in a poster session.

DATA
----
A subset of the dependency annotated Hindi Treebank (HTB ver-0.5*) is released as part of the Hindi Parsing Shared Task-2012 (HPST-2012). HTB ver-0.5* is a multi-layered dependency treebank with morphological, part-of-speech and dependency annotations on sentences from news domain corpus acquired from ISI-Kolkata, India. During annotation, the dependency relations are only marked between chunks in the sentence and the words are annotated with POS tags and morphological analysis. The annotations are stored in the Shakti Standard Format (See $parent_dir/docs/ssf-guide.pdf for a detailed description of the format). An automatic tool is then used on the inter-chunk relations as a post-processing step to get the complete dependency tree between words. This is done by first identifying the head word in the chunk and then identifying the intra-chunk relations between words in the chunks. The expanded tree is also stored in SSF without losing the chunk information.

HTB ver-0.5* is an ongoing effort and a portion of it is being released with multi-fold validation on dependency POS and chunk annotations. Morphological analysis, however, has not been validated for errors and incosistencies. 

Train – 12041 sentences, 268,093 words
Devel – 1233 sentences, 26416 words

DATA FONT
---------

Though the original data is in UTF-8, it is also being released in wx notation (See $parent_dir/docs/wxroman.doc for description) for the sake of users who can not read devanagari script. The files in  with "*.utf8.*" are in utf-8 encoding and the files with "*.wx.*" are in wx notation. The evaluation data would also be released in both of them. 

DATA FORMAT
-----------
The data is released in two formats, Expanded SSF and CoNLL-X formats. For detailed introduction to SSF, please read $parent_dir/docs/ssf-guide.pdf and for an intro to the CoNLL format, go through the link http://ilk.uvt.nl/conll/#dataformat .

Below is a quick description of the two formats with relevance to HTB ver-0.5* data being released.

1. Shakti Standard Format (SSF)
   ----------------------------
-A sentence is wrapped in the XML tags <Sentence id="2"> </Sentence> with these two occurring in new lines.
-A sentence consists of one or more tokens, each starting in a new line.
-A token consists of four fields described in the table below. Fields are separated by a single tab character.
-Descrition of the four fields in expanded SSF of HTB ver-0.5* data:
1 ID
2 WORD_FORM
3 POS TAG
4 FEATURE STRUCTURE

A feature structure is denoted using the XML tag "fs". The attributes and values of "fs" are in the standard XML format with the attribute value pairs separated by a space. The value of an attribute is enclosed in single  quotes. Below is the list of attributes and descriptions of them.

	af  		Used to denote the abbreviated feature listing lemma, category, gender, number, person, 
			case, vibhakti and TAM (tense aspect modality) in a single value by separating them out 
			with a comma. 
			e.g. <fs af=’child,n,m,p,3,0,,’>
			The field for each attribute is at a fixed position and thus, in case, no value 
			is given for a particular attribute the field is left blank, e.g. last two fields 
			(vibhakti and TAM)in the above example.
	posn		Position of the token in the sentence in multiples of 10.
	name		Unique identifier to the token in the sentence. The value is generally the token 
			itself unless a token appears more than once in a sentence. In that case, the value
			of name would be "token1" or "token2" etc. for subsequent occurrences of it in the 
			sentence. A token gets a name only if it has a child.
	deprel		Used to denote the labeled dependency relation. It has two parts separated by a 
			colon (:). The first part is the dependency label and the second is the parent's 
			identifier (found as the value of the "name" attribute in the parent's feature 
			structure.) 
	chunkType 	The value has two elements separted by a colon (:) with the first 
			being whether the token is a head or child of the chunk and the second being 
			the unique identifier of the chunk the token belongs to. This identifier is 
			typically the chunk name followed by a sequence of digits such as NP2, NP, 
			VGF1 etc.
	chunkId 		Optional attribute listed for tokens whose chunkType is a 'head' of 
			some chunk id. This value of the attribute chunkId is the same as the 
			second part of the value (after a colon ":") of chunkType.
	stype 		Sentence type.
	voicetype 	Active or passive.


Example sentence in expanded SSF.
========================================================================
<Sentence id="2">
1   यह  DEM <fs af='यह,pn,any,sg,3,d,,' posn='10' drel='nmod__adj:खिताब' chunkType='child:NP' name='यह'>
2   खिताब NN  <fs af='खिताब,n,m,sg,3,d,0,0' drel='k2:पाने' posn='20' name='खिताब' chunkId='NP' chunkType='head:NP'>
3   पाने  VM  <fs af='पा,v,any,sg,any,o,ना_वाला,nA' drel='nmod:सोनल' posn='30' vpos='tam_2' name='पाने' chunkId='VGNN' chunkType='head:VGNN'>
4   वाली  PSP <fs af='वाला,psp,f,sg,,d,,' posn='40' drel='lwg__psp:पाने' chunkType='child:VGNN' name='वाली'>
5   सोनल NNP <fs af='सोनल,n,f,sg,3,d,0,0' drel='k1:है' posn='50' name='सोनल' chunkId='NP2' chunkType='head:NP2'>
6   देश  NN  <fs af='देश,n,m,sg,3,o,0_का,0' drel='r6:लड़की' posn='60' vpos='vib_2' name='देश' chunkId='NP3' chunkType='head:NP3'>
7   की   PSP <fs af='का,psp,f,sg,,d,,' posn='70' drel='lwg__psp:देश' chunkType='child:NP3' name='की'>
8   पहली QO  <fs af='पहला,num,f,sg,,d,,' posn='80' drel='nmod__adj:लड़की' chunkType='child:NP4' name='पहली'>
9   लड़की NN  <fs af='लडकी,n,f,sg,3,d,0,0' drel='k1s:है' posn='90' name='लड़की' chunkId='NP4' chunkType='head:NP4'>
10  है   VM  <fs af='है,v,any,sg,3,,है,hE' stype='declarative' posn='100' voicetype='active' name='है' chunkId='VGF' chunkType='head:VGF'>
11  ।   SYM <fs af='।,punc,,,,,,' drel='rsym:है' posn='110' name='।' chunkId='BLK' chunkType='head:BLK'>
</Sentence>
========================================================================
Note that the above example is in UTF-8.

** APIs to access SSF structure are provided in $parent_dir/docs/ssf-apis/

2. CoNLL Format
   ------------
An example sentence is listed after the format description.

-Data contains sentences separated by a blank line. 
-A sentence consists of one or more tokens, each starting on a new line.
-A token consists of ten fields described in the table below. Fields are separated by a single tab character. Space/blank characters are not allowed within fields.
-Descrition of the ten fields in CoNLL format of HTB ver-0.5* data:
1 ID
2 WORD_FORM
3 LEMMA
4 FINE POS TAG
5 COARSE POS TAG
6 FEATURES
	-- These are the unordered set of mophological and syntactic features in the 
	fourth field in Shakti Standard Format. The features are separated by a vertical
	bar (|). Each feature has an attribute and value separated by a hyphen (-).
	The attributes for each token are 
		lex (the lemma of the token), 
		cat (the coarse grained POS tag), 
		gend (gender), 
		num (number), 
		pers (person), 
		case (case),
		vib (vibhakti i.e. the post position), 
		tam (tense aspect modality), 
		chunkType (the value has two elements separted by a colon (:) with the first 
			being whether the token is a head or child of the chunk and the second being 
			the unique identifier of the chunk the token belongs to. This identifier is 
			typically the chunk name followed by a sequence of digits such as NP2, NP, 
			VGF1 etc.)
		chunkId (optional attribute listed for tokens whose chunkType is a 'head' of 
			some chunk id. This value of the attribute chunkId is the same as the 
			second part of the value (after a colon ":") of chunkType)
		stype (sentence type)
		voicetype (active or passive)
7 HEAD 
8 DEPREL
9 '_'
10 '_'

Example sentence in CoNLL format:
========================================================================
1   xUwAvAsa    xUwAvAsa    XC  n   lex-xUwAvAsa|cat-n|gend-m|num-sg|pers-3|case-d|vib-0|tam-0|posn-10|chunkType-child:NP|name-xUwAvAsa 2   mod _   _
2   aXikAriyoM  aXikArI NN  n   lex-aXikArI|cat-n|gend-m|num-pl|pers-3|case-o|vib-0_ne|tam-0|posn-20|vpos-vib_3|name-aXikAriyoM|chunkId-NP|chunkType-head:NP    8   k1  _   _
3   ne  ne  PSP psp lex-ne|cat-psp|gend-|num-|pers-|case-|vib-|tam-|posn-30|chunkType-child:NP|name-ne  2   lwg__psp    _   _
4   use vaha    PRP pn  lex-vaha|cat-pn|gend-any|num-sg|pers-3|case-o|vib-ko|tam-ko|posn-40|name-use|chunkId-NP2|chunkType-head:NP2 8   k2  _   _
5   acCI    acCA    JJ  adj lex-acCA|cat-adj|gend-any|num-any|pers-|case-o|vib-|tam-|posn-50|chunkType-child:NP3|name-acCI  6   nmod__adj   _   _
6   sehawa  sehawa  NN  n   lex-sehawa|cat-n|gend-f|num-sg|pers-3|case-o|vib-0_meM|tam-0|posn-60|vpos-vib_3|name-sehawa|chunkId-NP3|chunkType-head:NP3  8   k7  _   _
7   meM meM PSP psp lex-meM|cat-psp|gend-|num-|pers-|case-|vib-|tam-|posn-70|chunkType-child:NP3|name-meM   6   lwg__psp    _   _
8   pAyA    pA  VM  v   lex-pA|cat-v|gend-m|num-sg|pers-3|case-|vib-yA|tam-yA|stype-declarative|posn-80|voicetype-active|name-pAyA|chunkId-VGF|chunkType-head:VGF   0   main    _   _
9   .   .   SYM punc    lex-.|cat-punc|gend-|num-|pers-|case-|vib-|tam-|posn-90|chunkType-child:VGF|name-.  8   rsym    _   _
========================================================================
Note that the above example is in wx-notation.


LICENSE
-------

The dependency treebank being released as part of the Hindi parsing shared task-2012 is a part of of an ongoing effort into the creation of the Hindi Treebank (HTB). Since HTB is a work in progress, IIIT-Hyderabad and all the agencies involved in creation of HTB do not warrant the accuracy, completeness, currentness or fitness for a particular purpose of the information contained in HTB. This data is being distributed for free for research purpose only.

The user agrees to not distribute the data or part of them either in original or modified form. Any publication reporting the work done using this data should cite the following reference:

By downloading the data, you agree to abide by the above rules and conditions.

DATA RELEASE
-------

Training and development data with both gold standard and automatic annotations are released in CoNLL format and Shakti Standard Format. The data will also be released in UTf-8 encoding as well as wx notation. Each of the training and development file would be available in four offerings (auto|gold and utf8|wx) in both SSF and conll format.

The participants should make a choice from the two font schemes and also from the two formats (SSF|CoNLL) for their work.  

HTB-ver0.5*/
 |
 |_ssf/
 |  |__utf8/
 |  |   |__train/
 |  |   |    |__train-htb-ver0.5*.auto.utf8.ssf
 |  |   |    |__train-htb-ver0.5*.gold.utf8.ssf
 |  |   |
 |  |   |__devel/
 |  |   |    |__devel-htb-ver0.5*.auto.utf8.ssf
 |  |   |    |__devel-htb-ver0.5*.gold.utf8.ssf
 |  |   |
 |  |   |__test/
 |  |        |__unanot-test-htb-ver0.5*.auto.utf8.ssf +
 |  |        |__unanot-test-htb-ver0.5*.gold.utf8.ssf +
 |	|
 |  |__wx/
 |      |__train/
 |      |    |__train-htb-ver0.5*.auto.wx.ssf
 |      |    |__train-htb-ver0.5*.gold.wx.ssf
 |      |
 |      |__devel/
 |      |    |__devel-htb-ver0.5*.auto.wx.ssf
 |      |    |__devel-htb-ver0.5*.gold.wx.ssf
 |      |
 |      |__test/
 |           |__unanot-test-htb-ver0.5*.auto.wx.ssf +
 |           |__unanot-test-htb-ver0.5*.gold.wx.ssf +
 |
 |_conll/
    |__utf8/
    |   |__train/
    |   |    |__train-htb-ver0.5*.auto.utf8.conll
    |   |    |__train-htb-ver0.5*.gold.utf8.conll
    |   |
    |   |__devel/
    |   |    |__devel-htb-ver0.5*.auto.utf8.conll
    |   |    |__devel-htb-ver0.5*.gold.utf8.conll
	|   |
    |   |__test/
    |        |__unanot-test-htb-ver0.5*.auto.utf8.conll +
    |        |__unanot-test-htb-ver0.5*.gold.utf8.conll +
	|
    |__wx/
        |__train/
        |    |__train-htb-ver0.5*.auto.wx.conll
        |    |__train-htb-ver0.5*.gold.wx.conll
        |
        |__devel/
        |    |__devel-htb-ver0.5*.auto.wx.conll
        |    |__devel-htb-ver0.5*.gold.wx.conll
        |
        |__test/
             |__unanot-test-htb-ver0.5*.auto.wx.conll +
             |__unanot-test-htb-ver0.5*.gold.wx.conll +
	

+ Evaluation data will be released on the dates given below. 

DOCUMENTATION
--------------------------
HPST-2012/
   |__ docs/
   |        |__README.txt  # Readme file with task description, data description etc.
   |        |__ ssf-guide.pdf
   |        |__ ssf-api/           # SSF APIs in C, Java and Python
   |        |__wxroman.doc   # Description of the wx notation
   |
   |__HTB-ver0.5/
            |__docs/
                    |__HTB-Guidelines-ver2.5.doc   # Treebank guidelines 
                    |__Appendix-10.1-Morph-specification.pdf
                    |__Appendix-10.2-SSF-Guide.pdf
                    |__Appendix-10.3-Chunk-POS-Annotaion-Guidelines.doc
                    |__Appendix-10.4-List-POS-Chunk-Dependency-Relations.pdf

ACKNOWLEDGEMENTS
----------------
We would like to thank Vishnu Raghumurthy, Jayendra Rakesh, Preeti Pradhan, Nandini Upasani, Narendra Annamaneni, Dipti Misra Sharma and others for helping us during the validation process and the user studies. The treebank  work is supported by the NSF grant (Award Number: CNS 0751202; CFDA Number:  47.070). Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.


CONTACT
-------
Prashanth Mannem <prashanth@research.iiit.ac.in>
