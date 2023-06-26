# Voice-Assistant-
# Voice Assistant using Python
import speech_recognition as sr
import pyttsx3

# Initialize the speech recognizer
r = sr.Recognizer()

# Initialize the text-to-speech engine
engine = pyttsx3.init()

# Function to speak text
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen to voice commands
def listen():
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1  # Adjust the pause threshold according to your environment
        audio = r.listen(source)
    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en')  # Use Google Speech Recognition API to convert speech to text
        print(f"You said: {query}")
        return query
    except Exception as e:
        print("Sorry, I couldn't understand. Please try again.")
        return ""

# Voice assistant logic
def voice_assistant():
    speak("Hello! How can I assist you?")

    while True:
        query = listen().lower()

        if 'hello' in query:
            speak("Hello there!")
        elif 'how are you' in query:
            speak("I'm fine, thank you!")
        elif 'goodbye' in query:
            speak("Goodbye! Have a great day!")
            break
        else:
            speak("Sorry, I cannot help with that.")

if __name__ == '__main__':
    voice_assistant()
