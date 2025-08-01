
### OVERVIEW:

This ID3 algorithm:

* Calculates **entropy** and **information gain**.
* Recursively builds a **decision tree**.
* Can **classify** unseen test data based on the tree.

---

## EXPLANATION OF EACH PART

### 🔹 1. **Importing Libraries**

```python
import math
import csv
```

* `math` is used for log calculation.
* `csv` is used to load CSV files containing datasets.

---

### 🔹 2. **Loading the CSV File**

```python
def load_csv(filename):
    lines = csv.reader(open(filename, "r"))
    dataset = list(lines)
    headers = dataset.pop(0)
    return dataset, headers
```

* Opens and reads a CSV file.
* Extracts **headers (feature names)**.
* Returns the **dataset** (excluding header) and **headers**.

---

### 🔹 3. **Node Class (Tree Node)**

```python
class Node:
    def __init__(self, attribute):
        self.attribute = attribute
        self.children = []
        self.answer = ""
```

Each `Node` represents:

* `attribute`: Name of the feature to split on.
* `children`: List of children (attribute value, child node).
* `answer`: If it's a leaf node, stores the class label.

---

### 🔹 4. **Sub-Tables (Split the Data)**

```python
def sub_tables(data, col, delete):
```

* Splits the dataset based on the unique values in column `col`.
* `delete=True` removes the splitting column for recursion.
* Returns:

  * `attr`: unique values (e.g., "Sunny", "Rainy")
  * `dic`: dictionary mapping each value to its corresponding sub-table

---

### 🔹 5. **Entropy Calculation**

```python
def entropy(S):
```

* Calculates entropy for a list of class labels (`S`).
* Assumes binary classification (improveable for multi-class).
* Formula used:

  $$
  \text{Entropy} = -\sum p_i \log_2(p_i)
  $$

---

### 🔹 6. **Compute Information Gain**

```python
def compute_gain(data, col):
```

* Computes **information gain** for a column:

  $$
  \text{Gain} = \text{Entropy(parent)} - \sum \left(\frac{|\text{subset}|}{|\text{total}|} \cdot \text{Entropy(subset)}\right)
  $$
* Picks the best attribute to split on.

---

### 🔹 7. **Build the Decision Tree**

```python
def build_tree(data, features):
```

* Recursive function to build the decision tree.
* Base case: If all instances belong to one class → create a leaf node.
* Recursive case: Find the best attribute (max gain), split, and recurse on each sub-table.

---

### 🔹 8. **Print the Decision Tree**

```python
def print_tree(node, level=0):
```

* Recursively prints the decision tree.
* Indentation (`level`) shows depth.

---

### 🔹 9. **Classify New Instance**

```python
def classify(node, x_test, features):
```

* Takes a test instance and traverses the decision tree.
* Returns predicted class label.
* If unknown value is encountered → returns `"Unknown"`.

---

### 🔹 10. **Main Program**

```python
dataset, features = load_csv("...Training_Dataset.csv")
node1 = build_tree(dataset, features)

print("The decision tree for the dataset using ID3 algorithm is:")
print_tree(node1, 0)

testdata, features = load_csv("...TestDataset.csv")
for xtest in testdata:
    print("\nThe test instance:", xtest)
    print("The label for test instance:", classify(node1, xtest, features))
```

#### What it does:

1. Loads the training dataset and builds the tree.
2. Prints the decision tree structure.
3. Loads the test dataset.
4. Classifies each test instance and prints the result.

---


