# Butterfly Classification

This is a simple repository of my final project for iD Tech's Artificial Intelligence and Machine Learning with NVIDIA. The repository contains the files needed to generate a model for butterfly classification, as well as code for exporting and validating the model.

**Note: Most of these commands need to be run on a Jetson Nano; however, you can train the model on a Google Colab notebook.**

## Getting Started

To get started, first download the dataset from [here](https://drive.google.com/file/d/1QN5i87xkpjvEZIqpWou2Mbi3I_cX4uC8/view?usp=sharing) and unzip it. This dataset contains images of various butterfly species and their corresponding names.

Then, create a `data` directory in the root of the repository with `mkdir data`, and place the dataset in the `data` folder with the following structure:

```
data
├─── test
│   ├─── ADONIS
│   ├───   ├─── 1.jpg
│   ├───   ├─── 2.jpg
│   ├───   ├─── ...
├─── train
│   ├─── ADONIS
│   ├───   ├─── 01.jpg
│   ├───   ├─── 02.jpg
│   ├───   ├─── ...
├─── val
│   ├─── ADONIS
│   ├───   ├─── 01.jpg
│   ├───   ├─── 02.jpg
│   ├───   ├─── ...
├─── labels.txt
```

After downloading the dataset, you can start training the model by running the following command:

```bash
python3 train.py --model-dir=model --batch-size=32 --workers=4 --epochs=30 data
```

## Exporting the Model

The model can be exported to a .onnx file by running the following command:

```bash
python3 onnx_export.py --model-dir=model
```

To validate the model, run the following command:

```bash
python3 onnx_validate.py --model=model
```

## Testing the Model

To test the accuracy of the model, download the 6 test images from [here](https://drive.google.com/file/d/1QN5i87xkpjvEZIqpWou2Mbi3I_cX4uC8/view?usp=sharing) and place them in the `test` folder.

Then, run the following commands:

```bash
imagenet.py --model=model/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=data/labels.txt test/<id>.jpg
```

where `<id>` is the id of the image.
