# **Darknet2Tensor Converter**

Prepare Python virtual environment :

```bash
$ cd darknet
$ python3 -m venv env
$ source env/bin/activate
```

Install dependencies :

```bash
(env) $ pip install -r requirements.txt
```

## **Usage**

Before start, please don't fotget change class list first by:
 - At the root of repo, go to `darknet/data/classes/product.names` then change the old one to your class names because the number of the class **MUST** match with your weight. 

### **Weight to Tensor**

Paste your `*.weight` to `ml_models/` at the root of the repository then run command below in `darknet` directory :

```bash
(env) $ python save_model.py \
--weights ../ml_models/YOUR_MODEL_NAME.weights \
--output ../checkpoints/YOUR_MODEL_NAME \
--input_size 416 \
--model yolov4

# Output

...
__________________________________________________________________________________________________
tf_op_layer_Reshape_14 (TensorF [(None, None, None)] 0           tf_op_layer_GatherV2_1[0][0]
                                                                 tf_op_layer_Reshape_14/shape[0][0
__________________________________________________________________________________________________
tf_op_layer_concat_18 (TensorFl [(None, None, None)] 0           tf_op_layer_concat_17[0][0]
                                                                 tf_op_layer_Reshape_14[0][0]
==================================================================================================
Total params: 64,014,760
Trainable params: 63,948,456
Non-trainable params: 66,304
__________________________________________________________________________________________________
2021-03-23 13:04:52.839035: W tensorflow/python/util/util.cc:348] Sets are not currently considered sequences, but this may change in the future, so consider avoiding using them.
INFO:tensorflow:Assets written to: ../checkpoints/product_20210322_yolov4_best/assets
I0323 13:05:20.397754 4595387840 builder_impl.py:775] Assets written to: ../checkpoints/product_20210322_yolov4_best/assets
(env) $
```

The output is in `checkpoints/` directory.

**Tensor to TFLite**

Just

```bash
(env) $ python convert_tflite.py \
--weights ../checkpoints/YOUR_MODEL_NAME \
--output ../checkpoints/YOUR_MODEL_NAME.tflite
```

The output is in `checkpoints/` directory.