# Python-based Machine Learning Frame Server for Nuke

This repository contains the client-server system enabling Machine Learning (ML) inference in Nuke. This work is split into two parts: a client Nuke plug-in [Plugins/Client/](Plugins/Client) and the Python frame server [Plugins/Server](Plugins/Server).

The following models are provided as examples:
- blur: a simple gaussian blur operation
- [Mask-RCNN](https://github.com/facebookresearch/Detectron)
- [trainingTemplateTF](https://github.com/TheFoundryVisionmongers/nuke-ML-server/tree/master/Models/trainingTemplateTF): a training template written in TensorFlow which enables simple image-to-image training. Instructions on how to use this template are found [here](https://github.com/TheFoundryVisionmongers/nuke-ML-server/tree/master/Models/trainingTemplateTF).

<div align="center">
  <img src="https://user-images.githubusercontent.com/27013153/54621337-837f0900-4a5f-11e9-9169-0e8ad1fbe67a.png" width="700px" />
  <p>Example of Nuke doing DensePose inference.</p>
</div>

## Introduction

The Machine Learning (ML) plug-in connects Nuke to a Python server to apply ML models to images.
The plug-in works as follows:
- The Nuke node can connect to a server given an ip address and port,
- The Python server responds with the list of available Machine Learning (ML) models and options,
- The Nuke node displays the models in an enumeration knob, from which the user can choose,
- On every renderStripe call, the current image and model options are sent from the Nuke node to the server,
- The server does an inference on the image using the chosen model/options. This inference can be an actual inference operation of a machine learning model, or just some other image processing code,
- The resulting image is sent back to the Nuke node.

## Installation

Please find installation instructions in [INSTALL.md](INSTALL.md).

## Known Issues

1. The GPU can run out of memory when doing model inference. To run Mask-RCNN, it is necessary to have a GPU memory of at least 6GB.
2. If you get the following error: "The TensorFlow library was compiled to use AVX instructions, but these aren't available on your machine." Please refer to [issue#10](https://github.com/TheFoundryVisionmongers/nuke-ML-server/issues/10) [Thanks to [samhodge](https://github.com/samhodge)]

## License

The source code is licensed under the Apache License, Version 2.0, found in [LICENSE](LICENSE).

## Contacts

- Johanna Barbier (Johanna.Barbier@foundry.com)
- Dan Ring (Dan.Ring@foundry.com)

This plug-in was initially created by Sebastian Lutz (https://v-sense.scss.tcd.ie/?profile=sebastian-lutz).

## References

- [Mask R-CNN](https://arxiv.org/abs/1703.06870).
  Kaiming He, Georgia Gkioxari, Piotr Doll??r, and Ross Girshick.
  IEEE International Conference on Computer Vision (ICCV), 2017.
- [DensePose: Dense Human Pose Estimation In The Wild](https://arxiv.org/abs/1802.00434).
  Riza Alp G??ler, Natalia Neverova, Iasonas Kokkinos.
  IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018.