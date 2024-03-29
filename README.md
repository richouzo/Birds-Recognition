# Birds-Recognition
Download mp3 files, data processing and training functions for birds classification, using pretrained CNN models.

### Download audiofiles and process data
Download the metadata of the birds in your BirdsList (Choose your bird species here)
```
python create_birds_dataset.py
```

Download the audio files (mp3)
```
python download_birds_audio.py
```

Process the audio (convert mp3 to wav), resample audios and create training labels csv
```
python mp3towav.py
```
(! The data_processing.py file is for data processing just before training !)

### Download pretrained models
Download your model from https://zenodo.org/record/3576403#.XqsOuyPVJPY and put it in the pretrained_models directory.

### Launch training (Transfer Learning)
Example: ResNet22, 75% of the dataset
```
python main.py --model_path="pretrained_models/ResNet22_mAP=0.430.pth" --trained_models_path="models" --graphs_path="graphs" --saving=1 --model_type="Transfer_ResNet22" --lr=1e-4 --batch_size=32 --epochs=25 --frac_data=0.75
```

Example: Cnn6, 100% of the dataset
```
python main.py --model_path="pretrained_models/Cnn6_mAP=0.343.pth" --trained_models_path="models" --graphs_path="graphs" --saving=1 --model_type="Transfer_Cnn6" --lr=1e-3 --batch_size=16 --epochs=25
```


--model_path: Path to your pretrained model

--saving: 0 = do not save; 1 = save training graph and trained model to .pth

--model_type: The class name of your Pytorch model in transflearn_models.py

--frac_data: Fraction of the dataset for training (0 <= frac_data =< 1, default = 1)

### Inference on the test set and show stats with a Confusion Matrix
Example: Plot CM for trained Transfer_ResNet22
```
python plot_cm.py --trained_model_path="models/Transfer_ResNet22_trained_testAcc=0.6330.pth" --graphs_path="graphs" --saving=1 --model_type="Transfer_ResNet22"
```


### Credits
Author: Richard Huang, under the guidance of [Nicolas Farrugia](https://github.com/nicofarr)

Dataset retrieved from https://www.xeno-canto.org

Download function inspired by [AgaMiko](https://github.com/AgaMiko/xeno-canto-download)

Code for Audioset Tagging CNN from [Qiu Qiang Kong](https://github.com/qiuqiangkong/audioset_tagging_cnn)
