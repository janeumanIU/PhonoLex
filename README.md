# PhonoLex
__Jared Neumann__ <br>
__janeuman@iu.edu__

### Description

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
### Functions

### References
[1]: http://www.speech.cs.cmu.edu/cgi-bin/cmudict
