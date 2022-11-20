## Data modifications:

1. start with two datasets: train and test
1. Drop rows with missing`SalesPrice` from train
1. Make `SalesPrice` column = target = y (for train)(train set target)
1. Remove `SalesPrice` columns from the original dataset (for train)
1. Drop all columns with non-numeric data or strings (for train)(train set features, X)
1. Drop all columns with non-numeric data or strings (for test)
1. Break off validation set from training data (for train)
1. Impute missing values with the mean value along each column (for train)

1-------------

# flowchart

```mermaid
graph LR
    id1[(train.csv)]
    id2[(test.csv)]
    id3[(X_full)]
    id3_1[(X_full)]
    id4[(X_test_full)]
    id5[(y)]
    id6[(X_test)]
    id7[(X)]
    id9[(X_train)]
    random_state1[/random state\]
    random_state2[/random state\]
    id14[(final_X_train)]
    id15[(final_X_valid)]
    id16[(final_X_test)]
    split1[\split 80% of X_full into Train Set/]
    split2[\split 20% of X_full into Validation Set/]
    id9[(X_train)]
    id9_1[[my_model_X_train: </br>- reduction</br> -imputation]]
    id10[(X_val)]
    id10_1[[my_model_X_valid: </br>- reduction</br> -imputation]]
    id11[(y_train)]
    id12[(y_valid)]
    id13[[miss_val_tech_X_test: </br>- reduction</br> -imputation]]
    drop1[[1 drop missing target </br>feature rows]]
    drop2[[2 drop non-numeric cols]]
    drop3[[3 my model: </br>- reduction</br> -imputation]]

subgraph Input
    id1
    id2
end
id1 --> id3
id2 --> id4

    subgraph Train
        subgraph X_full
        id3 --> drop1
        drop1 --> id3_1
        id3_1 --> |select target </br> feature col| id5
        id3_1 --> |drop target </br>feature col| id7
        end

        subgraph Train Set
        split1
        random_state1
        id7 ---> id9
        end
    end
        subgraph Validation Set
        split2
        random_state2
        id7 --> id10
        end

    subgraph Test
    id4 --> id6
    id6 --> id13
    end
    id9 --> id9_1
    id10 --> id10_1

subgraph Output
id9_1 --> id14
id10_1 --> id15
id13 --> id16
        id5 ---> id11
        id5 --> id12
end

```

2-------------

# flowchart

```mermaid
graph LR
    id1[(train.csv)]
    id2[(test.csv)]
    id3[(X_full)]
    id3_1[(X_full)]
    id4[(X_test_full)]
    id5[(y)]
    id6[(X_test)]
    id7[(X)]
    id9[(X_train)]
    id9_1[(miss_val_tech_X_train: </br>- reduction drop missing val col</br> -imputation)]
    id10[(X_val)]
    id10_1[(miss_val_tech_X_valid: </br>- reduction drop missing val col</br> -imputation)]
    id11[(y_train)]
    id12[(y_valid)]
    id13[(miss_val_tech_X_test: </br>- reduction drop missing val col</br> -imputation)]
    drop1{{2 drop non-numeric cols}}
    drop2{{1 drop missing target feature rows}}
    drop3{{3 missing value technique: </br>- reduction drop missing val col</br> -imputation}}
    random_state1[/random state\]
    random_state2[/random state\]
    id14[(final_X_train)]
    id15[(final_X_valid)]
    id16[(final_X_test)]
    split1[\split 80% of X_full into Train Set/]
    split2[\split 20% of X_full into Validation Set/]

subgraph Input
    id1
    id2
end
id1 --> id3
id2 --> id4
subgraph Applied Methods for Missing Values
drop1 -..-> id4
drop1 -..-> id3
drop2 -..-> id3
drop3 -..-> id9
drop3 -...-> id10
drop3 -...-> id6

    subgraph Train
        subgraph X_full
        id3 --> id3_1
        id3_1 --> |select target feature col|id5
        id3_1 -- drop target feature col --> id7
        end

        subgraph Train Set
        split1
        random_state1
        id7 ---> id9
        end
    end
        subgraph Validation Set
        split2
        random_state2
        id7 --> id10
        end

    subgraph test
    id4 --> id6
    id6 --> id13
    end
    id9 --> id9_1
    id10 --> id10_1
end
subgraph Output
id9_1 --> id14
id10_1 --> id15
id13 --> id16
        id5 ---> id11
        id5 --> id12
end

```

3-------------

# flowchart

```mermaid
graph LR
    id1[(train.csv)]
    id2[(test.csv)]
    id3[(X_full)]
    id3_1((X_full))
    id4[(X_test_full)]
    id5[(y)]
    id6((X_test))
    id7[(X)]
    id9((X_train))
    id10((X_val))
    id11((y_train))
    id12((y_valid))
    id13[(miss_val_tech_X_test: </br>- reduction drop missing val col</br> -imputation)]
    id14[(final_X_train)]
    id15[(final_X_valid)]
    id16[(final_X_test)]

    random_state1[/random state\]
    random_state2[/random state\]

  classDef state fill:#500,stroke:#299,stroke-width:1px;
    poly[Polyworks] -->|C#| tk
    class poly state;

subgraph input
    id1
    id2
end
    subgraph train
    id1 --> id3
        subgraph X_full
        id3 --> id3_1
        id3_1 -- select target feature col--> id5
        id3_1 -- drop target feature col --> id7
        end

        subgraph split into train set
        random_state1
        id7 --> id9
        id5 --> id11
    end
        end
        subgraph split into validation set
        random_state2
        id7 --> id10
        id5 --> id12
        end

    subgraph test
    id2 --> id4
    id4 --> id6
    end
subgraph output
id10 --> id15
id9 --> id14
id6 --> id16
end
```

# Notes:

Make sure that you use a method that agrees with how you preprocessed the training and validation data, and set the preprocessed test features to final_test_features `final_X_test`.
