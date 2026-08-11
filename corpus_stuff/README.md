# Creating the Corpus
## Sources
We pull our corpus from three sources:
* [PerseusDL/canonical-greekLit](https://github.com/PerseusDL/canonical-greekLit) 
* [OpenGreekAndLatin/First1KGreek](https://github.com/OpenGreekAndLatin/First1KGreek)
* [telota/galen](https://github.com/telota/galen/tree/main)
 
In total, these combine to form a corpus of about 33 million Greek words. If you wish, you can use the [Scaife Viewer](https://scaife.perseus.org/) to view the works found in these repositories. (You can also do much more! Explore the Viewer!)

## CTS API
You could think of the CTS API as a way the works are structured and what calls you can make to the servers holding these works to 
retrieve them. Each work has its own Uniform Resource Name (URN) associated with it. 
### Main URN Components
For example, the Iliad has the following URN assigned to it: 
`urn:cts:greekLit:tlg0012.tlg001`. The string `tlg0012` denotes an _author_ (Homer), whereas `tlg001` denotes a _work_ (the 
Iliad). Sometimes, you could also specify the _edition_ you want to reference. For example, 
`urn:cts:greekLit:tlg0012.tlg001.perseus-grc2` specifies the `perseus-grc2` edition, whereas 
`urn:cts:greekLit:tlg0012.tlg001.perseus-eng3` specifies an English translation of the Iliad. From there, you can get the 
_citation_ of a passage in the work. For example, if you'd like to get the first seven lines of the first book of the Iliad, then 
you can request the passage with URN `urn:cts:greekLit:tlg0012.tlg001.perseus-grc2:1.1-1.7`.
### Reference Levels
Depending on the work, you can make more (or less) granular choices of passages. For example, 
`urn:cts:greekLit:tlg0012.tlg001.perseus-grc2:1-6` is assigned to everything in the first 6 books of the Iliad. Here, we say that 
the _reference level_ is 1, whereas the URN `urn:cts:greekLit:tlg0012.tlg001.perseus-grc2:1.1-1.7` implies a _reference level_ of
2. To see all possible citations of a fixed reference level, you can access the `https://scaife.perseus.org/library/{urn}/cts-api-xml/reffs/level={reference_level}` endpoint. Try it with the Illiad example! What's the highest reference level?

__Note:__ These reference levels do not necessarily mean the same thing across different works. For example, `1.1` could refer to
either Book 1 Line 1 or Book 1 Chapter 1, depending on the work.

## Explanation of Files
* `get_corpus.py`: This is the script that generates the corpus. It relies on multithreading, where each thread makes a call to
a CTS server to get portions of a work one at a time. To preserve the formatting of poems and other documents, we also include the line break character [LB] at the beginning of an appropriate line. 
* `consolidate_books.py`: Initially, the way `get_corpus.py` was intended to work was that each book of a work would be saved in a 
different text file. This was to be determined through the citation, e.g. `1.3` and `2.1` would both be passages from Book 1 and
Book 2 of the work. However, as noted above, sometimes the first number in the citation is not necessary the book number and 
could instead be a chapter number. Therefore, this script goes through all text files that correspond to the same work, and 
determines if there is a single one that is too short. If so, then it combines all of the text files corresponding to that work
into a single text file. The rest of the works are untouched, and now each text file should be big enough where we can get proper
training samples, but not too big where it's possible to sample a piece of text that spans across two different books of the same 
work.   
* `clean_corpus.py`: Removes Latin characters, and adds space between works and non-words characters.  
* `test_clean_corpora.py`: Small test for `clean_corpus.py`.
* `words_list.tsv`: This is the list of words that one of the previous FastText models "learnt" after we've cleaned a version of 
the corpus.