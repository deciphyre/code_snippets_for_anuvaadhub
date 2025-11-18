# Code snippets for AnuvaadHub
Given below are code snippets and examples of how to use AnuvaadhHub apis for respective Models.

## Machine Translation
### Sending text to MT APIs
#### Python
```python
import requests

# Configuration
API_URL = "YOUR_API_ENDPOINT_URL"
ACCESS_TOKEN = "YOUR_ACCESS_TOKEN"

# Request Details
headers = {"access-token": ACCESS_TOKEN}
payload = {"input_text": "Hello, how are you?"} #request_payload

# POST Request
try:
    response = requests.post(API_URL, headers=headers, json=payload, verify=False)
    response.raise_for_status() 
    print(response.json())  
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```
#### Curl
```bash
curl -X POST "YOUR_API_ENDPOINT_URL" \
  -H "Content-Type: application/json" \
  -H "access-token: YOUR_ACCESS_TOKEN" \
  -d '{
    "input_text": "Hello, how are you?"
  }' \
  -k
```
#### Response Payload
```json
{
    "status": "success",
    "message": "Inference performed successfully",
    "data": {
        "output_text": "str"
    },
    "error": null,
    "code": 200
}
```

## Automatic Speech Recognition
### Sending Audio to APIs
#### Python
```python
import requests

API_URL = "YOUR_API_ENDPOINT_URL"
ACCESS_TOKEN = "YOUR_ACCESS_TOKEN"
FILE_PATH = "path/to/audio.wav"

headers = {"access-token": ACCESS_TOKEN}

try:
    with open(FILE_PATH, 'rb') as f:
        # 'audio_file' must match the API's expected form field name
        files = {'audio_file': (FILE_PATH.split('/')[-1], f, 'audio/wav')}
        response = requests.post(API_URL, headers=headers, files=files, verify=False)
        response.raise_for_status() 
        print(response.json())
except Exception as e:
    print(f"Request failed: {e}")
```
#### Curl
```bash
curl -X POST "YOUR_API_ENDPOINT_URL" \
  -H "access-token: YOUR_ACCESS_TOKEN" \
  -F "audio_file=@path/to/audio.wav;type=audio/wav" \
  -k

```
#### Response Payload
```json
{
    "status": "success",
    "message": "Inference performed successfully",
    "data": {
        "recognized_text": "str"
    },
    "error": null,
    "code": 200
}
```

## Text to Speech
### Sending text to APIs
#### Python
```python
import requests

# Configuration
API_URL = "YOUR_API_ENDPOINT_URL"
ACCESS_TOKEN = "YOUR_ACCESS_TOKEN"

# Request Details
headers = {"access-token": ACCESS_TOKEN}
payload = {
    "text": "Hello, I am a voice synthesis request.",
    "gender": "male"  # or "female"
}

try:
    response = requests.post(API_URL, headers=headers, json=payload, verify=False)
    response.raise_for_status() 
    print(response.json())
except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```
#### Curl
```bash
curl -X POST "YOUR_API_ENDPOINT_URL" \
  -H "Content-Type: application/json" \
  -H "access-token: YOUR_ACCESS_TOKEN" \
  -d '{
    "text": "Hello, I am a voice synthesis request.",
    "gender": "male"
  }' \
  -k
```
#### Response Payload
```json
{
    "status": "success",
    "message": "Inference performed successfully",
    "data": {
        "s3_url": "https://tto-asset.s3.ap-south-1.amazonaws.com/tts_output/1729151441_670bc7
8ced8a6aea0b504df2.wav"
    },
    "error": null,
    "code": 200
}
```
## Optical Character Recognition
### Sending Image to APIs
#### Python
```python
import requests

API_URL = "YOUR_API_ENDPOINT_URL"
ACCESS_TOKEN = "YOUR_ACCESS_TOKEN"
FILE_PATH = "path/to/image.jpg"  # Update this to your image file

headers = {"access-token": ACCESS_TOKEN} # Authentication
FILE_FIELD_NAME = "file"
try:
    with open(FILE_PATH, 'rb') as f:
        files = {
            FILE_FIELD_NAME: (FILE_PATH.split('/')[-1], f, 'image/jpeg') 
        }
        # POST Request using the 'files' parameter for form-data
        response = requests.post(API_URL, headers=headers, files=files, verify=False)
        response.raise_for_status() 
        print(response.json())
        
except Exception as e:
    print(f"Request failed: {e}")
```
#### Curl
```bash
curl -X POST "YOUR_API_ENDPOINT_URL" \
  -H "access-token: YOUR_ACCESS_TOKEN" \
  -F "file=@path/to/image.jpg;type=image/jpeg" \
  -k
```
#### Response Payload
```json
{
    "status": "success",
    "message": "OCR Inference performed successfully",
    "data": {
        "decoded_text": "string"
    },
    "error": null,
    "code": 200
}
```
