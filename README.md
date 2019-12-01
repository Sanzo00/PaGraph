# PaGraph

Graph Neural Network Framework on Large Scaled Graph Dataset with Multi-GPUs training, partitioning and caching.


## Prepare Dataset

* For randomly generated dataset:

  * Usa [PaRMAT](https://github.com/farkhor/PaRMAT) to generate a graph:

    ```bash
    $ ./PaRMAT -nVertices 10 -nEdges 50 -output /path/to/datafolder/pp.txt -noDuplicateEdges -undirected -threads 16

    ```
  
  * Generate random features, labels, train/val/test datasets:

    ```bash
    $ python data/preprocess.py --dataset xxx/datasetfolder --ppfile pp.txt --gen-feature --gen-label --gen-set
    ```

    This may take a while to generate all of these.

## Run

### Launch Graph Server

```bash
$ python launch/launch_server.py --dataset xxx/datasetfolder --num-workers 3
```

### Run Client Trainer

* Run w/o Partitioning

  ```bash
  $ DGLBACKEND=pytorch python examples/gcn_client_nccl_ns.py --gpu 0,1 --dataset /path/to/datasetfolder --num-neighbors 10 --batch-size 30000
  ```