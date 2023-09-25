---
layout: post
title: Decision Tree Program
description: Python program to construct a decision tree.
image:
---


## Python Programming

### Summary
This was a program I created in python to construct a decision tree with custom outputs. The purpose of the program is to print the decision being made, the information gain based on entropy, the ending leaf with its label, purity, and size. It leverages the scikit-learn decision tree classifier. The main program is one function that utilizes multiple functions to read the file and construct the tree. The program can take any csv file with the class as the last column. It was demonstrated on the iris dataset.

### Highlights
* Demonstrates the use of python functions with function documentation with docstring
* Error handling with try and except to read files and run the program
* Use of for loops, while loops, and if/else statements

### Tools
* Pandas
* Numpy
* Sklearn

### Program Preview
```Python
def Decision_Tree(D, min_node, min_impurity, headers=None, delimiter=','):
    """Function to make a decision tree based on entropy and information gain,
         until max depth is reached or purity.
       D: CSV file
       min_node: minimum size of leaf to stop
       min_impurity: Threshold for early stopping in tree growth. A node will
          split if it's impurity is above the threshold, otherwise it is a
          leaf. This is oposite of max impurity.
       headers = Defaults to none, option to put in headers for file.
       delimiter = Delimiter for file reading, defaults to comma.
       Returns a decision tree with decision, leaf, purity, gain, size, and
          class.
    """


    try:
        X,y = read_file(D, headers, delimiter)

        # build tree
        dt = build_tree(min_node, min_impurity, X, y)

        # get entropies
        entropies, values = get_entropy(dt.tree_.value)

        # determine type
        node_depth, is_leaves = construct_nodes(dt)

        # get info from classifier module
        n_nodes = dt.tree_.node_count
        feature = dt.tree_.feature
        threshold = dt.tree_.threshold

        # create list of classes for each node
        node_labels = []
        for node in dt.tree_.value:
            node_labels.append(dt.classes_[np.argmax(node)])


        # ---Print Outcome---

        for i in range(n_nodes):
            # if it is a leaf
            if is_leaves[i]:            
                depth = node_depth[i]
                class_label = node_labels[i]
                purity = np.round((1-dt.tree_.impurity[i]),2)
                size = dt.tree_.n_node_samples[i]

                print('{}Leaf: Label = {} Purity = {} Size = {}'.format
                      (depth*'\t', class_label, purity, size))

            # if it is a decision
            else:
                # parent and two children
                nodes = [i, i+1, i+2]

                # calculate information gain
                info_gain = np.round(calculate_info_gain(entropies, values,
                                                         nodes),2)
                depth = node_depth[i]
                decision_threshold = np.round(threshold[i],2)

                print('{}Decision: {} <= {} Gain = {}'.format
                      (depth*'\t', X.columns[feature[i]], decision_threshold,
                       info_gain))

    except:
        print('Unexpected error:', sys.exc_info()[0])
        raise
```


### The Complete Project
<section id="Repository">
	<div class="inner">
    <ul class="actions fit small">
      <li><a href="https://github.com/Torreylee1028/Decision-Tree-Program" target="_blank" class="button small">View Repository</a></li>
    </ul>
	</div>
</section>
