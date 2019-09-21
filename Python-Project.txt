import random

#Python Game for Guessing Single Word Oscar Winning Movies....

def attempts():
   while True :
      num_attempts = int(input('\nInput Number of attempts (4 - 10):'))
      if 4 <= num_attempts <= 10 :
        return num_attempts
      elif 4 > num_attempts > 10 :
        print(f'{num_attempts} is not between 4 - 10.')
      else  :
        print('Please input according to the instruction.')
        
        
def min_word_length():
    while True :
         word_length = int(input('Minimum length of word you want (4-10):'))         
         if 4 <= word_length <= 10 :
             return word_length
         elif word_length < 4 :
             print('Minimum word length is shorter than 4 characters')
         elif word_length > 10 :
             print('Word length should be less than 10 characters')
         else :
             print('Please input according to the instruction.')


def get_next_letter(repeat):
         con = True
         while con :         
          next_letter = input('Choose the letter: ')
          if len(next_letter) != 1:             
            print('{0} is not a single character'.format(next_letter)) 
          elif  ord(next_letter) >= 65 and ord(next_letter)<=90 :             
            print('Please input in small alphabet.')         
          elif next_letter in repeat:             
            print('{0} has been guessed before'.format(next_letter))
          else :
              con = False
         return next_letter           

def finding_word(word,guess,new) :
    newl = []
    for i in word : 
        if i == guess :   
           index = word.find(guess)
           newl.append(index)
           word = word.replace(guess,' ',1)
    xyz = replacing(newl,guess,new)
    return xyz

def replacing(newl,guess,new):
    for i in newl:
         new[i] = guess
    xyz = ""
    xyz = "".join(new)
    return xyz    
      
 
    
def try_again() :      
     try_again = input('\nWould you like to try again? [y/Y] ')  
     if try_again.lower() == 'y' :
        play_hangman()
     else :
        print('Thankyou for playing')  
        
def get_word() :
    movies = ['Gravity','Lincoln','Hugo','Inception','Up','Avatar','Titanic','Braveheart','Chicago','Unforgiven','Argo','Gandhi','Rocky','Gladiator','Birdman','Amadeus']
    z = min_word_length()
    while True :
       x = random.choice(movies)
       if len(x) != z :
           continue
       else :
           return x.lower()         
 

def play_hangman():
    
    attempts_remaining = attempts()
    #min_word_len = min_word_length()
    guess = 'None'
    condition = True    
    repeat = []
    
    print('Selecting a word...')
    word = get_word()  #get_random_word()
    
    wrd = ''
    r_word = word
    
    length = len(word)
    b = '*' * length    
    new = list(b)
    wrd = b

# Main starting here..............->->->->
    while condition :
     print(f'\n----xxxx----xxxx----xxxx--\nPrevious Guess : {guess}') 
     print(f'Attempts remaining : {attempts_remaining}')
     guess = get_next_letter(repeat)
     repeat.append(guess)
     
     for i in word : 
        if i == guess :
            con = True
            break
     else :    
            con = False 
            
     if con == True :    
         wrd = finding_word(word,guess,new)  
     elif con == False :
         attempts_remaining = attempts_remaining -  1

     print(f'Word : {wrd}')         
     print(f'Attempts remaining : {attempts_remaining}')
     
     if wrd == r_word :  
           print('\n\n-----Congrats! you won.-----')
           break
     elif attempts_remaining == 0 :
        condition = False
        print('Game Over')
        print(f'The Word is : {word}')
                 
    try_again() 
           
           

if __name__ == '__main__':
     play_hangman()
           
 

