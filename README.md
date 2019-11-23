This repository contains notebooks showing how to perform mixed precision training in `tf.keras` (2.0). 

A great introduction to mixed precision policy is available here: https://forums.fast.ai/t/mixed-precision-training/20720. You can also follow NVIDIA's article: http://docs.nvidia.com/deeplearning/sdk/mixed-precision-training/index.html. 

Mixed precision training has allowed to train very deep neural networks like ResNet50, Transformers etc. sufficiently faster without compromising on the performance part. To perform mixed precision training in `tf.keras` (2.0) there are a number of options available:
- [`tf.train.experimental.enable_mixed_precision_graph_rewrite`](https://www.tensorflow.org/api_docs/python/tf/train/experimental/enable_mixed_precision_graph_rewrite)
- [`tf.keras.mixed_precision.experimental.LossScaleOptimizer`](https://www.tensorflow.org/api_docs/python/tf/keras/mixed_precision/experimental/LossScaleOptimizer)
- [`tf.keras.mixed_precision.experimental.set_policy`](https://www.tensorflow.org/api_docs/python/tf/keras/mixed_precision/experimental/set_policy)

When I was trying the above options in my experiments, I was not satisfied with the results as there was no significant boostup in the model training time. This led me to think if I was using the above options in the correct way. So, I had to open [this issue](https://github.com/tensorflow/tensorflow/issues/34406) in TensorFlow's repo. It turned out to be extremely informative. People like **Timothy Liu** came to pass along all the necessary resources and information I needed to consider while going for mixed precision training. 

After I incorporated the suggestions, I could easily see the results. The notebooks in this repository, however, does not show `tf.train.experimental.enable_mixed_precision_graph_rewrite` but it shows the other two options. I hope you find them useful. 

Here's a mini comparison (model used: **ResNet50**):

| Dataset used        | With mixed precision | Without mixed precision |
|---------------------|:--------------------:|------------------------:|
| [Ship identification](https://datahack.analyticsvidhya.com/contest/game-of-deep-learning) |      **144.69 secs**     |       329.95 secs       |

Find the summary of the experiments [here](https://app.wandb.ai/sayakpaul/mixed-precision-tf-keras). You will be able to find information on CPU usage, memory footprint etc. on experiment basis. 

### Acknowledgements:
- I used the dataset as given in [this Hackathon](https://datahack.analyticsvidhya.com/contest/game-of-deep-learning). The dataset comes in a different form but I adjusted it accordingly to aid my experiments. 
- **Timothy Liu** of NVIDIA. He linked me to a wonderful resource: https://github.com/NVAITC/pycon-sg19-tensorflow-tutorial. 
