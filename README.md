# ASL-Signs-Prediction-Using-CNN

## Project Overview

This project develops a **Convolutional Neural Network (CNN)** to recognise 27 American Sign Language (ASL) classes covering **digits, selected alphabets, and simple signs** from images.

The project explores how computer vision and deep learning can be used to recognise hand gestures without requiring wearable sensors or specialised hardware.

The model was developed using the **27-Class Sign Language Dataset** collected from 173 individuals. Several CNN configurations were tested through data augmentation and hyperparameter tuning, with the final selected model achieving a reported **95% classification accuracy**.

## Objective

The objective was to develop and optimise a CNN capable of recognising a combination of:

* 10 digits: 0–9
* 5 alphabet characters: A–E
* 12 simple signs: Hello, Yes, No, Good, Bye, Good Morning, What's Up, Pardon, Project, Little Bit, Please

This combination extends beyond projects focused solely on alphabet or digit recognition.

## Dataset

The project uses the **27-Class Sign Language Dataset** by Mavi and Dikle (2022).

* **27 classes**
* Images collected from **173 individuals**
* 130 images collected per individual
* Original image size: 3024 × 3024
* Images resized to **128 × 128**
* Pixel values normalised to the range **[0, 1]**
* Training/validation/testing split: **80/10/10**

Dataset source:

https://www.kaggle.com/ardamavi/27-class-sign-language-dataset

### Classes

| Category     | Classes                                                                                 |
| ------------ | --------------------------------------------------------------------------------------- |
| Numbers      | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9                                                            |
| Letters      | A, B, C, D, E                                                                           |
| Simple Signs | Hello, Yes, No, Good, Bye, Good Morning, What's Up, Pardon, Project, Little Bit, Please |

## Data Preprocessing and Augmentation

Images were resized and normalised before being supplied to the CNN.

Data augmentation was applied to increase the diversity of the training data and improve model generalisation.

Techniques included:

* Random rotation between -20° and +20°
* Horizontal and vertical image shifts
* Cropping
* Tilting
* Random zooming

The augmentation was designed to expose the model to variations in hand position, orientation and image composition.

## CNN Architecture

The model uses a four-block convolutional architecture.

### Convolutional layers

* Conv2D — 32 filters
* Conv2D — 32 filters
* Conv2D — 64 filters
* Conv2D — 128 filters

Each convolutional block is followed by:

* ReLU activation
* Max pooling
* Dropout

The convolutional layers progressively increase the number of filters to allow the network to learn increasingly complex visual features.

### Classification layers

After the convolutional blocks:


Flatten
   ↓
Dense — 128 neurons (ReLU)
   ↓
Dense — 64 neurons (ReLU)
   ↓
Dense — 27 neurons (Softmax)


The final Softmax layer produces a probability for each of the 27 sign classes.

## Hyperparameter Tuning

Several model configurations were evaluated.

| Model       | Augmentation | Kernel  | Dropout  | Optimizer / Learning Rate | Epochs |
| ----------- | ------------ | ------- | -------- | ------------------------- | -----: |
| Model 0     | No           | 3×3     | 0.25     | SGD                       |     10 |
| Model 1     | Yes          | 3×3     | 0.50     | Adam / 0.0001             |     10 |
| Model 2     | Yes          | 3×3     | 0.50     | Adam / 0.01               |     20 |
| Model 3     | Yes          | 5×5     | 0.50     | Adam / 0.01               |     20 |
| **Model 4** | **Yes**      | **5×5** | **0.50** | **Adam / 0.01**           | **50** |
| Model 5     | Yes          | 5×5     | 0.50     | Adam / 0.01               |     80 |

Early stopping was also used during experimentation to reduce the risk of overfitting.

## Model Evaluation

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrix

The baseline model initially achieved approximately **67% accuracy**. Performance improved through augmentation and hyperparameter tuning.

The selected **Model 4** achieved a reported **95% accuracy**.

### Performance progression

| Model       | Reported Accuracy |
| ----------- | ----------------: |
| Model 0     |               67% |
| Model 3     |               86% |
| **Model 4** |           **95%** |
| Model 5     |               42% |

Model 5 demonstrated the potential impact of excessive training, with early stopping terminating training before the planned 80 epochs.

## Comparison with Previous Approaches

The project report compared the selected CNN model with several previously published approaches:

| Approach                       | Reported Accuracy |
| ------------------------------ | ----------------: |
| Cohen et al. — SVM             |               92% |
| Bantupalli & Xie — CNN/RNN     |               93% |
| Tao et al. — CNN               |               93% |
| **This project — CNN Model 4** |           **95%** |

These figures are reported from the respective studies and are not necessarily directly comparable because the datasets, experimental setups and evaluation methodologies differ.

## Key Findings

The experimentation demonstrated several important observations:

1. The baseline CNN achieved 67% accuracy without augmentation.
2. Data augmentation improved the model's ability to generalise.
3. Increasing the kernel size from 3×3 to 5×5 improved performance during experimentation.
4. Increasing training epochs improved performance up to the selected Model 4 configuration.
5. Further increasing the training duration to 80 epochs resulted in poorer performance, demonstrating the importance of monitoring validation performance.
6. The selected Model 4 achieved a reported **95% accuracy across 27 sign classes**.

## Technologies Used

* Python
* TensorFlow / Keras
* NumPy
* Matplotlib
* Convolutional Neural Networks
* Computer Vision
* Deep Learning
* Image Data Augmentation
* Classification Metrics

## How to Run

1. Clone this repository.
2. Install the required Python libraries.
3. Open the Jupyter Notebook.
4. Obtain the dataset from the original Kaggle source.
5. Update the dataset path in the notebook.
6. Run the notebook cells sequentially.

The original dataset files are **not included in this repository** because the dataset is available from its original source.

## Future Improvements

Potential extensions of the project include:

* Expanding the number of recognised ASL classes
* Recognising more complex signs
* Moving from isolated signs to phrases and sentences
* Using transfer learning with pretrained CNN architectures
* Testing the model on real-time webcam input
* Evaluating performance under more challenging lighting and background conditions
* Developing a real-time sign-to-text application

## References

Mavi, A. & Dikle, Z. (2022). *A New 27 Class Sign Language Dataset Collected from 173 Individuals.*

Bantupalli, K. & Xie, Y. (2018). American Sign Language Recognition using Deep Learning and Computer Vision.

Cohen, M., Zikri, M. & Velkovich, A. (2018). Recognition of Continuous Sign Language Alphabet Using Leap Motion Controller.

Dong, C., Leu, M. C. & Yin, Z. (2015). American Sign Language Alphabet Recognition Using Microsoft Kinect.

Tao, W., Leu, M. C. & Yin, Z. (2018). American Sign Language Alphabet Recognition Using Convolutional Neural Networks with Multiview Augmentation and Inference Fusion.

Shorten, C. & Khoshgoftaar, T. M. (2019). A Survey on Image Data Augmentation for Deep Learning.
