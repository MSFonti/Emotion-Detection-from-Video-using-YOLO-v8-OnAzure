# Emotion Detection from Video using YOLOv8
This project uses YOLOv8 for face detection based on the wider_face datasets and an emotion classification model based on fer2013 dataset for detecting human facial emotions from real-time or recorded videos. The system detected faces and identifies emotions such as happy, sad, angry, surprise, neutral, and more, in real-time or video files. The goal of this project is to demonstrate real-time emotion detection and provide an API for integrating emotion detection into other applications.
## Key Features:
- Face Detection: Detects faces using YOLOv8, a state-of-the-art object detection model by trained on wider_face dataset.
- Emotion Recognition: Classifies emotions from faces using a deep learning model trained on the fer2013 dataset.
- Real-Time Processing: Process webcam video streams or recorded videos for emotion detection.
- Deployment: Deploys the emotion detection model on AWS Elastic Beanstalk as a REST API.

## Requirements
### System Dependencies
- Python 3.8+

## Setup
1. #### Clone the repository :
- git clone https://github.com/rahuljoshi1814/Emotion-Detection-from-Video-using-YOLO-v8.git
- cd /Emotion-Detection-from-Video-using-YOLO-v8
2. #### Create a virtual environment :
- python -m venv venv
- venv\Scripts\activate     # For Windows
3. #### Python Libraries :
- To install all the necessary dependencies for this project, create a virtual environment and install from the "requirements.txt" file.

## Model Training
### Dataset Preparation
1. Face Detection Dataset:
- create a folder "wider_face" in the datasets directory, download the data by using this link : http://shuoyang1213.me/WIDERFACE/ 
- Extract the Files: 
  - unzip WIDER_train.zip
  - unzip WIDER_val.zip
  - unzip wider_face_split.zip, extract all these 3 files and put them into folder wider_face and then Use the WIDER FACE dataset for fine-tuning YOLOv8 on face detection. Follow the instructions in the "datasets" script to convert annotations to YOLO format.
  - now in the folder "wider_face_data_preprocess" Run scripts WIDER_train.py (scripts for WIDER_train data to YOLO format - like to create the labels) and after that in that same folder Run the WIDER_val.py script (for WIDER_val).
2. Emotion Classification Dataset: create a folder "fer2013" in the datasets directory, download the datasets by using link : "https://www.kaggle.com/datasets/msambare/fer2013"
- Extract the files (test and train) and then put them into fer2013 folder. Use the fer2013 dataset, which is already split into train and test directories, each containing labeled emotions such as happy, sad, angry, etc.
### YOLOv8 Fine-tuning
To fine-tune YOLOv8 for face detection
Load YOLOv8 and fine-tune on the WIDER FACE dataset. for this run this command on terminal :
- To train: - "yolo task=detect mode=train model=yolov8n.pt data=wider_face.yaml epochs=50 imgsz=640"
- To test : - "yolo task=detect mode=predict model=runs/detect/train/weights/best.pt source=path_to_test_images_or_video" , 
after this in the folder "integration_pipeline" Run the script : face_detection.py (to capture faces testing in web_cam )
### emotion_recognition_model
- Train the emotion classification model on the FER-2013 dataset. for this in emotion_recognition folder run the script : "emotion_recognition.py"
- For detailed instructions on how to fine-tune the models, refer to the specific code for training the YOLO model and the emotion classifier in the repository.
- run web_app.py to live emotion-recognition or run "integration.py" in integration_pipelines.
## API Deployment
The application provides a REST API using FastAPI for detecting emotions from videos. The following steps guide you to deploy the app to AWS Elastic Beanstalk.

1. Install FastAPI and Uvicorn
If you are running this locally or want to run the server, use the following dependencies:
- pip install fastapi uvicorn
2. API Endpoints
- POST /predict: Accepts a video stream or video file and returns the detected emotion with bounding boxes around the faces.
- Request Format: A video file or webcam stream.
- Response: The detected emotion and bounding boxes for each detected face.

## Running the Project
#### Local Development
- You can run the app locally using Uvicorn: "uvicorn fast_api_app:app --reload"
#### Real-Time Video Processing
To process a live video from your webcam or a recorded video file, run the following Python script:"python web_app.py"
This script will detect faces and emotions in real-time using your webcam.


## Azure Container Apps Deployment
1. Deploy a Container App Instance


## AWS Deployment
1. Deploy to AWS Elastic Beanstalk
- Configure AWS CLI with aws configure (access keys and region).
- Initialize Elastic Beanstalk with eb init.
- Create the environment with eb create.
- Deploy the app with eb deploy.
2. Access the Application
- After deployment, access your API via the provided URL: eb open
- You can test the deployed application by sending video files or streaming webcam video.




