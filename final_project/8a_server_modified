"""
server.py

Flask web application to detect emotions in user input text
using the EmotionDetection package.
"""

from flask import Flask, request, render_template
from EmotionDetection import emotion_detector

app = Flask(__name__)


@app.route("/")
def render_index_page():
    """
    Render the index.html page located in the templates folder.

    Returns:
        str: Rendered HTML page
    """
    return render_template("index.html")


@app.route("/emotionDetector")
def emotion_detector_route():
    """
    Flask route to process the user input text and return
    the emotion detection results in a formatted string.

    Handles blank input by displaying an error message.

    Query Parameters:
        textToAnalyze (str): Text input from the user

    Returns:
        str: Formatted string with emotion scores and dominant emotion
    """
    text_to_analyze = request.args.get("textToAnalyze")

    result = emotion_detector(text_to_analyze)

    # Handle blank input or invalid result
    if result is None or result.get("dominant_emotion") is None:
        return "Invalid text! Please try again."

    response = (
        f"For the given statement, the system response is "
        f"'anger': {result['anger']}, "
        f"'disgust': {result['disgust']}, "
        f"'fear': {result['fear']}, "
        f"'joy': {result['joy']} and "
        f"'sadness': {result['sadness']}. "
        f"The dominant emotion is {result['dominant_emotion']}."
    )

    return response


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
