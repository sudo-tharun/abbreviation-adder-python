# abbreviation-adder
This is program to add the short forms with their abbreviations to a notepad file. Further extension can be writing to a word file.

import os

    
def duplicate(d,sf1):
    temp=[]
    index=0
    m=0
    with open(d , "r") as t:
        for i in t:
            temp.append(i)
        for m in temp:
            print("The first word:" + m[0])
            #index=index+1
    t.close()
    return

def selectfromexisting(shortform,listoffullform):
    arr=os.listdir('.')
    l=(list(enumerate(arr)))
    for i in l:
        string=str(i)[1:-1]
        string = string[:1] + ":" + string[1+1:]
        print(string)
    print("Does the file exitsts here in the above list? ")
    a=input("1. Yes     2. No")
    if a == "1":
        index=int(input("Enter the index of file: "))
        l=(list(enumerate(arr)))
        filename=arr[index]
        print(filename)
        return filename
    else:
        findingfile(shortform,listoffullform)

def abbreviate():
    word=input("Enter the short-form: (Ex: ABC or abc) ")
    word=word.upper()
    print(word)
    m=list()
    for i in word:
        a=input("Give the fullform of " + i + " in " + word +": ")
        m.append(a.capitalize())
    findingfile(word,m)

def writetofile(name,sf2,l):
        filename=name
        duplicate(filename,sf2)
        f=open(filename,"a")
        f.write("\n")
        f.write(sf2 + ": ")
        for k in l:
            f.write(k + " ")
        f.close()

        f=open(filename, "r")
        print(f.read())
        f.close()

        print("Do you wish to write more? ")
        choice=input("Yes(y) or No(n) ")
        choice=choice.lower()
        if choice == "y" or choice == "yes":
            abbreviate()
        else:
            return

def findingfile(sf,l):
    file=input("Enter the name of the file (case sensitive): ")
    filename=file + ".txt"
    try:
        f=open(filename)
    except FileNotFoundError:
        print("\n File not found!! Kindly check the name!")
        print("Not remembering the name? ")
        c=input("Select your choice: \n 1. View all files in directory  \n 2. Create new file  ")
        if c == "1":
            filefromdir=selectfromexisting(sf,l)
            writetofile(filefromdir,sf,l)
        if c == "2":
            f=open(filename, "x")
            f.close()
            writetofile(filename,sf,l)

abbreviate()
