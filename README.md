# controlnet_stable_tensorrt

This project implements TensorRT acceleration for Stable Diffusion with ControlNet, demonstrated through text-to-image generation.

Since NVIDIA officially only provides a Stable Diffusion demo without ControlNet integration, but many users need ControlNet functionality, this project aims to help those in need. Please note that this project has some imperfections, and any errors are appreciated to be pointed out.

## Dependencies

This project is developed based on SD1.5, using opset 17 (SD2.1 has also been tested and works).

The main testing environment is as follows. For more details, please refer to: [tensorrt](https://github.com/NVIDIA/TensorRT/tree/release/8.6/demo/Diffusion)

```
cuda-python              12.1.0rc1+1.g9e30ea2.dirty
huggingface-hub          0.13.4
nvidia-cublas-cu12       12.1.0.26
nvidia-cuda-runtime-cu12 12.1.55
nvidia-cudnn-cu12        8.8.1.3
nvidia-dali-cuda110      1.22.0
nvidia-pyindex           1.0.9
onnx                     1.13.1
onnx-graphsurgeon        0.3.26
onnxruntime              1.14.1
protobuf                 3.20.3
tensorrt                 8.6.0
torch                    1.13.1+cu117
triton                   2.0.0
```

## Running

```bash
python3 demo_txt2img_db.py  --hf-token="your huggingface token" -v
```

*Note: The engine building process is extremely time-consuming, taking approximately 30-40 minutes. Please be patient.*

## Results

Compared the performance with and without TensorRT - the results are essentially identical (left image is TensorRT-optimized), with efficiency improvement of approximately 30-40% (baseline using fp16). On an RTX 8000, processing a 512x512 image takes about 1200ms.

<img src="./images/trt.png" alt="img" width="375" style="zoom:50%;" /><img src="./images/origin.png" alt="img" width="375" style="zoom:50%;" />

## Limitations

- Currently, generating a 512x512 image requires approximately 30GB of VRAM. Since this project is developed based on NVIDIA's official code, bug fixes depend on official updates. Please consider this accordingly.
- Currently, the image size is fixed at 512x512. Future updates may optimize for other dimensions.

## Acknowledgments

This project references [tensorrt](https://github.com/NVIDIA/TensorRT/tree/release/8.6/demo/Diffusion) and [paddle](https://github.com/PaddlePaddle/PaddleNLP/tree/develop/ppdiffusers/deploy). Thanks to the power of open source.
