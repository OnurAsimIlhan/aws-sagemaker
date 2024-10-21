# End To End Sagemaker Project

This project demonstrates an end-to-end machine learning workflow using AWS SageMaker. The workflow includes data preparation, model training, and deployment.

## Project Structure

- `mob_price_classification_train.csv`: Training dataset.
- `test-V-1.csv`: Test dataset.
- `train-V-1.csv`: Additional training dataset.
- `research.ipynb`: Jupyter notebook containing the end-to-end workflow.
- `script.py`: Python script used as the entry point for SageMaker training.
- `requirements.txt`: Python dependencies for the project.
- `venv/`: Virtual environment directory.

## Setup

1. **Clone the repository:**
    ```sh
    git clone https://github.com/OnurAsimIlhan/aws-sagemaker.git
    cd aws-sagemaker
    ```

2. **Create and activate a virtual environment:**
    ```sh
    python3 -m venv venv
    source venv/bin/activate
    ```

3. **Install dependencies:**
    ```sh
    pip install -r requirements.txt
    ```

## Usage

1. **Data Preparation:**
    - Upload the datasets (`train-V-1.csv` and `test-V-1.csv`) to an S3 bucket.

2. **Model Training:**
    - Open `research.ipynb` and execute the cells to train the model using SageMaker.

3. **Model Deployment:**
    - The notebook includes steps to deploy the trained model as an endpoint.

## Key Components

- **Data Upload:**
    ```python
    trainpath = sess.upload_data(path='train-V-1.csv', bucket=bucket, key_prefix=sk_prefix)
    testpath = sess.upload_data(path='test-V-1.csv', bucket=bucket, key_prefix=sk_prefix)
    ```

- **Model Training:**
    ```python
    artifact = sm_boto3.describe_training_job(
        TrainingJobName=sklearn_estimator.latest_training_job.name
    )["ModelArtifacts"]["S3ModelArtifacts"]
    ```

- **Model Deployment:**
    ```python
    model = SKLearnModel(
        name=model_name,
        model_data=artifact,
        role="<insert role>",
        entry_point="script.py",
        framework_version=FRAMEWORK_VERSION
    )
    ```
