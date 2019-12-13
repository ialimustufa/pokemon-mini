
To train on colab (online) :

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ialimustufa/pokemon-mini-tflite/Train%20Online/pokemon.ipynb]

(Activate your Virtual Enviorment)
cd env 
cd /Script/activate.bat

Don't Type: You should see this (env) $
(Virtual Enviorment Activated)

cd..

tensorboard --logdir tf_files/training_summaries &

Start New command prompt

(Activate your Virtual Enviorment)
cd env
cd /Script/activate.bat

Don't Type: You should see this (env) $
(Virtual Enviorment Activated)

cd..

python -m scripts.retrain   --bottleneck_dir=tf_files/bottlenecks --how_many_training_steps=500   --model_dir=tf_files/models/ --summaries_dir=tf_files/training_summaries/"mobilenet_0.50_224" --output_graph=tf_files/retrained_graph.pb   --output_labels=tf_files/retrained_labels.txt   --architecture="mobilenet_0.50_224"  --image_dir=tf_files/smalldb

python -m scripts.label_image  --graph=tf_files/retrained_graph.pb --image=tf_files\smalldb\Charmeleon\26cd745d4a7943c5af9a20fef4f90fad.jpg

tflite_convert --graph_def_file=tf_files/retrained_graph.pb  --output_file=tf_files/optimized_graph.lite  --input_format=TENSORFLOW_GRAPHDEF  --output_format=TFLITE  --input_shape=1,224,224,3  --input_array=input  --output_array=final_result  --inference_type=FLOAT   --input_data_type=FLOAT


