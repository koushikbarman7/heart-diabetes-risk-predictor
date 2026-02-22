# Heart Diabetes Risk Predictor

A machine learning web app and API that predicts heart disease and diabetes risk from user health inputs using trained classification models.

## Features
- Predicts **Heart Disease risk** from 13 clinical input features
- Predicts **Diabetes risk** from 8 clinical input features
- Simple **Streamlit web interface** for user interaction
- **FastAPI endpoint** for programmatic predictions
- Model training script for regenerating saved models (`.pkl`)

## Tech Stack
- Python
- Streamlit
- FastAPI
- Scikit-learn
- Pandas
- NumPy
- SQLite (used by Streamlit app for local user data)

## Project Structure
```text
heart-diabetes-risk-predictor/
|-- main.py                 # FastAPI app
|-- streamlit_app.py        # Streamlit UI app
|-- ml_models.py            # Model training script
|-- requirements.txt        # Python dependencies
|-- diabetes.csv            # Diabetes dataset
|-- heart.csv               # Heart dataset
|-- diabetes_model.pkl      # Trained diabetes model
|-- diabetes_scaler.pkl     # Diabetes scaler
|-- heart_model.pkl         # Trained heart model
|-- heart_scaler.pkl        # Heart scaler
`-- .gitignore
```

## Setup
1. Clone the repository:
```bash
git clone https://github.com/koushikbarman7/heart-diabetes-risk-predictor.git
cd heart-diabetes-risk-predictor
```

2. Create and activate virtual environment:

Windows (PowerShell):
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

macOS/Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Train Models
If you update or clean datasets, retrain models:
```bash
python ml_models.py
```
This will generate/update:
- `diabetes_model.pkl`
- `diabetes_scaler.pkl`
- `heart_model.pkl`
- `heart_scaler.pkl`

## Run Streamlit App
```bash
streamlit run streamlit_app.py
```
Then open the local URL shown in terminal (usually `http://localhost:8501`).

## Run FastAPI App
```bash
uvicorn main:app --reload
```
- API base URL: `http://127.0.0.1:8000`
- Interactive docs: `http://127.0.0.1:8000/docs`

## API Usage
### `GET /`
Health check endpoint.

### `POST /predict`
Request body example:
```json
{
  "diabetes_features": [6, 148, 72, 35, 0, 33.6, 0.627, 50],
  "heart_features": [63, 1, 3, 145, 233, 1, 0, 150, 0, 2.3, 0, 0, 1]
}
```

Response example:
```json
{
  "diabetes_prediction": 1,
  "heart_disease_prediction": 0
}
```

## Notes
- `1` typically indicates higher risk and `0` lower risk, based on model output labels.
- The app is for educational/research use and is **not medical advice**.
- `users.db` is generated automatically by Streamlit app at runtime and is excluded from Git.

## Future Improvements
- Add model evaluation metrics and confusion matrices
- Add input validation and feature descriptions in UI
- Add password hashing for user authentication
- Add Docker support for one-command deployment
