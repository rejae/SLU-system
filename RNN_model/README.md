## RNN 模型
参考 chengyunlong 的 ca_finetune模型 地址： https://github.com/MiuLab/SpokenVec

论文： 《LEARNING ASR-ROBUST CONTEXTUALIZED EMBEDDINGS FOR SPOKEN LANGUAGE UNDERSTANDING》


### Steps
For training baseline models with or without ELMo embeddings:


# 1. For static word embeddings
python3 main.py ../models/snips_tts/1   

# 2. For pre-trained ELMo embeddings
python3 main.py ../models/snips_tts/2

# 3. Fine-tuning LM
```
For fine-tuning ELMo with only LM objective (ULMFit) and using it to train SLU classifier
# Training SLU classifier with the fine-tuned LM, you might want to modify the specific checkpoint in the config.
```
python3 main_lm.py ../models/lm/snips_tts/1

python3 main.py ../models/snips_tts/3

# 4. Fine-tuning LM with unsupervised extracted confusions

python3 main_lm.py ../models/lm/snips_tts/2   --ca_finetune

python3 main.py ../models/snips_tts/4

testing finished, testing loss 0.4018888771533966, acc 0.8970643939393939

# 5. Fine-tuning LM with supervised extracted confusions
python3 main_lm.py ../models/lm/snips_tts/3  --ca_finetune

python3 main.py ../models/snips_tts/5