Run command

```
docker run --ipc=host -it --rm --runtime=nvidia \
  -v /disk1/scratch/data/KiTS19/kits19/data/:/raw_data \
  -v /disk1/scratch/preprocessed_data/KiTS19/training/:/data \
  -v /disk1/scratch/results/:/results \
  unet3d:latest /bin/bash
```
