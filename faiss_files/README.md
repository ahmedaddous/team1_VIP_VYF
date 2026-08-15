# Generating FAISS Table (Old File)
You can think of [FAISS](https://github.com/facebookresearch/faiss) as a very smart look-up table. Once you pass in a vector as an
input, it enables you to search for vectors (FastText word embeddings in our case) that are most similar to it. While you can do 
this with the FastText library itself, FAISS was designed to be more efficient.

# How to Run
Log into PACE-ICE, and type 
```sh
sbatch generate_faiss 
```