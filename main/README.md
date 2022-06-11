Raksit Tyler Lau-Preechathammarach
2016.06.24

This is the revised implementation of Lau (2016)

Main Code 2 guesses only ending

~*~

# Input layer
- A stem can have a maximum of 36 phonemes (6 syllables, 6 potential phonemes)
- Potential phonemes are: p, t, k, b, d, g, f, v, s, z, h, m, n, w, r, l, y, i, u, e, o, a, - (no phoneme)
- COMMENTS: Back? High? Also lateral to distinguish l and r?

- Each phoneme is represented by 11 features, from Chomsky & Halle (1968):
1) Syllabic (Vowels VS Non-Vowels)
2) Consonantal (Consonants VS Glides & Vowels)
3) Voice (Voiced VS Unvoiced)
4) Continuant (Continuants VS Stops/Nasals)
5) Strident (f, v, s, z, VS others)
6) Nasal (m, n VS others)
7) Anterior (front—includes l and r unlike English VS back)
8) ??? (a, o VS others)
9) Grave (u, o, a, schwa, labial, velar VS coronal)
10) Round (w, u, o VS others)
11) ??? (u, a, ptkfsh VS others)
?12) Lateral (l VS others)

- 36 * 11 = 396 nodes

--

- ABOVE SEEMS OFF SO REMADE:
1) Sonorant
2) Vocalic
3) Consonantal
4) Coronal
5) Anterior (in front of palatoalveolar—labial, dental, alveolar)
6) High (Palatals and Velars VS Uvulars and Pharyngeals)
7) Low (Pharyngeals VS Palatals, Velars, uvulars)
8) Back (Velars, Uvulars, Pharyngeals VS Palatals)
9) Nasal 
10) Lateral
11) Continuant
12) Voice
13) Strident (f, v, s, z, VS others)

- Round not distinctive
- Strident not distinctive

--

## 8 nodes are used to represent humanness

1 1 1 1 0 0 0 0 —> male human

0 0 0 0 1 1 1 1 —> female human

0 0 0 0 0 0 0 0 —> non-human

--

## Original had Slavic gender, but they are irrelevant (12 nodes)

1 1 1 1 0 0 0 0 0 0 0 0 —> masculine

0 0 0 0 1 1 1 1 0 0 0 0 —> feminine

0 0 0 0 0 0 0 0 1 1 1 1 —> neuter

--

## Case Frequencies Implemented as how many times case goes into model—estimated by Polinsky and van Everbroeck

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Prose</th>
		<th colspan="2" style="text-align:center;">Poetry</th>
	</tr>
	<tr>
		<th></td>
		<th>Sg</th>
		<th>Pl</th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>8</td>
		<td>3</td>
		<td>4</td>
		<td>2</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>4.5</td>
		<td>2.5</td>
		<td>7</td>
		<td>2</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>4</td>
		<td>2</td>
		<td>2</td>
		<td>1</td>
	</tr>
</table>

- In this instantiation, we get rid of human frequencies, because the token frequency is ALREADY accounted for—humans are already much more common than non-humans.

- From Delatte et al 1981: TAKE ALL WORDS THAT SHOW UP 10 OR MORE TIMES IN BOTH POETRY AND PROSE

## Raw Numbers

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Prose</th>
		<th colspan="2" style="text-align:center;">Poetry</th>
	</tr>
	<tr>
		<th></td>
		<th>Sg</th>
		<th>Pl</th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>27138</td>
		<td>8807</td>
		<td>14479</td>
		<td>3931</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>394</td>
		<td>210</td>
		<td>1849</td>
		<td>401</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>33532</td>
		<td>17906</td>
		<td>9177</td>
		<td>12421</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>15837</td>
		<td>8811</td>
		<td>5802</td>
		<td>1656</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>6081</td>
		<td>3446</td>
		<td>2141</td>
		<td>1610</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>28485</td>
		<td>10446</td>
		<td>10860</td>
		<td>3994</td>
	</tr>
	<tr>
		<td>Total</td>
		<td>112026</td>
		<td>49626</td>
		<td>44585</td>
		<td>24015</td>
	</tr>	
	<tr>
		<td></td>
		<td colspan="2" style="text-align:center;">161652</td>
		<td colspan="2" style="text-align:center;">68600</td>
	</tr>	
	<tr>
		<td>Full Total</td>
		<td colspan="4" style="text-align:center;">230252</td>
	</tr>	
</table>

## By percentage:

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Prose</th>
		<th colspan="2" style="text-align:center;">Poetry</th>
	</tr>
	<tr>
		<th></td>
		<th>Sg</th>
		<th>Pl</th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>16.79</td>
		<td>5.45</td>
		<td>21.11</td>
		<td>5.73</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>0.24</td>
		<td>0.13</td>
		<td>2.7</td>
		<td>5.85</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>20.74</td>
		<td>11.08</td>
		<td>13.38</td>
		<td>18.11</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>9.8</td>
		<td>5.45</td>
		<td>8.46</td>
		<td>2.41</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>3.76</td>
		<td>2.13</td>
		<td>3.12</td>
		<td>2.35</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>17.62</td>
		<td>6.46</td>
		<td>15.83</td>
		<td>5.82</td>
	</tr>
</table>

## By ratio:

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Prose</th>
		<th colspan="2" style="text-align:center;">Poetry</th>
	</tr>
	<tr>
		<th></td>
		<th>Sg</th>
		<th>Pl</th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>129.23</td>
		<td>41.94</td>
		<td>36.11</td>
		<td>9.80</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>1.88</td>
		<td>1</td>
		<td>4.61</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>159.68</td>
		<td>85.27</td>
		<td>22.89</td>
		<td>30.98</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>75.41</td>
		<td>41.96</td>
		<td>14.47</td>
		<td>4.13</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>28.96</td>
		<td>16.41</td>
		<td>5.34</td>
		<td>4.01</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>135.64</td>
		<td>49.74</td>
		<td>27.08</td>
		<td>9.96</td>
	</tr>
</table>

## TOTAL

### Raw

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Total</th>
	</tr>
	<tr>
		<th></th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>41617</td>
		<td>12738</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>2243</td>
		<td>611</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>42709</td>
		<td>30327</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>21639</td>
		<td>10467</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>8222</td>
		<td>5056</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>39345</td>
		<td>14440</td>
	</tr>
	<tr>
		<td></td>
		<td colspan="2" style="text-align:center;">230252</td>
	</tr>
</table>

~*~

### By percentage:		

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Total</th>
	</tr>
	<tr>
		<th></th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>18.07</td>
		<td>5.53</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>0.97</td>
		<td>0.27</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>18.55</td>
		<td>13.17</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>9.40</td>
		<td>4.55</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>3.57</td>
		<td>2.20</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>17.09</td>
		<td>6.27</td>
	</tr>
</table>

### By ratio:

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Total</th>
	</tr>
	<tr>
		<th></th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>68.11</td>
		<td>20.85</td>
	</tr>
	<tr>
		<td>Voc</td>
		<td>3.67</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>69.90</td>
		<td>49.63</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>35.42</td>
		<td>17.13</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>13.46</td>
		<td>8.27</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>64.39</td>
		<td>23.63</td>
	</tr>
</table>	

### By ratio without vocative:

<table>
	<tr>
		<th></th>
		<th colspan="2" style="text-align:center;">Total</th>
	</tr>
	<tr>
		<th></th>
		<th>Sg</th>
		<th>Pl</th>
	</tr>
	<tr>
		<td>Nom</td>
		<td>8.23</td>
		<td>2.52</td>
	</tr>
	<tr>
		<td>Acc</td>
		<td>8.45</td>
		<td>6.00</td>
	</tr>
	<tr>
		<td>Gen</td>
		<td>4.28</td>
		<td>2.07</td>
	</tr>
	<tr>
		<td>Dat</td>
		<td>1.63</td>
		<td>1</td>
	</tr>
	<tr>
		<td>Abl</td>
		<td>7.78</td>
		<td>2.86</td>
	</tr>
</table>	

***

## Declension Breakdown (Delatte et al 1981)

|	|	Total	|	Prose	|	Poetry	|
| ---	|	---	|	---	|	---	|
| 1	|	39,480	|	27,176	|	12,304	|
| 2	|	75,965	|	55,215	|	20,750	|
| 3	|	86,882	|	61,428	|	25,454	|
| 4	|	12,899	|	9,087	|	3,812	|
| 5	|	7,119	|	5,973	|	1,146	|
| Total	|	230,252	|	161,652	|	68,600	|

Percentage

|	|	Total	|	Prose	|	Poetry
| ---	|	---	|	---	|	---	
| 1	|	17.15	|	16.81	|	17.94
| 2	|	32.99	|	34.16	|	30.25
| 3	|	37.73	|	38.00	|	37.10
| 4	|	5.60	|	5.62	|	5.56
| 5	|	3.09	|	3.58	|	1.67


***

## Hidden layer
- 30 hidden nodes

***

## Output layer
- Mapped to four outputs (P&VE only did gender)
- Gender (3):

	M: 1 0 0
	
	F: 0 1 0
	
	N: 0 0 1

- Declension (5):

	I: 1 0 0 0 0
	
	II: 0 1 0 0 0
	
	III: 0 0 1 0 0 
	
	IV: 0 0 0 1 0
	
	V: 0 0 0 0 1

- Number (2):

	SG: 1 0
	
	PL: 0 1

- Case (3):
	
	- If Case Hierarchy implemented (consider Acc closer to Nom and Gen than Nom and Gen to each other)
	
		Nom: 1 0 0
		
		Acc: 1 1 0
		
		Gen: 1 1 1

	- If Case Hierarchy not Implemented (all three equidistant)
	
		Nom: 1 0 0
		
		Acc: 0 1 0
		
		Gen: 0 0 1


### Relevant parameters

- Genitive Drop (Gnv)
	- If T, genitive is dropped
	- If F, genitive is not dropped
- Case Hierarchy
- Features 1: Changed features to 1 instead of 0.9
