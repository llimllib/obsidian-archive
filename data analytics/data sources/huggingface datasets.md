---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/huggingface/datasets

> 🤗 Datasets is a lightweight library providing **two** main features:

-   **one-line dataloaders for many public datasets**: one-liners to download and pre-process any of the [![number of datasets](https://camo.githubusercontent.com/0bb5df216a0dacdce5e9fc266f800407c52c59ed0e36358b95f6ff8938f40d89/68747470733a2f2f696d672e736869656c64732e696f2f656e64706f696e743f75726c3d68747470733a2f2f68756767696e67666163652e636f2f6170692f736869656c64732f646174617365747326636f6c6f723d627269676874677265656e)](https://camo.githubusercontent.com/0bb5df216a0dacdce5e9fc266f800407c52c59ed0e36358b95f6ff8938f40d89/68747470733a2f2f696d672e736869656c64732e696f2f656e64706f696e743f75726c3d68747470733a2f2f68756767696e67666163652e636f2f6170692f736869656c64732f646174617365747326636f6c6f723d627269676874677265656e) major public datasets (text datasets in 467 languages and dialects, image datasets, audio datasets, etc.) provided on the [HuggingFace Datasets Hub](https://huggingface.co/datasets). With a simple command like `squad_dataset = load_dataset("squad")`, get any of these datasets ready to use in a dataloader for training/evaluating a ML model (Numpy/Pandas/PyTorch/TensorFlow/JAX),
-   **efficient data pre-processing**: simple, fast and reproducible data pre-processing for the above public datasets as well as your own local datasets in CSV/JSON/text/PNG/JPEG/etc. With simple commands like `processed_dataset = dataset.map(process_example)`, efficiently prepare the dataset for inspection and ML model evaluation and training.