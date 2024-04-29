

## 训练并运行Vary-tiny-600k来生成txt文件（已提供生成的txt文件可跳过）
1. Install Package
cd LAVIS-main
pip install -e .

2. pdf2image
cd data
python data_process.py
cd ../

3. Prepare Pretrain Weights and Data
   - download the OPT-125M [here](https://huggingface.co/facebook/opt-125m/tree/main) and the SAM-b weights [here](https://github.com/facebookresearch/segment-anything)
   - download the Vary-600k [here](https://pan.baidu.com/s/18Rh53JxvbYYl9BPHoFvWcQ) with code "vary"
   - prepare the dirs as follows:
   - 
   ![image](https://github.com/Ucas-HaoranWei/Vary-tiny-600k/assets/50487563/21d529ea-be53-41d3-9ca0-72eb29958bef)

4. Train

python -m torch.distributed.run --nproc_per_node=8 --master_port=29501 train.py --cfg-path lavis/projects/varytiny/train/pretrain.yaml

5. Test
python tests/models/inference_ocr.py --image-file  data/image/


## 使用RAG模块生成回答并保存文件
python tests/models/inference_ocr.py --question  data/question.json --context data/context


