import tkinter
import random
from tkinter import*

questions = [
    "Q.India won the first cricket world cup in the year?",
    "Q.India got independence in the year?",
    "Q.The English company ruled India for how many years?",
    "Q.Who is the captian of Indian football team?",
    "Q.Who was the first president of India?",
    "Q.The phrase 'Inquilab Zindabad' was given by whom?",
    "Q.The revolution known as 'Dandi March' was started by whom?",
    "Q.Who was the leader of 'Muslim league' in 1947?",
    "Q.According to ICC ranking list 2020 who is the best batsmen?",
    "Q.According to ICC ranking list 2020 who is the best bowler?",
]

answer_choice = [
    ["A.1963","B.1983","C.1975","D.1987"],
    ["A.1950","B.1947","C.1944","D.1952"],
    ["A.10","B.200","C.190","D.150"],
    ["A.Sunil Chetri","B.Manvir Singh","C.Pronay Halder","D.SarthakGoloui"],
    ["A.Rajendra Prasad","B.Jawahar Lal Nehru","C.Sardar VallabhBhai Patel","D.Mahatma Gandhi"],
    ["A.Shivaram Rajguru","B.Sukhdev Thappar","C.Maulana Hasrat Mohani","D.Bhagat Singh"],
    ["A.Jawahar Lal Nehru","B.bal Gangadhar Tilak","C.Nathuram Godse","D.Mahatma Gandhi"],
    ["A.Khwaja Nazimuddin","B.Nawab Waqar-ul-Mulk","C.Nawab Khwaja Salimullah","D.Muhammad Ali Jinnah"],
    ["A.Steve smith","B.Virat Kholi","C.Rohit sharma","D.Babar Azam"],
    ["A.jasprit Bumrah","B.Trent Boult","C.Mujeeb Ur Rahman","D.Chris woakes"],
]

answers= [1,1,2,0,0,2,3,3,1,1]

user_answer = []

indexes = []


def showresult(score):
    lblQuestion.destroy()
    r1.destroy()
    r2.destroy()
    r3.destroy()
    r4.destroy()

    labelimage = Label(
        root,
        background = "#ffffff",
        border = 0,
    )
    labelimage.pack(pady=(100,100))

    lableresulttext = Label(
        root,
        font = ("Consolas",50),
        background = "#ffffff"
    )
    lableresulttext.pack()
    if score >= 35:
        img = PhotoImage(file = "excellent work.png")
        labelimage.configure(image=img)
        labelimage.image = img
        lableresulttext.config(text = "You Are Excellent!!")

    elif score >= 20 and score < 35:
        img = PhotoImage(file = "pretty_good.png")
        labelimage.configure(image = img)
        labelimage.image = img
        lableresulttext.config(text = "You can do better!!")

    else:
        img = PhotoImage(file = "bad.png")
        labelimage.configure(image = img)
        labelimage.image = img
        lableresulttext.configure(text = "You are awfull")
def gen():
    global indexes
    while(len(indexes) < 9):
        x = random.randint(0,9)
        if x in indexes:
            continue
        else:
            indexes.append(x)
    print(indexes)

def calc():
    global indexes,user_answer,answers
    x = 0
    score = 0
    for i in indexes:
        if user_answer[x] == answers[i]:
            score = score + 5
        x += 1
    print(score)
    showresult(score)

ques = 1

def selected():
    global lblQuestion,r1,r2,r3,r4
    global radiovar,user_answer
    global ques
    x = radiovar.get()
    user_answer.append(x)
    radiovar.set(-1)
    if ques < 10:
        lblQuestion.config(text= questions[indexes[ques]])
        r1['text'] = answer_choice[indexes[ques]][0]
        r2['text'] = answer_choice[indexes[ques]][1]
        r3['text'] = answer_choice[indexes[ques]][2]
        r4['text'] = answer_choice[indexes[ques]][3]
        ques += 1

    else:
        print(indexes)
        print(user_answer)
        calc()
    


def startquiz():
    global lblQuestion,r1,r2,r3,r4
    
    lblQuestion = Label(
        root,
        text = questions[indexes[0]],
        font = ("Consolas",30,"bold"),
        width = 500,
        background = "red",
    
    )
    lblQuestion.pack(pady=(100,30))

    global radiovar
    radiovar = IntVar()
    radiovar.set(-1)

    r1 = Radiobutton(
        root,
        text = answer_choice[indexes[0]][0],
        font = ("Times",20),
        value = 0,
        command = selected,
        background = "#ffffff",
        variable = radiovar,
    )
    r1.pack(pady=5)

    r2 = Radiobutton(
        root,
        text = answer_choice[indexes[0]][1],
        font = ("Times",20),
        background = "#ffffff",
        value = 1,
        command = selected,
        variable = radiovar,
    )
    r2.pack(pady=5)

    r3 = Radiobutton(
        root,
        text = answer_choice[indexes[0]][2],
        font = ("Times",20),
        value = 2,
        command = selected,
        background = "#ffffff",
        variable = radiovar,
    )
    r3.pack(pady=5)

    r4 = Radiobutton(
        root,
        text = answer_choice[indexes[0]][3],
        font = ("Times",20),
        value = 3,
        command = selected,
        background = "#ffffff",
        variable = radiovar,
    )
    r4.pack(pady=5)

def startIspressed():
    labelInstruction.destroy()
    labelRules.destroy()
    labelimage.destroy()
    labeltext.destroy()
    gen()
    btnstart.destroy()
    startquiz()

root = tkinter.Tk()
root.title("Quizmaster")
root.geometry("1540x850+0+0")
root.config(background="#ffffff")
root.resizable(0,0)

bg_icon = PhotoImage(file = "quiz.png")
img1 = PhotoImage(file = "Gradhat.png")

labelimage = Label(
    root,
    image = img1,
    background = "#ffffff",
)
labelimage.pack(pady=(40,0))

labeltext = Label(
    root,
    text = "Quizmaster",
    font = ("Comic sans MS",40,"bold"),
    background="#ffffff",
)
labeltext.pack(pady=(0,50))

labelInstruction = Label(
    root,
    text = "Read The Rules And\nClick Start Once You Are Ready!",
    background = "#ffffff",
    font = ("consolas",14), 
)
labelInstruction.pack(pady=(10,90))

labelRules = Label(
    root,
    text = "This quiz contains 10 questions\nYou will get 5 minutes to solve this quiz\nOnce you select a radio button that will be final choice\nHence think before you select",
    width = 100,
    background = "#000000",
    font = ("Times",24),
    foreground = "#FACA2F"
)
labelRules.pack(pady=(90,90))

btnstart = Button(
    root,
    text = "Start",
    width = 15,
    command = startIspressed,
    font = ("Times new roman",14,"bold"),
    background = "red",
    foreground = "white",
)
btnstart.pack(padx=(1000,0))
root.mainloop()