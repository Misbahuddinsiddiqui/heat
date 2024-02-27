import speech_recognition as sr
import pyttsx3
import webbrowser
import os

engine = pyttsx3.init('sapi5')
voices= engine.getProperty('voices') #getting details of current voice
engine.setProperty('voice', voices[0].id)

def speak(text):
   engine.say(text) 
   engine.runAndWait()

def takeCommand() :
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")    
        query = r.recognize_google(audio, language='en-in') #Using google for voice recognition.
        print(f"User said: {query}\n")  #User query will be printed.

    except Exception as e:
    # print(e)    
        print("Say that again please...")   #Say that again will be printed in case of improper voice 
        return "None" #None string will be returned
    return query



speak("hello sir ")
speak("what is password")
a = takeCommand()
if a == "time":
   speak("Ok how i can help your highness")
   c = takeCommand() 
   c = "open local file"  # Assuming this is how you get the command
   if c == "open local file":
    # Your block of code starts here
    speak("Tell me file name")
    filename = takeCommand().lower() 
    root_folder = "C:\\"
    # Searching for the file
    for root, dirs, files in os.walk(root_folder):
        if filename in files:
            file_path = os.path.join(root, filename)
            os.startfile(file_path)
            break  # Stop searching once file is found
        else:
         speak("File not found.")
         break
   else:
      b = takeCommand().lower()
      if b =="open google":
        webbrowser.open("www.google.com")   
        speak("opening google")
      else:
       a = b.split()[1:]
       address = "https://"+a+".com"
       webbrowser.open(address)
else:
    speak("i cannot help you and who are you")
   
