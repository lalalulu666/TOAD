# 基于对抗学习的社交媒体零样本检测研究

## 环境
python 3.7.6 <br/>
transformers 3.4.0 <br/>
pytorch 1.5.1 <br/>
numpy 1.18.1 <br/>
pandas 1.0.3 <br/>
scipy 1.4.1


## 训练
cd src/ 

创建一个文件夹并在其中创建一个名为src的文件夹

在数据/资源中，放置预先训练的 GloVe 词嵌入和主题词典（将训练数据中的主题映射到索引）。

运行 
```angular2html
python train_and_eval_model.py --mode "train" --config_file <config_name> --trn_data <train_data> --dev_data <dev_data> --score_key <score_key> --topics_vocab <topic_dictionary> --mode train 
```
例如:
```angular2html
python train_and_eval_model.py --mode "train" --config_file data/config-0.txt --trn_data data/twitter_testDT_seenval/development_setup/train.csv --dev_data data/twitter_testDT_seenval/development_setup/validation.csv --score_key f_macro --topics_vocab twitter-topic-TRN-semi-sup.vocab.pkl --mode train 
```

TOAD配置文件遵循示例TOAD配置文件的格式 - src/config_example_toad.txt

## 模型评估
要在测试集上评估模型，需运行
```angular2html
python train_and_eval_model.py --mode "eval" --config_file <config_name> --trn_data <train_data> --dev_data <test_data> --topics_vocab <topic_dictionary> --saved_model_file_name <saved_model_file_name> --mode eval 
```

例如:
```angular2html
python train_and_eval_model.py --mode "eval" --config_file data/config-0.txt --trn_data data/twitter_testDT_seenval/development_setup/train.csv --dev_data data/twitter_testDT_seenval/test_setup/test.csv --saved_model_file_name data/checkpoints/DT_checkpoint.tar --topics_vocab twitter-topic-TRN-semi-sup.vocab.pkl --mode eval 
```

## 基线模型
### BiCond
运行
```angular2html
python train_and_eval_model.py --mode "train" --config_file <config_name> --trn_data <train_data> --dev_data <dev_data> --score_key <score_key>
```

配置文件需遵循示例中的格式 - src/config_example_bicond.txt

## TOAD的超参数搜索
运行
```angular2html
python hyperparam_selection.py -m 1 -s <config_file_for_hyperparam_tuning> -k <score_key>
```

配置文件应遵循示例TOAD超参数配置文件格式 -  src/hyperparam-twitter-adv.txt



