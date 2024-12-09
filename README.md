# OCR Development Journey

## Introduction
This document outlines the methodology and steps undertaken to develop an OCR solution tailored to specific document processing tasks. The goal was to recognize checkboxes and extract text and numerical data from structured documents accurately and efficiently. Several libraries and approaches were evaluated to achieve the desired results.

## Initial Experiments
The task began with recognizing checkboxes in a document. The following libraries were tested:

- OpenCV
- PaddleOCR
- PyTesseract
- Microsoft TrOCR
- EasyOCR
- SuryaOCR

Unfortunately, none of these libraries provided satisfactory accuracy for checkbox detection. This led to exploring alternative approaches.

## YOLO Implementation
To improve checkbox detection, YOLO was fine-tuned on a custom dataset comprising blocks of text, checked boxes, and unchecked boxes. The fine-tuned YOLO model performed exceptionally well for this task. Additionally, **SIFT alignment** was used to align documents to a predefined template before feeding them into the YOLO model. This alignment ensured consistent detection results.

## Text Extraction Challenges
Following checkbox detection, the next step was extracting text from the segmented blocks identified by YOLO. The same OCR libraries—OpenCV, PaddleOCR, PyTesseract, TrOCR, EasyOCR, and SuryaOCR—were evaluated again for this purpose. However, they did not perform well in this specific use case.

Experiments with convolutional neural networks trained on MNIST and EMNIST datasets were also conducted. While these models could classify single digits, their accuracy was insufficient, and they could not handle multi-digit recognition, posing a significant limitation.

## Current Strategy
To address these challenges, data has been labeled for fine-tuning **PaddleOCR** and **TrOCR**. The aim is to identify which of these two models performs better after fine-tuning. Additionally, **Vertex AI's multimodal approach** is being used for text extraction. While it excels in extracting general text, it struggles with accurate numerical data extraction. Thus, further efforts are focused on finding an effective solution for extracting numbers from the documents.

## Fine Tuning Models
Significant progress has been made in fine-tuning OCR models, with promising results from **TrOCR**. Specifically:

- **TrOCR-large-stage1** achieved a **Character Error Rate (CER)** of 0.1 and a **Word Error Rate (WER)** of 0.3.
- These results were based on a dataset of **576 images**, which represents a limitation. With additional labeled data, further accuracy improvements are anticipated.

Attempts were also made to fine-tune:

- **PaddleOCR**, which did not yield favorable results due to the complexity of the fine-tuning process and its substantial resource requirements.
- **DTrOCR (Decoder-only TrOCR)**, which similarly produced poor results, indicating that this model may not be well-suited for the specific task or requires a different approach.

## Future Work
Moving forward, the focus will be on:

- Expanding the dataset to further improve the performance of TrOCR.
- Streamlining the fine-tuning process for PaddleOCR or considering alternative lightweight OCR solutions.
- Investigating the limitations of DTrOCR and exploring whether adjustments in the dataset or fine-tuning strategy could yield better results.
- Continuing efforts to improve numerical data extraction, leveraging the strengths of TrOCR and other emerging tools.

## Data Labeling and Fine-Tuning PaddleOCR
Follow the JSON document labeling guide and try fine-tuning **PaddleOCR** for better performance.

## Files

- **YOLO_CheckboxDetection&TROcr.ipynb**
  - Contains the checkbox detection and text extraction from text blocks using TrOCR.
- **Fine_tuning_TrOCR_on_GLAUKOS_Database_using_PyTorch.ipynb**
  - Contains the code on fine-tuning TrOCR on a custom dataset. TrOCR large stage 1 was fine-tuned using this notebook.
- **Fine_tuning_Paddle_OCR.ipynb**
  - Contains the code to fine-tune PaddleOCR.
- **CNN_MNIST_tensorflow.ipynb**
  - Contains the code to train a neural network on the MNIST dataset to be used for single-character recognition.
- **Checking_TROCR_on_Images.ipynb**
  - Testing TrOCR on images and adjusting hyperparameters to get better inference results.

## Directories
The directories containing the scanned documents have been removed due to security and privacy issues.
