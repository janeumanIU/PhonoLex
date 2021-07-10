# PhonoLex
__Jared Neumann__ <br>
__janeuman@iu.edu__

### Description
PhonoLex is an application (in progress) that allows users to write phonological queries that return lists of words satisfying that phonology. Word-level features such as character and phoneme length, number of syllables, the presence of diphthongs, and the frequency of the potential matches, can be combined with phoneme-level features to generate those lists. Phoneme-level features include all manners of articulation, and any number of these features can be combined in a particular order to create patterns. Three options for the mode of matching are available: users can find their patterns starting from the beginning of a word (STARTS_WITH), the end of a word (ENDS_WITH), or anywhere (CONTAINS). 
<br><br>
The initial use-case and motivation for this project was generating phonologically precise word-lists for targeted speech-language pathology therapies.

### Data
The data folder includes four files: cmu.json, features.json, commonlemmas.txt, and commonwords.txt. 
#### *cmu.json*
This file contains a json version of the [CMU Pronouncing Dictionary][1]. It includes a dictionary of English vocabulary terms as keys and an ordered list of phonemes with stress indicated. There are approximately 135k words, some of which are represented more than once with alternate proncunciations.
<details>
  <summary>Vocabulary Example</summary>
  
| WORD |  0  |  1  |  2  |  3  |  4  |  5  |
|:-----|:---:|:---:|:---:|:---:|:---:|:---:|
|banana|  B  | AH0 |  N  | AE1 |  N  | AH0 |
</details>

#### *features.json*
This file maps the ARPAbet symbols for phonemes used in the CMU Pronouncing Dictionary to their corresponding phonological features. These features were derived from the definitions of those symbols. Several features are described, for example:
<details>
  <summary>Feature Example</summary>
  
|    FEATURE   | 'IH' |
|:-------------|-----:|
|TYPE          | V    |
|HEIGHT        | 0.2  |
|DEPTH         | 0.75 |
|ROUNDED       | 0    |
|RHOTIC        | 1    |
|STOP          | None |
|VOICE         | None |
|BILABIAL      | None |
|AFFRICATE     | None |
|ALVEOPALATAL  | None |
|ALVEOLAR      | None |
|FRICATIVE     | None |
|DENTAL        | None |
|LABIODENTAL   | None |
|VELAR         | None |
|LATERAL       | 0    |
|POSTALVEOLAR  | None |
|NASAL         | None |
|LABIOVELAR    | None |
|PALATAL       | None |
|GLIDE         | None |
|GLOTTAL       | None |
</details>

The values may have the following data types: string (for TYPE, i.e., vowel or consonant), float (for all numerical values, even those that are binary), None (for the cases in which a feature is not relevant/possible), and list (for ranges of values as in the case of diphthongs or search queries). Numerical values were derived in two ways: binary values come from the simple presence or absence of the feature, e.g., RHOTIC; other values come from the relative distance of a feature on a continuum. Continuous features are typically described as discrete values that divide a continuum. In the case of HEIGHT, this can be anywhere from 3 to 7 values. Here, 6 values are possible (0.0, 0.2, 0.4, 0.6, 0.8, 1.0).

#### *commonwords.txt*
This file contains 5027 of the most common words in English derived from the [Corpus of Contemporary American English (COCA)][2] 2020 data. The original lists were obtained from www.wordfrequency.info. This particular list contains words and their various forms that also made the top 5027. Duplicates were removed and a new file was generated by cross-referencing the CMU vocabulary (so phonetic descriptions could be obtained). Specifying this file allows the user to avoid obscure results, although there is a smaller *unique* vocabulary than in the next file.

#### *commonlemmas.txt*
This file contains 4369 of the most common lemmas in English derived from the same corpus. Lemmas are the so-called 'dictionary' form of the word, so the list contains a richer unique vocabulary, albeit fewer words altogether. Again, duplicates were removed and the included list has been cross-referenced with the CMU vocabulary.

### Functionality
Currently, there is only the core Phonology class. If you have data in the same format as the available data, an instance can be created that uses it. Otherwise, the defaults will be used. The only dependencies are json for reading the files and pandas for constructing and displaying the description table (not used in the core functionality, but will become important for the GUI).

####Getting information about particular words
If you would like to know the available phonological data about a particular word, you can access those functions directly. All that data is included in the description_table function, e.g.,

```
ph = Phonology()
ph.description_table('banana')
```

gives the following output:
<details>
  <summary>Table 1: Word-Level Features</summary>
  
  |            |         |
  |:-----------|--------:|
  | word       | banana  |
  | is_word    | True    |
  | syllables  | 3       |
  | diphthongs | []      |
  | characters | 6       |
  | phonemes   | 6       |
  
</details>
<details>
  <summary>Table 2: Phoneme-Level Features</summary>
  
|             |   B  | AH0  |  N   | AE1  |  N   | AH0  |
|:------------|:----:|:----:|:----:|:----:|:----:|:----:|
|TYPE         |   C  |  V   | C    | V    | C    | V    |
|HEIGHT       | NaN  |0.6   | NaN  | 0.8  | NaN  | 0.6  |
|DEPTH        | NaN  |  0   | NaN  |  1   | NaN  |  0   |
|ROUNDED      | NaN  |  0   | NaN  |  0   | NaN  |  0   |
|RHOTIC       |   0  |  0   | 0    |  0   | 0    | 0    |
|STOP         |   1  |NaN   | 0    | NaN  |  0   | NaN  |
|VOICE        |   1  |NaN   | 0    | NaN  |  0   | NaN  |
|BILABIAL     |   1  |NaN   | 0    | NaN  |  0   | NaN  |
|AFFRICATE    |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|ALVEOPALATAL |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|ALVEOLAR     |   0  |NaN   | 1    | NaN  |  1   | NaN  |
|FRICATIVE    |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|DENTAL       |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|LABIODENTAL  |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|VELAR        |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|LATERAL      |   0  |  0   | 0    | 0    | 0    | 0    |
|POSTALVEOLAR |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|NASAL        |   0  |NaN   | 1    | NaN  |  1   | NaN  |
|LABIOVELAR   |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|PALATAL      |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|GLIDE        |   0  |NaN   | 0    | NaN  |  0   | NaN  |
|GLOTTAL      |   0  |NaN   | 0    | NaN  |  0   | NaN  |
  
</details>

One limitation of this function currently is that it only returns the first match. So, if there are alternate pronunciations, only the primary pronunciation is returned. However, alternate pronunciations can be looked up directly by adding (1) or some other number in parentheses to the search term.

[1]: http://www.speech.cs.cmu.edu/cgi-bin/cmudict
[2]: https://www.english-corpora.org/coca/
