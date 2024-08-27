# Final assignment submission

* Course: Grammar Development

* Due date: 30.8.2024

* Term: Summer term 2024

* Instructors: Mark-Matthias Zymla and Kengatharaiyer Sarveswaran

* Institution: University of Konstanz

## Contained files
The file TODO: _grammar\_19.lfg_ contains a simple grammar that parses Spanish sentences. A selection of sentences can be found in TODO: _ts.lfg_.

## Phenomena and implementation
The grammar accounts for _two_ phenomena that distinguish the Spanish from the English language: 
* Pro-drop: The subject may be omitted from surface representation of a sentence. 
    
* Gender and Number Agreement of determiners, pronouns, adjectives and nouns.

In Pro-drop sentences, the subject can be usually inferred semantically, e.g. from the preceding context. Verbs are encoded for the features Number and Person, and thus allow for the reference to the real world entities. 
Example: 
1. Overt subject: La (Det S) mujer ("woman", S) come (eat, V:3PSg) el (Det Object) churro (Object).
2. Omitted subject: Come (eat, V:3PSg) el (Det Object) churro (Object).

I chose this phenomenon because it is crucial to understanding Spanish sentences. It is important to implement it in a grammar specific to the language, since it does not exist in English. Consequently, a similar sentence in English (sentence 4. marked with an asterisk) would fail to be parsed. Example: 
3. The woman eats the churro.
4. * Eats the chrurro. 

## OT-markers

With OT-markers certain rules, and thus constructions, templates, or
lexical items can be preferred or dispreferred. OT-markers reduce the number of solutions.
The following preferences were implemented:

* _+cat_

* _+drop_

TODO (challenge or OT mark): I implemented an OT-marker _+cat_ that is supposed to choose the postverbal over the prenominal position for adjectives. It would prefer the construction "comida rica" over "rica comida". The first option is more common in the Spanish language, since prenominal adjectives either tend to be associated with a more subjective reading or carry a distinct meaning than the same phrase with a postverbal adjective.
In the latter case, both sentences are correct, as shown in the famous example of the two readings of "An old friend" in 5a and 5b:

5a. Una amiga vieja. (Meaning: A friend of old age.)

5b. Una vieja amiga. (Meaning: An friend known for a long time.)

TODO: Furthermore, I implemented an OT-marker _+drop_. It chooses a sentence without a personal pronoun over a sentence with an overt personal pronoun, because the encoding of Number and Person on the verb make the personal pronoun mostly redundant. The parse in example 6. would be preferred over example 7., only if the referent of the pronoun "ella" has been previously introduced:

6. Come (eat, V:3PSg) el churro.
7. Ella (Pron:3PSgFem) come (eat, V:3PSg) el churro.

Methodically, these sentences can be implemented with an empty node that carries the features of the verb it belongs to.  Thus, the sentence with the omitted subject behaves like an imperative sentence in English. To account for the phenomenon, I created a rule "Sdrop" which has the same structure as the "Simp" rule in previous English grammars featured in the Grammar Development course. However, in imperative sentences, the implicit subject is always in second person. Since pro-drop can be used with any person (1, 2, 3), this restriction not featured in the present Spanish grammar.


The second phenomenon constitutes the Gender and Number Agreement. While Gender Agreement not exist in English, it affects adjectives, nouns, pronouns and determiners in Spanish. Any Part-Of-Speech governed by the NP must have the same Gender and Number as the noun. This can be observed with the objects "plato" (dish) and "comida" (food) in the following examples from the testsuite:

8.  Ella come el (DetSgMasc) plat-o (NSgMasc) delicios-o (AdjSgMasc).

9. Ella come la (DetSgFem) comid-a (NSgFem) delicios-a (AdjSgFem).

10. Ella come l-os (DetPlMasc) plat-os (NPlMasc) delicios-os (AdjPlMasc).

11. Ella come l-as (DetPlFem) comid-as (NPlFem) delicios-as (AdjPlFem).

A challenge that remains is, that adjectives may occur before or after the noun they are governed by. The present grammar has not implemented a working OT-mark that prefers one or the other reading, which could be implemented in the future. Critically, even sentences like 12., with the same adjective in both pre- and postverbal position can be parsed with the grammar, although they are ungrammatical in Spanish: 

12. Los deliciosos platos deliciosos.

Another case can be described as the following: When two _different_ adjectives are used, it can be perceived more natural to fill both adjective positions, before and after the noun. This intensifies, when one adjective is perceived more objective ("blanco" = white) than the other ("rico" = tasty). Thus sentence 13. is acceptable, although 12. is not.

13. El blanco (Adj objective) churro rico (Adj subjective).

## Testsuite 

Along with _grammar\_19.lfg_ , a testsuite _ts.lfg_ contating 14 TODO sentences was submitted. It showcases sentences that can be parsed in the first sentences. The second part shows sentences that are ungrammatical and cannot be parsed. To highlight the remaining challenges mentioned above, the last sentences in the testfile are the ones that could be parsed although they are grammatically incorrect.

## Other files
No files containing templates have been submitted, in order to keep the implications of the Spanish grammar traceable.