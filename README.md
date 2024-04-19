<br/>
<p align="center">
  <a href="https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Archtecture Style Classifier</h3>

  <p align="center">
    Convolutional-Neural-Network Implementation Project
    <br/>
    <br/>
    <a href="https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/issues">Report Bug</a>
    .
    <a href="https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/issues">Request Feature</a>
  </p>
</p>

<!-- ![Downloads](https://img.shields.io/github/downloads/ChengaFEI/ReadME-Generator/total) -->

![Contributors](https://img.shields.io/github/contributors/ChengaFEI/cnn-driven-architecture-style-classifier?color=dark-green) ![Forks](https://img.shields.io/github/forks/ChengaFEI/cnn-driven-architecture-style-classifier?style=social) ![Stargazers](https://img.shields.io/github/stars/ChengaFEI/cnn-driven-architecture-style-classifier?style=social) ![Issues](https://img.shields.io/github/issues/ChengaFEI/cnn-driven-architecture-style-classifier) ![License](https://img.shields.io/github/license/ChengaFEI/cnn-driven-architecture-style-classifier)

## Table Of Contents

- [Table Of Contents](#table-of-contents)
- [About The Project](#about-the-project)
  - [Project Overview](#project-overview)
  - [Model Selection](#model-selection)
  - [Model Optimization](#model-optimization)
  - [Model Performance](#model-performance)
  - [Project Report](#project-report)
- [Project Structure](#project-structure)
- [Built With](#built-with)
- [Getting Started](#getting-started)
  - [Dataset](#dataset)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
  - [Creating A Pull Request](#creating-a-pull-request)
- [License](#license)
- [Authors](#authors)
- [Acknowledgements](#acknowledgements)

## About The Project

![Project Overview](images/project-overview.jpg)

### Project Overview

This project introduces a novel architecture style classification model aimed at discerning various architectural styles based on their visual characteristics. As individuals explore new environments, encountering buildings of historical or unique significance often sparks curiosity about their architectural styles and the narratives they encapsulate. However, recognizing and cataloging diverse architectural styles can be challenging for humans due to their sheer abundance and complexity. In response to this challenge, our study proposes the development of an architecture style classification model capable of real-time recognition. This model holds promising applications, particularly for tourists who can capture images of buildings and promptly identify their architectural styles. The primary objective is to create a system adept at recognizing architectural styles across different historical eras and various architects' designs. By employing advanced visual recognition techniques, our model aims to contribute to the seamless integration of technology into architectural appreciation, providing an accessible tool for enthusiasts, historians, and tourists alike. The potential impact of such a model extends beyond individual curiosity, offering a practical solution for instant architectural style identification in diverse scenarios.

### Model Selection

![Model Selection](images/model-selection.jpg)

To identify the most suitable CNN architecture for classifying architectural images, we conducted a thorough evaluation of various Convolutional Neural Network (CNN) architectures to determine the most suitable model for classifying architectural images in our initial phase of research. This evaluation encompassed a diverse range of CNN models, including well-known architectures such as VGG, Inception, and ResNet. Each of these models was assessed for their potential effectiveness in our specific application. Ultimately, the ResNet architecture was selected for its advanced residual learning framework. This framework is particularly beneficial as it effectively combats the vanishing gradient problem that often plagues deep neural networks, ensuring consistent learning even as the network depth increases. The selection criteria were not solely based on architectural features; we also considered critical performance metrics. These included the accuracy of the model and the speed of convergence during preliminary testing. Another key factor in our decision was the model's ability to handle deep architectures without significant performance degradation. ResNet's capability to maintain robust performance in deep network structures, without losing efficiency or accuracy, made it the standout choice for our complex image classification task.

### Model Optimization

![Model Optimization](images/model-optimization.png)

**Build ResNet 9 from scratch**: The objective of this phase of our research was to construct and refine a Convolutional Neural Network (CNN) model using PyTorch, tailored specifically for the effective classification of various architectural styles. We build a ResNet 5 from the ground up to test the baseline performance of the model. According to the performance plots, the ResNet 5 model underfits the dataset and converges quickly. Hence, we build a more expressive model, ResNet 9, to improve the model's training accuracy. However, ResNet 9 turns out to overfit the current dataset.

**Causes of overfitting**: Normally, a model overfitting a dataset is caused by two conditions -- either the model is too expressive or the dataset is too small. Hence, we come out with two possible approaches to resolving this issue -- regularizing the model or fetching more data. We first apply the data augmentation techniques, including rotation, scaling, and horizontal flipping, to enrich our training dataset. Data augmentation basically enable the model to identify key features from abnormal images, such as images taken in a dark setting or taken from a skewed perspective. The model trained on the augmented dataset performs better than the last version. Then, to streamline the model's focus and enhance its accuracy, we simplified the classification categories by consolidating them. This step involved merging similar architectural styles into broader categories, decreasing the categories to classify from 25 to 10, thereby reducing the complexity and potential ambiguity of the classification task. However, since augmented data share a large portion of key features with the original dataset, the model still reaches a performance bottleneck. Hence, we adopt the regularization technique.

**Regularization**: We manually add Dropout layers to allow the model to randomly set some fractions of the dataset to 0 at each update and prevent the parameters from co-adapting too much. Compared with its former performance plots, the regularized ResNet9 model produces a higher accuracy in both the training set and the cross-validation set. That is a good sign for the low bias and the low variance.

**Pivot to transfer learning**: Although we handled the over-fitting issue in the ResNet 9 model, there are two subsequent concerns. Compared with using a pre-trained model, it consumes a significant amount of time and data to train it from scratch. However, it is neither time-efficient nor resource-efficient to train the whole model from the ground up because we can borrow the general image classification capabilities from pre-trained CNN models. Hence, in the next stage, we import a larger pre-trained model and feed our specific dataset.

### Model Performance

![Accuracy](images/model-performance-accuracy.png)

Our journey of refinement and optimization culminated with the selection of the ResNet 18 model as our final model. This decision was informed by the model's performance during the previous phases, particularly its ability to effectively address the overfitting issues we encountered.

An integral part of this finalization process involved the meticulous optimization of hyper-parameters. Parameters such as learning rate, batch size, and the number of epochs were fine-tuned to align with the performance metrics we aimed to optimize. This step was crucial to ensure that the model not only performed optimally in terms of accuracy but also operated efficiently.

![Confusion Matrix](images/model-performance-confusion-matrix.jpg)

A suite of metrics was employed to provide a holistic view of the model's performance. These included accuracy, which measures the proportion of correctly predicted instances; precision, indicating the proportion of positive identifications that were actually correct; recall, reflecting the proportion of actual positives that were correctly identified; and the F1 score, which provides a balance between precision and recall. These metrics together offered a comprehensive understanding of the model's strengths and areas for improvement, giving us a detailed picture of its overall effectiveness in classifying architectural styles. In our experiment, the F1 score is 0.93, the recall is 0.93, and the precision is 0.93. These key metrics prove that our model is good enough to identify the correct architecture labels in the picture.

### Project Report

If interested in the project details, you can find the [final report](https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/blob/main/reports/architectural-style-classification.pdf).

## Project Structure

```sh
.
├── LICENSE.md
├── README.md
├── data  # Dataset
│   ├── dataset-lite-augumented  # Put downloaded dataset here
│   └── download.txt  # Follow the instructions to download the dataset
├── images  # Images for README.md
│   ├── logo.png
│   └── screenshot.jpg
├── models  # Trained models
│   ├── custom.ipynb  # Custom model
│   └── transfer.ipynb  # Transfer learning model
├── reports  # Project reports
│   ├── architectural-style-classification.pdf  # Final report
│   ├── docs
│   │   ├── milestone.docx  # Milestone report
│   │   ├── milestone.pdf
│   │   ├── proposal.docx  # Project proposal
│   │   └── proposal.pdf
│   └── latex  # Latex source files
└── utils  # Utils for data processing
    ├── augment-data.ipynb  # Utils for data augmentation
    └── visualize-data.ipynb  # Utils for data visualization
```

## Built With

- `Python`
- `PyTorch`

## Getting Started

### Dataset

1. Augumented Dataset

   - You can download the dataset from the [link](https://drive.google.com/file/d/1Yt9CG-i1Ktt5NevSWfNTlQtQDt8PPyJR/view?usp=drive_link)
   - Unzip the file and rename the folder to `data/dataset-lite-augumented`

2. Raw Dataset

   - You can also find the raw data from the [link](https://drive.google.com/file/d/13_szSJ_DuF98blFr58l8hNftC2lXeWy1/view?usp=drive_link)

### Prerequisites

1. Jupyter Notebook

   - Install the classic Jupyter Notebook with:

     ```sh
     pip install notebook
     ```

   - To run the notebook:

     ```sh
     jupyter notebook
     ```

1. PyTorch

   - Install PyTorch with:

     ```sh
     pip install torch torchvision
     ```

### Installation

1. Clone the repo

   ```sh
   git clone https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier.git
   ```

2. Create a [virtual environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#activating-an-environment)

3. Install the [IPython kernel](https://ipython.readthedocs.io/en/stable/install/kernel_install.html)

4. Run the notebook

   ```sh
   jupyter notebook
   ```

## Usage

The notebook is self-explanatory. You can run the cells one by one to see the results.

## Roadmap

See the [open issues](https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/issues) for a list of proposed features (and known issues).

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

- If you have suggestions for adding or removing projects, feel free to [open an issue](https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/issues/new) to discuss it, or directly create a pull request after you edit the _README.md_ file with necessary changes.
- Please make sure you check your spelling and grammar.
- Create individual PR for each suggestion.
- Please also read through the [Code Of Conduct](https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/blob/main/CODE_OF_CONDUCT.md) before posting your first idea as well.

### Creating A Pull Request

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See [LICENSE](https://github.com/ChengaFEI/cnn-driven-architecture-style-classifier/blob/main/LICENSE) for more information.

## Authors

- **Cheng Fei** - _MEng CS student_ - [Cheng Fei](https://github.com/ChengaFEI) - _Built the project_

## Acknowledgements
