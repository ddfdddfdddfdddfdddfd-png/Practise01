So u rememeber the game where u place the pieces of different sizes to fit the board?
despite having no interest in making the game,
As an exercise I figured out a (clean) way to detect whether each space is taken.
LLMs can probably do this in a much better way... BUT...
it is a way...

So, below is howbI would detect whether a space is free and to store the info that a space is occupied
this does not include how to detect which space the player chose (not due to laziness)

I will use a 5x5 grid as the board and biggest piece 4x4 as an example of how to do it, I'll say what to do with bigger dimensions later (if I remember)


I assume that u can check which piece the player picked and what coordinate to put it
The coordinate to player picked correspondent to to lefttop conner of a peice, and should store the info into the x and y variables, so:
x = player_chosen_column
    y = player_chosen_row

each piece is a function, it is ran when player do the placement, and check availability for that specific piece, and it puts down the piece if available



My method checks the avalibility of the squars column by column, below is what to do with the first (leftmost) colume, I'll mention how to check all the necessary condoms at the later
# For each colume
the leftmost colume is called c1, the one to right of c1 is c2 etc

imagine a column 4 squares tall, squars have values (top down) 1,2,4,8 respectively
only one information for each column of each piece is needed —  its value
this is counted from the top left conner of a peice(can be empty), which tells the code where the player choose to put the piece
eg if c1 of a piece occupies squares 1 and 3 (from The top), c1 of the piece has a value of 1+4=5, 
another eg: if c2 (second colume) of a piece occupies squares 2,3 and 4,c2 of that piece has a value of 2+4+8 = 14, 
this is put in the function of the piece manually

to check wether the squares are occupied:
use thw piese in figure 1 as an example — 
c1 has a value of 6, 
c2 has a value of 3, 
c3 has a value of 0, 
c4 has a value of 0, 

def piece1():
    Global all the variables

    fine = False #A flag that goes true if the placement is possible
    
    value = 6
    
    check()  #a function that checks the ability of the colume

    x += 1 #check the next cloumn
    value = 3
    
    check()

    x += 1 #check the next cloumn
    value = 0
    
    check()

    x += 1 #check the next cloumn
    value = 0
    
    check()
    
    if fine = True:  #if it servived The checks
        peice_one = True #it is placed down, disallow player to pick a piece if its true or sm


so obviously check() is important, i'm doing it a smart way😈
first thing i do is to slove the issue that pieces are not always placed at the top row
using a variable called code

def check():
    Global all the variables
    code = 2^(y-1)*value
#for eample using figuer one c1, if y=3(player places top left conner on the third row):
#code would be 2^(3-1)*6= 4*6 = 24 ( =8+16 if you are wondering why this works)
#now we unpack the code into another variable called size

    size = 1
    if code >= 16:   #if the piece uses the bottom square:  
        size *= 2     # 2 is occupied , more on this later
        code -= 16    #allows next check
    
    if code >= 8:   #if the piece uses the second bottom square:  
        size *= 3     # 3 is occupied , more on this later
        code -= 8    #allows next check
    
    if code >= 4:   #if the piece uses the middle square:  
        size *= 5     # 5 is occupied , more on this later
        code -= 4    #allows next check
    
    if code >= 2:   #if the piece uses the 2nd from top square:  
        size *= 7     # 7 is occupied , more on this later
        code -= 2    #allows next check
    
    if code >= 1:   #if the piece uses the top square:  
        size *= 11     # 11 is occupied , more on this later
        code -= 1    #allows next check
    
    if code > 0:  #if it is out of The board
        return    #failed check

#now compare size to the desired cloume
    if x = 1:   #which clomn the player picked
        col = col1   #col1 is a variable for the left column, defult 1 at start of game when empty
    if x = 2:
        col = col2
.
.
.
#(repeat for x = 3 4 and 5)

#finally, to check whether it is free, I will explain why this work later:
    rs = col*size #multiply col and size for check

    while rs > 0: #check devisibility by 4
        rs -= 4  
    if rs = 0:    #if it is divisible, the bottom square is already occupied, and would cause overlap
        return #so failed check

    rs = col*size #multiply col and size for check

    while rs > 0: #check devisibility by 9
        rs -= 9  
    if rs = 0:    #if it is divisible, the seound bottom square is already occupied, and would cause overlap
        return #so failed check

    rs = col*size #multiply col and size for check

    while rs > 0: #check devisibility by 25
        rs -= 25  
    if rs = 0:    #if it is divisible, the middle square is already occupied, and would cause overlap
        return #so failed check

    rs = col*size #multiply col and size for check

    while rs > 0: #check devisibility by 49
        rs -= 49
    if rs = 0:    #if it is divisible, the secoumd square is already occupied, and would cause overlap
        return #so failed check

    rs = col*size #multiply col and size for check

    while rs > 0: #check devisibility by 121
        rs -= 121
    if rs = 0:    #if it is divisible, the top square is already occupied, and would cause overlap
        return #so failed check

    fine = True #survived check🥳

    if x = 1:
        col1 *= size   # place it on
    if x = 2:
        col2 *= size    #place it on
.
.
.
#repeat for 345

DONE!

why this work is, using 121 as an example, rs is divisible by 121 if and only if 11 is in both col and size, 
this happens if and only if top square is not free + piece takes top square, so failed test

when you place a piece down you multiply the size to the col, so which square is used is stored
The piece function allows check for the next column due to x += 1, 

all you need to make is the value in the function of the indiviual pieces, so it should be pretty easy





































duck































goes

























go












































🦆