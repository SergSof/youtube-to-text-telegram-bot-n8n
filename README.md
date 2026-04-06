````markdown
# Vehicle Detection API

A practical computer vision project for vehicle detection based on **YOLOv11** and **FastAPI**.

The project provides an HTTP API for image inference, supports **Docker deployment**, and can run on both **CPU** and **GPU** environments.

## Project overview

This project provides vehicle detection in images through a simple API service built with YOLOv11 and FastAPI.

It includes:

- vehicle detection with YOLOv11
- FastAPI-based HTTP service
- Docker and Docker Compose support
- local execution with Python
- sample images for quick testing

## Tech stack

- Python
- YOLOv11
- FastAPI
- Uvicorn
- Docker
- Docker Compose
- Makefile

## Model metrics

Evaluation results for the trained model:

- **Precision:** 0.996
- **Recall:** 1.000
- **mAP50:** 0.995

## Inference threshold

The selected confidence threshold for inference is:

- **conf = 0.55**

This value was chosen based on confidence tuning using the **F1-confidence curve**.

## Repository structure

```text
.
├── app/
│   ├── main.py
│   ├── detector.py
│   ├── schemas.py
│   └── models/
├── images/
├── check_api.py
├── Dockerfile
├── docker-compose.yml
├── Makefile
├── requirements.txt
└── README.md
````

## How to run locally

### 1. Clone the repository

```bash
git clone https://github.com/SergSof/task-complex-systems.git
cd task-complex-systems
```

### 2. Create a virtual environment

#### Linux / macOS

```bash
python -m venv venv
source venv/bin/activate
```

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the API

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

The service will be available at:

```text
http://127.0.0.1:8000
```

## Run with Docker

### Build and start the service

```bash
docker compose up --build
```

Or, if needed:

```bash
docker-compose up --build
```

## API usage

### Swagger UI

Available at:

```text
http://127.0.0.1:8000/docs
```

### Example inference request

```python
import requests

url = "http://127.0.0.1:8000/predict"
files = {"file": open("images/test.jpg", "rb")}

response = requests.post(url, files=files)
print(response.json())
```

### Example response

```json
{
  "detections": [
    {
      "class_name": "car",
      "confidence": 0.91,
      "bbox": [120, 85, 340, 260]
    }
  ]
}
```

## Quick test

You can use the included helper script:

```bash
python check_api.py
```

## Training notebook

The training workflow was prepared in Google Colab.

Notebook:
[YOLO training notebook](https://colab.research.google.com/drive/13CAaRRoUbgyOGs_QMqul9o4DwFN_rYWk?usp=sharing)

## Possible improvements

Potential directions for further improvement:

* add more training images with small objects
* continue dataset refinement and annotation cleanup
* further tune augmentation parameters such as:

  * `scale`
  * `translate`
  * `hsv_h`
  * `hsv_s`
  * `hsv_v`
  * `fliplr`
  * `mosaic`
* continue confidence threshold tuning based on the F1-confidence curve

## Notes

* The dataset is not included in this repository.
* The project is focused on practical deployment and inference serving.
* The repository can be used as a base for extending the detection service to video streams or production pipelines.
