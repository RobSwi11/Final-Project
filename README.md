# Final-Project

link to video
https://www.youtube.com/watch?v=l11fjlZu80k 

#Title: Blood Sugar Tracker and food option suggestor

#Robert Swiatek

#Senior Accounting Major

import pandas as pd
from matplotlib import pyplot as plt
from datetime import date
from datetime import datetime

print("Hi there, so just some basics for you to remember; \n\nBlood sugar between 80-120mg/L is normal for not having eaten yet.\nAfter eating you should be between 120-180mg/L.\n\nNow let's get started.\n")

bs = int(input('What is your current blood sugar: '))

def askQ(bs):
    record = True
    if bs < 60:
        print('\nEat your your emergency fruit roll up, and recheck your blood sugar in 15 minutes.')
        return recorderData()
    elif bs < 180:
        print('\nYou can have some more food.\n')
        return food()
    elif bs >= 180 and bs <= 200:
        print('\nNo more carbs for now. Eat some cheese, jerky, or pickles as a snack.\nOtherwise here is how you have been trending:)')
        return recordedData(), bloodSugarCarbs()
    elif bs > 200:
        return emergency()

def emergency():

    if bs <= 250 and bs > 200:
        print('Take one unit of the fast acting insulin.')
        return recorderData()
    elif bs <= 275 and bs > 250:
        print('Take two units of the fast acting insulin.')
        return recorderData()
    elif bs <= 300 and bs > 275 :
        print('Take three units of the fast acting insulin.')
        return recorderData()
    elif bs <= 350 and bs > 300:
        print('Take four units of the fast acting insulin.')
        return recorderData()
    else:
        print('Have someone take you to the ER.')
        return recorderData()

def food():
    breakfast = {'bagel': 52, 'eggs': 0, 'pancakes': 30, 'grits': 31, 'granola bar': 15, 'apple': 25
                 , 'clementine': 9, 'french toast': 33, 'bacon egg and cheese': 28, 'bacon': 7,'sausage': 3} 
    lunch = {'sandwich': 45, 'snack bar': 25, 'cheese puffs': 15, 'popcorn': 15, 'carrots': 7, 'apple': 25
                 , 'fruit rollup': 9, 'grilled cheese': 24, 'pasta': 40}
    dinner = {'chipotle bowl': 80, 'chicken': 0, 'buttered noodles': 60, 'mini pizza': 50, 'salad': 33, 'steak': 0
                 , 'veggies': 8, 'brisket': 47, 'quesadilla': 35, 'cauliflower pizza': 45}
    snack = {'nuts': 3, 'protein bar': 5, 'jolly racher': 0, 'gummy bears': 19, 'granola bar': 15, 'cheese': 0
                 , 'jerkey': 7, 'pickles': 0, 'fruit rollup': 20, 'beer': 6}
    
    typeFood = str(input('What kind of food do you want? Breakfast, Lunch, Dinner, or just a Snack: '))
    typeFood = typeFood.lower()
    
    choices = ['breakfast','lunch','dinner','snack','none']
    yn = ['y', 'n']
    global pick    

    if typeFood in choices:
        
        if typeFood == choices[0]:
            print('\n',breakfast)
            pick = input('What would you like for breakfast: ')
            if pick not in breakfast:
                add = str(input("Doesn't look like that is in the choices. Would you like to add it? y/n \n"))
                if add == yn[0]:
                    newfood = input("Enter in the food: ")
                    newcarb = int(input('Enter the number of carbs: '))
                    breakfast.update({newfood:newcarb})
                elif add == yn[1]:
                    return food()       
            else:
                print('That is',breakfast.get(pick),'grams of carbs. \n')
            print('That will increase your blood sugar by about', 1.1 * breakfast.get(pick),'mg/L.')            

        elif typeFood == choices[1]:
            print('\n',lunch)
            pick = input('What would you like for lunch: ')
            if pick not in lunch:
                add = str(input("Doesn't look like that is in the choices. Would you like to add it? y/n \n"))
                if add == yn[0]:
                    newfood = input("Enter in the food: ")
                    newcarb = int(input('Enter the number of carbs: '))
                    lunch.update({newfood:newcarb})
                elif add == yn[1]:
                    return food()       
            else:
                print('That is',lunch.get(pick),'grams of carbs. \n')
            print('That will increase your blood sugar by about', 1.1 * lunch.get(pick),'mg/L.')            
        
        elif typeFood == choices[2]:
            print('\n',dinner)
            pick = input('What would you like for dinner: ')
            if pick not in dinner:
                add = str(input("Doesn't look like that is in the choices. Would you like to add it? y/n \n"))
                if add == yn[0]:
                    newfood = input("Enter in the food: ")
                    newcarb = int(input('Enter the number of carbs: '))
                    dinner.update({newfood:newcarb})
                elif add == yn[1]:
                    return food()             
            else:
                print('That is',dinner.get(pick),'grams of carbs. \n')
            print('That will increase your blood sugar by about', 1.1 * dinner.get(pick),'mg/L.')

        elif typeFood == choices[3]:
            print('\n',snack)
            pick = input('What would you like as a snack: ')
            if pick not in snack:
                add = str(input("Doesn't look like that is in the choices. Would you like to add it? y/n \n"))
                if add == yn[0]:
                    newfood = input("Enter in the food: ")
                    newcarb = int(input('Enter the number of carbs: '))
                    snack.update({newfood:newcarb})
                elif add == yn[1]:
                    return food() 
            elif pick == 'beer':
                print('That is',snack.get(pick),'grams of carbs. \n')
                print("Don't worry professor, I'm 22 lol\n")
                
            else:
                print('That is',snack.get(pick),'grams of carbs. \n')
            print('That will increase your blood sugar by about', 1.1 * snack.get(pick),'mg/L.')
    elif typeFood not in choices:
        return food()
    
    return exercise()    

def exercise():
    yn = ['y', 'n']
    exerciseType = ['running','walking','lifting']
    ex = input('Do you plan on working out after eating? Y/N: ')
    ex = ex.lower()
    work = False
    
    global minutes
    
    while not work:
        if ex == yn[0]:
            print('\n',exerciseType)
            hl = input('What are you going to be doing? ')
            minutes = int(input('\nHow long will you be working out in minutes? '))
            if hl == exerciseType[0]:
                newBS = (minutes*1.2)
                print('If you run for',minutes,'minutes your blood sugar will drop by',newBS,'mg/L.')
                print('Keep it up Rob! Here is how you sugars have been trending.')
                return recordedData()
            elif hl == exerciseType[1]:
                newBS = (minutes*.85)
                print('If you walk for',minutes,'minutes your blood sugar will drop by',newBS,'mg/L.')
                print('Keep it up Rob! Here is how you sugars have been trending.')
                return recordedData()
            elif hl == exerciseType[2]:
                newBS = (minutes)
                print('If you lift for',minutes,'minutes your blood sugar will drop by',newBS,'mg/L.')
                print('Keep it up Rob! Here is how you sugars have been trending.')
                return recordedData()
            else:
                return exercise()
            
        elif ex == yn[1]:
            work = True
            print('Okay you lazy bum... well here is how you sugars have been trending.')
            return recordedData()
        elif ex not in yn:
            return exercise()

def recordedData():

    today = date.today()
    times = datetime.now()
    currentTime = times.strftime("%H:%M")
    data = True
    
    while data:
        with open('FPE/bloodsugardata.txt','a') as add:
            print("\nToday's date:",today,',',currentTime,file=add)
            print('Blood Sugar:',bs,'mg/L',file=add)
            if bs < 180:
                print('Food choice:',pick,file=add)
            else:
                return bloodSugarCarbs()
        
        return bloodSugarCarbs()

#partially from tutorialspoint/rishikesh kumar
def bloodSugarCarbs():
    plt.rcParams["figure.figsize"] = [10.00, 6]
    plt.rcParams["figure.autolayout"] = True

    title = ['Morning Blood Sugar', 'Carbs Morning', 'Night Blood Sugar', 'Carbs Dinner']

    gf = pd.read_csv("FPE/BST.csv", usecols=title)
    gf.plot()    

    plt.xlabel("Days")
    plt.ylabel("Blood Sugar & Carbs Eaten")
    plt.title("Trends in Blood Sugar and Carb Consumption", loc = 'right')

    plt.show()

askQ(bs)
