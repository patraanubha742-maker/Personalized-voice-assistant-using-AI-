# Personalized-voice-assistant-using-AI-
A Python-based AI voice assistant that uses speech recognition and text-to-speech to perform tasks like searching Wikipedia, opening websites, and telling time.

Introduction
In today’s digital world, voice assistants like Siri, Alexa, and Google Assistant have become an essential part of our daily lives. Inspired by these technologies, this project demonstrates how to build a personalized AI-based voice assistant using Python.

A voice assistant is an AI-powered software that can understand human speech, process it, and respond intelligently. This project uses Speech Recognition to convert voice into text and Text-to-Speech (TTS) to respond back to the user.

 Objectives
To understand the basics of speech recognition techniques
To convert voice into text and text into speech
To automate everyday tasks using voice commands
To develop a simple and functional AI voice assistant using Python

 Tools and Technologies Used
Python 3.13 (IDLE 64-bit)
speech_recognition – for capturing and recognizing voice input
gTTS (Google Text-to-Speech) – for converting text into audio
wikipedia – for fetching information
webbrowser – for opening websites
datetime – for time-based responses
os – for system-level operations

 How It Works
The assistant follows a simple workflow:

Listens to the user's voice command
Converts speech to text using Speech Recognition
Processes the command using conditional logic
Performs the task (search, open apps, tell time, etc.)
Responds using text-to-speech output

 Code Implementation
 Speak Function (Text-to-Speech)
def speak(text):
    print("Assistant:", text)
    try:
        tts = gTTS(text=text, lang='en')
        tts.save("voice.mp3")
        os.system("start voice.mp3")
    except Exception as e:
        print("Error in speaking:", e)
 Take Command Function (Speech Recognition)
def take_command():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        try:
            audio = r.listen(source, timeout=5)
        except:
            return "none"

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print("You said:", query)
    except:
        print("Could not understand")
        return "none"

    return query.lower()
 Greeting Function
def wish():
    hour = int(datetime.datetime.now().hour)

    if hour < 12:
        speak("Good Morning")
    elif hour < 18:
        speak("Good Afternoon")
    else:
        speak("Good Evening")

    speak("I am your assistant. How can I help you?")
 Main Assistant Loop
if __name__ == "__main__":
    wish()

    while True:
        query = take_command()

        if query == "none":
            continue

        elif "wikipedia" in query:
            speak("Searching Wikipedia")
            try:
                result = wikipedia.summary(query.replace("wikipedia", ""), sentences=2)
                speak(result)
            except:
                speak("Sorry, I could not find information")

        elif "open youtube" in query:
            webbrowser.open("https://youtube.com")

        elif "open google" in query:
            webbrowser.open("https://google.com")

        elif "time" in query:
            time = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {time}")

        elif "open cuims" in query:
            webbrowser.open("https://uims.cuchd.in/")

        elif "open linkedin" in query:
            webbrowser.open("https://www.linkedin.com/feed/")

        elif "bye bye" in query or "thank you" in query:
            speak("Goodbye!")
            break
 Features of the Voice Assistant
 Voice command recognition
 Audio response using TTS
 Opens websites like YouTube, Google, LinkedIn
 Fetches information from Wikipedia
 Tells current time
 Greets user based on time of day

 Applications
Personal productivity assistant
Hands-free computer interaction
Educational AI projects
Smart home automation (with extensions)
Accessibility support for users

 Future Enhancements
Add GUI interface using Tkinter or PyQt
Integrate machine learning for better responses
Add support for multiple languages
Connect with APIs (weather, news, email, etc.)
Enable offline speech recognition

Conclusion

This project demonstrates how Artificial Intelligence can be used to create a simple yet powerful voice assistant. It enhances human-computer interaction by enabling communication through natural language. With further improvements, this assistant can evolve into a more advanced and intelligent system capable of handling complex real-world tasks.
