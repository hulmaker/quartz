I have a python application that I would like to deploy using google cloud.

The app has the following functionalities:
- react frontend
- python API backend
- uses google storage for saving data
- user authentication with oauth and email/password
- allows user to upload recording and save to google storage
- allows user to process the recording and save the result next to the recording to the storage as a json file.



### Component description
**React frontend**:
- Cloud Storage with Cloud CDN
**Python API backend**: 
- Containerized deploy to Cloud Run
- consider cloud functions
**Connecting Frontend and Backend**:
- React makes HTTP requests to backend via API Gateway (call cloud run service URL)
- consider CORS requests
**User Authentication**:
- Firebase Authentication:
	- part of gcloud Identity Platform - Allows both OAuth and email/password
	- Firebase provides ID token which React sends with Authorization header to Python backend
- Backend Token Verification:
	- Python receives ID token
	- use Firebase Admin SDK, or auth library to verify the ID validity and signature
	- Once verified, extract user-specific actions.
**Google Cloud Storage**:
- Frontend requests signed URL from Python backend to directly upload the recording to specific bucket.
- Storage structure `gs://bucket/user_id/recording_id/...`









### **Simplified Workflow Example (Upload & Process)**

1. **User Login (Frontend):** User authenticates via Firebase Authentication.
2. **Request Upload URL (Frontend to Backend):** Frontend asks the Python API for a secure upload URL for Cloud Storage.
3. **Generate Signed URL (Backend):** Python API generates a signed URL for a specific path in Cloud Storage and returns it to the frontend.
4. **Upload Recording (Frontend to Cloud Storage):** Frontend uses the signed URL to upload the recording directly to Cloud Storage.
5. **Initiate Processing (Frontend to Backend):** User clicks a "process" button. Frontend sends the recording's identifier to the Python API.
6. **Process Recording (Backend):**
    - Python API (Cloud Run) retrieves the recording from Cloud Storage.
    - It processes the audio.
    - It saves the resulting JSON to Cloud Storage next to the original recording.
7. **Notify User (Backend to Frontend - Optional):** Backend informs the frontend that processing is complete (or frontend polls for the result).


Generate patient scenarios and then understand how does she works

