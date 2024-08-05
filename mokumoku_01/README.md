# chapter01 テキストクラシフィケイション


## datasetを使ってみる
emotionDatasetの中身を確認した


## 番外編
オリジナルのデータセットを作ってみる
- ### csvで作った場合
    ```python
    original_dataset = load_dataset('csv', data_files='./original_dataset2.csv', sep=',', names=['label', 'text'])
    original_dataset
    ```
    出力
    ```
    DatasetDict({
        train: Dataset({
            features: ['label', 'text'],
            num_rows: 6
        })
    })
    ```

- ### trainオンリーになってしまうし、featruesがない
    ```python
    original_dataset['train'].features
    ```
    出力
    ```
    {'label': Value(dtype='int64', id=None),
    'text': Value(dtype='string', id=None)}
    ```

- ### featuresをemotionから持ってくる
    ```python
    original_dataset.features = emotions['train'].features
    original_dataset.features
    ```
    出力
    ```
    {'text': Value(dtype='string', id=None),
    'label': ClassLabel(names=['sadness', 'joy', 'love', 'anger', 'fear', 'surprise'], id=None)}
    ```

- ### train testで分ける
    ```python
    train_test_split = original_dataset['train'].train_test_split(test_size=0.2)
    train_test_split
    ```

    出力
    ```
    DatasetDict({
        train: Dataset({
            features: ['label', 'text'],
            num_rows: 4
        })
        test: Dataset({
            features: ['label', 'text'],
            num_rows: 2
        })
    })
    ```
