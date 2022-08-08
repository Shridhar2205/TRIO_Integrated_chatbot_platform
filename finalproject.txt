'''
PROJECT WORK
'''

import string
from sys import exit

#edzo - education bot

def leave_record():
    print("Currently, I have the record of 10 students in my system whose id's are as follows: 101,102,103,104,105,106,107,108,109,110.")
    leave_record={101:'PAAPPAA',102:'AAPPPAP',103:'PAPPAAP',104:'AAAAPAP',105:'PAAPPPA',106:'PPAPPAP',107:'APAPPAA',108:'PAAPPPP',109:'PPAPPPA',110:'PAAAPAA'}
    a=int(input("Enter your id:"))
    b=leave_record[a]
    count=b.count('P')
    if count<4:
        print("This is your record for past 7 days (Here, P - present, A - absent):",b,"Your attendance is:",(count/7)*100,"%",". Your attendance is less than 50%. Please be more punctual.")
    else:
        print("This is your record for past 7 days(Here, P - present, A - absent):",b,"Your attendance is:",(count/7)*100,"%",". PHEWW! Your attendance is up to the mark.")
    
def course_details():
        #5 course options
        #subject info
        #fees
    print("Hi I can show you the course details or your leave record of the past 7 days.")
    x=int(input("Enter your choice - \n 1. Course details \n 2. Leave record \n"))
    if x==1:
        pass
    elif x==2:
        leave_record()
        return None
    
    print("We offer the following courses: BBA, BA Economics Honours, BTech") 
    print("Enter the course you're looking for:")
    a=input()
    if a=='BA Economics Honours':
        subject_choice(a)
        fees(a)
    elif a=='BBA':
        subject_choice(a)
        fees(a)
    elif a=='BTech':
        subject_choice(a)
        fees(a)
    else:
        print("Sorry, we do not offer this course") 


def subject_choice(a):
        #get more info about subjects
        #content, grading
    if a=='BA Economics Honours':
        print("We offer the following subjects in this course: Basic Statistics, Behavioural Economics, Financial Economics, Microeconomics, Macroeconomics.")     
    elif a=='BBA':
        print("We offer the following subjects in this course: Business Mathematics, Financial Accounting, Principles of Management, Business Economics.")
    elif a=='BTech':
        print("We offer the following subjects in this course: Engineering Mechanics, Engineering Physics, Mathematics-I, Basic Eletronics, Engineering Graphics.")

                  
def fees(a):    
    if a=='BTech':
        print("Fees is Rs. 3,50,000")
    elif a=='BBA':
        print("Fees is Rs. 80,000")
    elif a=='BA Economics Honours':
        print("Fees is Rs. 1,00,000")

              
#geoguessr - weather bot

def weather():
    loc=input("Enter your current location: ")
    import pyowm
    owm = pyowm.OWM('2474217b047e84887e7db99c2708e53c')
    mgr = owm.weather_manager()
    observation = mgr.weather_at_place(loc)
    #print(dir(owm))
    #print(observation)
    w = observation.weather
    print("The weather is described as follows: ",w.detailed_status)
    print("The temperature is as follows: ",w.temperature('celsius'))
    print("The wind speed is as follows: ",w.wind())
    print("The humidity is as follows: ",w.humidity)
    print("The forecast of rain is as follows: ",w.rain)
    print("The final status is as follows: ",w.status)


def remove_punctuation(s):
    list_punctuation = list(string.punctuation)
    for i in list_punctuation:
        s = s.replace(i,'')
    return s
def preprocess(text):
    text = text.lower()
    text = remove_punctuation(text)
    textList = text.split()
    return textList


#trenzo - news bot

def news():
    import requests
    from bs4 import BeautifulSoup

    def print_headlines(response_text):
        soup = BeautifulSoup(response_text, 'lxml')
        headlines = soup.find_all(attrs={"itemprop": "headline"})
        for headline in headlines:
            print(headline.text)


    url = 'https://inshorts.com/en/read'
    response = requests.get(url)
    print_headlines(response.text)



#main code

print("Hello, welcome to T.R.I.O. ")
i=input("May I know your good name? ")
print("Hey,",i,"! That's a lovely name! I consist of three bots - \n Edzo, that'll help you with your education details, but sadly not your homework xD \n GeoGuessr, that'll give you the weather conditions of your place, but not of your life xD \n Trenzo, that'll give you the latest news headlines, but not your latest gf xD")


while True:
        
        query=input("How may I help you? \n Tip: You can also summon the powerful bots using their names (Edzo,Trenzo,Geoguessr). \n")
        
        query=preprocess(query)
        
        if ('trenzo' in query) or ('news' in query) or ('headlines' in query) or ('events' in query) or ('affairs' in query):
            news()
        
        elif ('weather' in query) or ('climate' in query) or ('rain' in query) or ('temperature' in query) or ('wind' in query) or ('sunny' in query) or ('travel' in query) or('geoguessr' in query):
            weather()
    
        
        elif ('edzo' in query) or ('course' in query) or ('education' in query) or ('enrollment' in query):
            course_details()
        elif ('attendance' in query) or ('leave' in query) :
            leave_record()
              
        elif ('hi' in query) or ('hello' in query) or ('hey' in query) or ('morning' in query) or ('afternoon' in query) or ('evening' in query) or ('night' in query):
            print("Hey! I'm available if you have a query.")            
         
        elif ('bye' in query) or ('thank' in query) or ('goodbye' in query) or ('thanks' in query):
            print("Thank you for using T.R.I.O, see ya. Do visit again :)")
            exit()            
        
        else:
            print("Please try again")
            
