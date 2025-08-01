:

---

## **What the Code Does**

### 🔹 **1. Load Data**

```python
def load_csv(filename)
```

* Reads a CSV file.
* Returns the dataset as a list of rows and a separate list of headers.

### **2. Entropy Calculation**

```python
def entropy(S)
```

* Computes Shannon entropy for the class labels in the dataset.

### **3. Information Gain**

```python
def compute_gain(data, col)
```

* Calculates how much information gain is obtained by splitting on a specific attribute.

### **4. Sub-Tables**

```python
def sub_tables(data, col, delete)
```

* Splits data based on unique values in a column.
* Removes the column if `delete=True` (for recursive tree building).

### **5. Build Decision Tree**

```python
def build_tree(data, features)
```

* Recursively builds the decision tree using the highest information gain at each level.
* Uses a custom `Node` class.

### **6. Display Tree**

```python
def print_tree(node, level=0)
```

* Nicely prints the tree structure.

### **7. Classify a Test Instance**

```python
def classify(node, x_test, features)
```

* Traverses the tree based on feature values of a test instance.

### **8. Main Program**

* Loads training and test datasets.
* Builds the tree and classifies each test instance.

---

## **Expected File Structure**

* `Training_Dataset.csv`: Should contain training data (with headers and class labels in the last column).
* `TestDataset.csv`: Should contain test instances (with the same features).

Ensure both files are in:

```
D:\MLT_LAB\Decision_Tree_Algorithm\
```

---

##  Suggestions for Improvement

1. **Handle Binary Class Assumption in `entropy()`**

   * Currently assumes only 2 classes (binary classification).
   * Generalize using:

     ```python
     counts = [S.count(val)/len(S) for val in attr]
     ```

2. **Error Handling for File Paths**
   Add:

   ```python
   try:
       ...
   except FileNotFoundError:
       print("File not found!")
   ```

3. **Normalize Output**
   You can display the decision tree using libraries like `graphviz` for better visualization.

---

##  Sample Output

```
The decision tree for the dataset using ID3 algorithm is:
Outlook
  (Sunny)
    Humidity
      (High)
        => No
      (Normal)
        => Yes
  (Overcast)
    => Yes
  (Rain)
    Wind
      (Strong)
        => No
      (Weak)
        => Yes
```

---





