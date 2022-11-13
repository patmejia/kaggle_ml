## Data modifications:

1. start with two datasets: train and test
1. Drop rows with missing`SalesPrice` from train
1. Make `SalesPrice` column = target = y (for train)(train set target)
1. Remove `SalesPrice` columns from the original dataset (for train)
1. Drop all columns with non-numeric data or strings (for train)(train set features, X)
1. Drop all columns with non-numeric data or strings (for test)
1. Break off validation set from training data (for train)
1. Impute missing values with the mean value along each column (for train)

# flowchart

```mermaid
graph TD
    id1[(train.csv)]
    id2[(test.csv)]
    id3[(X_full)]
    id3_1((X_full))
    id4[(X_test_full)]
    id5[(y)]
    id6((X_test))
    id7[(X)]
    id9((X_train))
    id9_1((miss_val_tech_X_train: </br>- reduction drop missing val col</br> -imputation))
    id10((X_val))
    id10_1((miss_val_tech_X_valid: </br>- reduction drop missing val col</br> -imputation))
    id11((y_train))
    id12((y_valid))
    id13((miss_val_tech_X_test: </br>- reduction drop missing val col</br> -imputation))
    drop1{{2 drop non-numeric cols}}
    drop2{{1 drop missing target feature rows}}
    drop3{{3 missing value technique: </br>- reduction drop missing val col</br> -imputation}}
    random_state1[/random state\]
    random_state2[/random state\]

subgraph missing value techniques
drop1 -..-> id4
drop1 -..-> id3
drop2 -...-> id3
drop3 -.-> id9
drop3 -.-> id10
drop3 -.-> id6

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
        subgraph split into Validation Set
        random_state2
        id7 ==> id10
        id5 ==> id12
        end

    subgraph test
    id2 --> id4
    id4 --> id6
    end
    id6 --> id13
    id9 --> id9_1
    id10 --> id10_1
end
```

# flowchart

```mermaid
graph TD
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

    random_state1[/random state\]
    random_state2[/random state\]


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
```

# Notes:

Make sure that you use a method that agrees with how you preprocessed the training and validation data, and set the preprocessed test features to final_test_features `final_X_test`.
