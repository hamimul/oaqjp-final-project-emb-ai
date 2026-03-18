import json
import urllib.request
import urllib.error

def emotion_detector(text_to_analyze):
    url = "https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict"
    
    headers = {
        "Content-Type": "application/json",
        "grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"
    }
    
    data = json.dumps({
        "raw_document": {
            "text": text_to_analyze
        }
    }).encode('utf-8')
    
    req = urllib.request.Request(url, data=data, headers=headers)
    
    try:
        response = urllib.request.urlopen(req)
        
        # Check HTTP status code
        if response.status == 400:
            # Blank or invalid input
            return {
                "anger": None,
                "disgust": None,
                "fear": None,
                "joy": None,
                "sadness": None,
                "dominant_emotion": None
            }
        
        # Convert response to dictionary
        response_text = response.read().decode('utf-8')
        response_dict = json.loads(response_text)
        
        emotions = response_dict["emotionPredictions"][0]["emotion"]
        
        anger = emotions["anger"]
        disgust = emotions["disgust"]
        fear = emotions["fear"]
        joy = emotions["joy"]
        sadness = emotions["sadness"]
        
        dominant_emotion = max(emotions, key=emotions.get)
        
        return {
            "anger": anger,
            "disgust": disgust,
            "fear": fear,
            "joy": joy,
            "sadness": sadness,
            "dominant_emotion": dominant_emotion
        }
    
    except urllib.error.HTTPError as e:
        if e.code == 400:
            # Blank input
            return {
                "anger": None,
                "disgust": None,
                "fear": None,
                "joy": None,
                "sadness": None,
                "dominant_emotion": None
            }
        else:
            raise e