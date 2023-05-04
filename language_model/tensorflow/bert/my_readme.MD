Run commands as below:
```
git clone https://github.com/sgpyc/training
cd language_model/tensorflow/bert/cleanup_scripts
source download_and_umcompress.sh
git clone https://github.com/attardi/wikiextractor.git
cd wikiextractor
git checkout 3162bb6c3c9ebd2d15be507aa11d6fa818a454ac
cd .. 
python wikiextractor/WikiExtractor.py wiki/enwiki-20200101-pages-articles-multistream.xml
./process_wiki.sh './text/*/wiki_??'
```

The original code works for TF.1. The following fix is for TF-2.12.0:


pip install --user tensorflow

The file `create_pretraining_data.py` has been modified

run command to create pretain data:
```
for f in results/par*; do b=`basename $f`; echo $f; echo $b; python3 create_pretraining_data.py \
   --input_file=$f   --output_file=tfrecord/$b --vocab_file=wiki/vocab.txt   \
   --do_lower_case=True    --max_seq_length=512    --max_predictions_per_seq=76 \
   --masked_lm_prob=0.15    --random_seed=12345    --dupe_factor=10; done
   
python3 create_pretraining_data.py  --input_file=./results/eval.txt --output_file=./eval_intermediate --vocab_file=./wiki/vocab.txt --do_lower_case=True --max_seq_length=512 --max_predictions_per_seq=76 --masked_lm_prob=0.15 --random_seed=12345 --dupe_factor=10


git clone https://github.com/mlperf/logging.git mlperf-logging
pip install -e mlperf-logging


TF_XLA_FLAGS='--tf_xla_auto_jit=2' python3 run_pretraining.py --bert_config_file=./cleanup_scripts/wiki/bert_config.json --output_dir=/tmp/output/ --input_file=./cleanup_scripts/tfrecord/eval_10k --do_eval --nodo_train --eval_batch_size=8 --init_checkpoint=./cleanup_scripts/wiki/tf2_ckpt/model.ckpt-28252.index --iterations_per_loop=1000 --learning_rate=0.0001 --max_eval_steps=1250 --max_predictions_per_seq=76 --max_seq_length=512 --num_gpus=1 --num_train_steps=107538 --num_warmup_steps=1562 --optimizer=lamb --save_checkpoints_steps=1562 --start_warmup_step=0 --train_batch_size=24 --nouse_tpu


```


