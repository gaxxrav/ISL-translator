<img src="https://github.com/gaxxrav/ISL-translator/blob/main/isldiagram.png?raw=true" alt="ISL Translator Architecture" width="700">

# System Architecture and Data Flow

This diagram illustrates the **architecture and data flow** of a microservice-based machine learning system that processes images or video frames and returns classification results via an API.

---

## 1. Client / Consumer
- The user or an external application (the client) sends an **HTTP POST** request containing an image or a frame to the microservice.  
- The client later receives an **HTTP response** with the classification result (in JSON).

---

## 2. HTTP API (`app.py`)
- Acts as the **entry point** of the system (the main API endpoint).  
- Receives the image/frame and routes it through the pipeline.  
- This API runs inside a **Microservice Container** (e.g., Docker).

---

## 3. Preprocessing (`cvfspalac.py` under `Utilities`)
- The API calls preprocessing utilities to:
  - Clean or normalize the input image.
  - Possibly resize, crop, or convert formats.  
- **Output:** Preprocessed data ready for the model.

---

## 4. Model Package (`__init__.py`)
- Manages loading and orchestrating model components.  
- Calls the classifier after preparing the model pipeline.

---

## 5. Keypoint Classifier (`keypoint_classifier.py`)
- Loads trained models from **Model Artifacts**.  
- Performs the **core classification** task using:
  - `.tflite` (TensorFlow Lite models)
  - `.csv` or `.npy` (metadata, label maps, or numerical weights)  
- **Output:** Classification result.

---

## 6. Response Generator (`response.py`)
- Takes the classification result.  
- Formats it as a **JSON response**.  
- Sends it back to the HTTP API, which returns it to the client.

---

## 7. Dependencies (`requirements.txt`)
- Lists all Python dependencies required to run this service.

---

## 8. Documentation (`README.md`)
- Explains setup, usage, and configuration of the microservice.

---

## Summary of Flow

**Client → HTTP API → Preprocessing → Model Package → Classifier → Response → Client**

---

### Key Design Principles
- **Separation of Concerns:** Clear modular boundaries between API, preprocessing, model, and response components.  
- **Reusability and Scalability:** Each block can be updated independently.  
- **Extensibility:** Provides clear integration points for model updates or additional processing steps.
