# implementation-of-GSP-algorithm

## EX3 Implementation of GSP Algorithm In Python
DATE: 12/04/25

## AIM: To implement GSP Algorithm In Python.
Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.

## Steps:
Database Scanning: GSP scans the sequence database to determine the support of each item in the dataset.
Candidate Generation: It generates a set of candidate sequences using frequent items found in the previous step.
Pattern Growth: It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
Repeat: The process continues until no new sequences meet the minimum support threshold.
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.

## Procedure:
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is used to create a dictionary with default values and combinations generates all possible combinations of a sequence.

2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.

3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.

4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.

5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.

6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the minimum support threshold.

7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns along with their support counts for each wear category.

8. Visulaize the sequence patterns using matplotlib.

### Program:
```
NAME : MOHAMED AZEEM N
REG NO : 212222110026


from collections import defaultdict
from itertools import combinations
import pandas as pd  # Import pandas for table formatting

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for sequence in dataset:
        for subsequence in combinations(sequence, k):
            candidates[subsequence] += 1
    return candidates

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1  # Start with item sequences of length 1
    frequent_patterns = defaultdict(int)  # Store frequent patterns and their support counts
    while True:
        candidates = generate_candidates(dataset, k)
        # Prune candidates that do not meet the minimum support threshold
        candidates = {pattern: support for pattern, support in candidates.items() if support >= min_support}
        
        if not candidates:  # No frequent patterns found, stop the algorithm
            break
        
        # Add frequent patterns of this length to the result
        frequent_patterns.update(candidates)
        k += 1  # Increase the length of the candidate subsequences
    
    return frequent_patterns

# Example dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"],
    ["hoodie"],
    ["hoodie", "sweater"]
    # Add more sequences for top wear
]

bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"],
    # Add more sequences for bottom wear
]

party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"],
    ["party_dress"],
    # Add more sequences for party wear
]

# Minimum support threshold
min_support = 2

# Perform GSP algorithm for each category
top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)

# Create a function to display results in a table
def display_results(category, result):
    if result:
        df = pd.DataFrame(list(result.items()), columns=["Pattern", "Support"])
        df["Pattern"] = df["Pattern"].apply(lambda x: ', '.join(x))  # Format tuples to string
        print(f"Frequent Sequential Patterns - {category}:")
        display(df)  # Display the table
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Display results for each category
display_results("Top Wear", top_wear_result)
display_results("Bottom Wear", bottom_wear_result)
display_results("Party Wear", party_wear_result)



import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize patterns for each category
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result, 'Party Wear')

```

## Output:
![Screenshot 2025-04-12 140956](https://github.com/user-attachments/assets/09623430-8c39-46af-ba99-23a0ea956ad3)
![Screenshot 2025-04-12 141019](https://github.com/user-attachments/assets/c8c78feb-f995-4116-80d9-a5f4a2232f6f)
![Screenshot 2025-04-12 141041](https://github.com/user-attachments/assets/2680db00-dcbe-418c-8116-f92af6758afa)

![Screenshot 2025-04-12 141054](https://github.com/user-attachments/assets/0f709e6e-b5e4-4ab3-a51a-1db42e0076b2)


## Result:

Thus the experimented of GSP algorithm is successfully completed
