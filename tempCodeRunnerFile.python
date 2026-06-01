import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import wikipedia
import pywhatkit
import pyjokes
import os

# Initialize engine
engine = pyttsx3.init()
engine.setProperty('rate', 170)
engine.setProperty('volume', 1.0)

ASSISTANT_NAME = "nova"

def speak(text):
    print("NOVA:", text)
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)

    try:
        command = r.recognize_google(audio)
        print("You:", command)
        return command.lower()
    except:
        return ""

def wake_word_detected(command):
    return ASSISTANT_NAME in command

def wish_user():
    hour = datetime.datetime.now().hour
    if hour < 12:
        speak("Good morning! I am NOVA.")
    elif hour < 18:
        speak("Good afternoon! I am NOVA.")
    else:
        speak("Good evening! I am NOVA.")
    speak("Say NOVA to wake me up.")

def run_nova():
    wish_user()

    while True:
        command = listen()

        if not wake_word_detected(command):
            continue

        speak("Yes? How can I help you?")
        command = listen()

        if "time" in command:
            time_now = datetime.datetime.now().strftime("%I:%M %p")
            speak(f"The time is {time_now}")

        elif "date" in command:
            date_now = datetime.datetime.now().strftime("%B %d, %Y")
            speak(f"Today's date is {date_now}")

        elif "wikipedia" in command:
            speak("Searching Wikipedia")
            query = command.replace("wikipedia", "")
            try:
                result = wikipedia.summary(query, sentences=2)
                speak(result)
            except:
                speak("Sorry, I couldn't find that.")

        elif "play" in command:
            song = command.replace("play", "")
            speak(f"Playing {song} on YouTube")
            pywhatkit.playonyt(song)

        elif "open google" in command:
            speak("Opening Google")
            webbrowser.open("https://www.google.com")

        elif "open youtube" in command:
            speak("Opening YouTube")
            webbrowser.open("https://www.youtube.com")

        elif "joke" in command:
            speak(pyjokes.get_joke())

        elif "shutdown" in command:
            speak("Shutting down the system")
            os.system("shutdown /s /t 5")

        elif "restart" in command:
            speak("Restarting the system")
            os.system("shutdown /r /t 5")

        elif "your name" in command:
            speak("My name is NOVA, your personal voice assistant.")

        elif "stop" in command or "exit" in command:
            speak("Goodbye! I am going offline.")
            break

        else:
            speak("Sorry, I didn't understand that.")

if __name__ == "__main__":
    run_nova()
