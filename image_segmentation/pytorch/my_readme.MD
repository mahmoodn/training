Run command

```
docker run --ipc=host -it --rm --runtime=nvidia \
  -v /disk1/scratch/data/KiTS19/kits19/data/:/raw_data \
  -v /disk1/scratch/preprocessed_data/KiTS19/training/:/data \
  -v /disk1/scratch/results/:/results \
  unet3d:latest /bin/bash
```


Commnad at host:
```
python3 main.py 
   --data_dir /disk1/scratch/preprocessed_data/KiTS19/training 
   --epochs 4000 --evaluate_every 20 --start_eval_at 1000 --quality_threshold 0.908 --batch_size 1 
   --optimizer sgd --ga_steps 1 --learning_rate 0.8 --seed ${1:--1} --lr_warmup_epochs 200
```
