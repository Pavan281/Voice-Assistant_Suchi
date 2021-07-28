# Voice-Assistant_Suchi
I created the voice assistant named Suchi using the Python Programming Language. So I just wanted to share the details here.
# Here is the Complete Code for the VOICE ASSISTANT using PYTHON.

import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()


def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'SUCHI' in command:
                command = command.replace('Pandu', '')
                print(command)
    except:
        pass
    return command


def run_SUCHI():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        print(time)
        talk('Current time is ' + time)
    elif 'who is' in command:
        person = command.replace('who the heck is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk('sorry, I have a headache')
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    elif 'stop' in command:
        print("Thank You so much and I hope i was given the Best to you")
        talk("Thank You so much and I given my Best.")
        talk("Visit again. Have a good day. Bye")
    else:
        talk('Please say the command again.')

while True:
    run_SUCHI()
