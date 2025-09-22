### EX3 Implementation of GSP Algorithm In Python
### DATE: 22.09.2025
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>


## PROGRAM:



```

from collections import defaultdict
from itertools import combinations
def generate_candidates(dataset, k, min_support):
    candidates = defaultdict(int)
    for seq in dataset:
         flat_seq = [item for itemset in seq for item in itemset]
        for comb in combinations(flat_seq, k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

def gsp(dataset, min_support):
    fp = defaultdict(int)
    k = 1
    while True:
        candidates = generate_candidates(dataset, k, min_support)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp

dataset = [
    [["a","b","c"], ["b","e"], ["c","f","g"], ["a","b","e"]],   # <abc (be) cfg (abe)>
    [["a","d"], ["b","c"], ["c"], ["f","g"], ["c","h"]],        # <ad (bc) c (fg) (ch)>
    [["b","c"], ["a","d"], ["e","b","f"], ["c","d","f","g","h"]], # <bc (ad) ebf (cdfgh)>
    [["c"], ["e","c"], ["e","h"]]                               # <c (ec) (eh)>
]

dataset2 = [
    [["b","d"], ["c","b"], ["a","c"]],  
    [["b","f"], ["c","e"], ["b"], ["f","g"]],       
    [["a","h"], ["b","f"], ["a","b","f"]],
    [["b","e"], ["c","e"], ["d"]],   
    [["a"], ["b","d"], ["b","c","b"], ["a","d","e"]]
]

min_support = 3


results = gsp(dataset, min_support)


print("Frequent Sequential Patterns for Dataset 1:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
    


results = gsp(dataset2, min_support)

print("\nFrequent Sequential Patterns for Dataset 2:")
if results:
    for pattern, support in results.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")


```

### Output:



<img width="754" height="453" alt="image" src="https://github.com/user-attachments/assets/91e412a1-f824-4db4-91da-9ba2161fdbc3" />



<img width="1011" height="361" alt="image" src="https://github.com/user-attachments/assets/9cdc4d74-5266-4f48-96c4-cdfc86e3ebe6" />



<img width="1008" height="510" alt="image" src="https://github.com/user-attachments/assets/1531149b-314a-41d0-91f4-de47ab08ecfe" />




<img width="999" height="515" alt="image" src="https://github.com/user-attachments/assets/8971cce9-baf5-47e3-904c-06dc727b8f44" />





### Result:

GSP Algorithm in Python is implemented successfully.
