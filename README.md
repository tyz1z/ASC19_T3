# Training method (for ASC19)

- Prepare **HR dataset** with **LR dataset**

- Use the `create_lmdb.py` which we provided to build .lmdb

- Fill the `config file` (in options/train/) correctly

For single node multiple GPUs training:

```bash
python train.py -opt options/train/train_ESRGAN_single.json
```

For multiple nodes distributed training, modify values (IP:FREEPORT etc) in the `config files` and run on each node with correct param.

**FOR EXAMPLE**: 

Run the training program on 2 nodes,so here is what to do: 

node0(master node):

```bash
python train.py -opt options/train/train_ESRGAN_node0.json
```

node1:

```bash
python train.py -opt options/train/train_ESRGAN_node1.json
```

Also you may need to reactivate those validation parts in the json config files and `train.py` to enable result validation, which has been disabled for convenience and faster training speed.

# Testing Method (for ASC19)

Put LR images in the LR folder, then run the command

```bash
python test.py final_model.pth
```

After that run `post-processing-scripts/main_bp.m` in MATLAB for post processing, final SR images will be ouput to `post-processing-scripts/results_20bp` folder.

# Others

`final_model.pth` is the final interpolated model mentioned in our proposal, `net_interp.py` is the python script used for interpolating two models.

