<!-- 
NavPath: Academic Knowledge API
LinkLabel: Entity Attributes
Url: Academic-Knowledge-API/documentation/EntityAttributes
Weight: 60
-->

# Entity Attributes

Name	|Description	            |Type       | Operations
------- | ------------------------- | --------- | ----------------------------
Id		|Entity ID					|Int64		|Equals
Ti		|Paper title				|String		|Equals,<br/>StartsWith 	
Y		|Paper year					|Int32		|Equals,<br/>IsBetween
D		|Paper date					|Date		|Equals,<br/>IsBetween
CC		|Citation count				|Int32		|none  
AA.AuN	|Author name				|String		|Equals,<br/>StartsWith
AA.AuId	|Author ID					|Int64		|Equals
AA.AfN	|Author affiliation name	|String		|Equals,<br/>StartsWith
AA.AfId	|Author affiliation ID		|Int64		|Equals
F.FN	|Field of study name		|String		|Equals,<br/>StartsWith
F.FId	|Field of study ID			|Int64		|Equals
J.JN	|Journal name				|String		|Equals,<br/>StartsWith
J.Id	|Journal ID					|Int64		|Equals
C.CN	|Conference series name		|String		|Equals,<br/>StartsWith
C.Id	|Conference series ID		|Int64		|Equals
RId	    |Reference ID				|Int64		|Equals
W       |Words from paper title/abstract for full text search |String |Equals
E		|Extended metadata (see table below) |String |Equals  
		


## Extended Metadata Attributes ##

Name    | Description               
--------|---------------------------	
DN		| Display Name of the paper 
D		| Description 
S		| Sources - list of web sources of the paper, sorted by static rank
S.Ty	| Source Type (1:HTML, 2:Text, 3:PDF, 4:DOC, 5:PPT, 6:XLS, 7:PS)
S.U		| Source URL
VFN		| Venue Full Name - full name of the Journal or Conference
VSN		| Venue Short Name - short name of the Journal or Conference
V		| Volume - journal volume
I 		| Issue - journal issue
FP		| FirstPage - first page of paper
LP 		| LastPage - last page of paper
DOI		| Digital Object Identifier		
