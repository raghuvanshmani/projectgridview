# projectgridview
from tkinter import *
import pymongo
from  tkinter import colorchooser
from tkinter import filedialog
import json
import pandas as pd
import geojson
from  tkinter import messagebox
import re
import prettytable
root =Tk()
n = StringVar()
a= StringVar()
q=StringVar()
nu=IntVar()
g=StringVar()
d1= StringVar()
d2=StringVar()
u1=StringVar()
u2=StringVar()
crt1=StringVar()
crt2=StringVar()
em = StringVar()

def create():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    data = {"age":23}
    collection.insert_one(data)
def insert():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    p=em.get()
    m=re.search('\w+@\w+\.com',p)
    if m:
        messagebox.showinfo("all the data save succesfully")
        data = [
            {"name": n.get()},
            {"address": a.get()},
            {"qualification": q.get()},
            {"number": nu.get()},
            {"email": em.get()},
            {"gender": g.get()}

        ]
        collection.insert_many(data)

    else:
        messagebox.showinfo("the email address is not proper formate")






def fetch():
    la=" "
    top=Toplevel()
    top.geometry('600x600')
    top.title("fetch the data")

    #text=Text(top,font=10)
    #text.pack(fill=BOTH,expand=1)
    var = StringVar()




    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    y=prettytable.PrettyTable()
    y.field_names=["name","city"]
    y.add_row(["Raghu","Noiad"])
    print(y)
    #inventory_data = [data for data in collection.inventory.find()]
    #df_inventory_data = pd.DataFrame(inventory_data)
    #print(df_inventory_data)

    x = collection.find()
    '''for i in x:
        text.insert(INSERT,i)'''






    for j in x:
        for k in j:
            la += str(j[k])


        la += str("\n")

    data = Label(top, text=la, bg="#effffb", font=20, bd=4)
    data.grid(row=3, column=3)





    ''' for k,v in j.items():
         print()
         y.add_row([k,v])
         text.insert(INSERT,(k,v))'''














def dele():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    my={d1.get():d2.get()}
    mydoc = collection.delete_one(my)

def updat():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    oldquery= {d1.get():d2.get()}
    newquery={"$set":{u1.get():u2.get()}}
    collection.update_one(oldquery,newquery)
def drop_c():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['Student']
    collection.drop()
def openfolder():
      f =filedialog.askopenfile()

#create reset button
def Res():
    n.set("")
    a.set(" ")
    q.set(" ")
    nu.set(" ")
    g.set(" ")
    d1.set(" ")
    d2.set(" ")
    u1.set(" ")
    u2.set(" ")
    crt1.set(" ")
    crt2.set(" ")
    em.set(" ")
def form():
    global use,pas
    use = StringVar()
    pas=StringVar()
   # messagebox.showinfo("this is the loginform")
    def log():
        if use.get()=="" or pas.get() =="":
            messagebox.showinfo("all feild are required")
        elif use.get()==n.get():
            messagebox.showinfo("login successfull")
        else:
            messagebox.showinfo("invalid credential")











    win1 = Toplevel()
    win1.title("Login from")
    title = Label(win1, text="Loginpage", bg="#effffb", font=20, bd=4)
    title.grid(row=0, column=0 )
    user = Label(win1, text="username", bg="#effffb", font=20, bd=4)
    user.grid(row=3, column=3)
    usere1 = Entry(win1, font=10, bg="white", textvariable=use)
    usere1.grid(row=3, column=4)
    passw = Label(win1, text="password", bg="#effffb", font=20, bd=4)
    passw.grid(row=4, column=3)
    passwe = Entry(win1, font=10, bg="white", textvariable=pas)
    passwe.grid(row=4, column=4)
    lo = Button(win1, text="login", font=10, activebackground="yellow", command=log)
    lo.grid(row=5, column=4)


    win1.geometry('600x600')







name = Label(root ,text="Name",bg="#effffb",font = 20,bd=4)
name.grid(row = 0,column= 0,)
namee=Entry(root,font=10,bg="white",textvariable=n)
namee.grid(row=0,column=3)


#address of the person
addr = Label(root ,text="Address",bg="#effffb",font = 20,bd=4)
addr.grid(row = 1,column= 0)
addre = Entry(root,font=20,bg="white",textvariable=a)
addre.grid(row=1,column=3)



#qualification
quali = Label(root ,text="Qualification",bg="#effffb",font = 20,bd=4)
quali.grid(row = 2,column= 0)
qualie = Entry(root,font=20,bg="white",textvariable=q)
qualie.grid(row=2,column=3)




#number of the person
number = Label(root ,text="Mobile Number",bg="#effffb",font = 20,bd=4)
number.grid(row = 3,column= 0)
numbere = Entry(root,font=20,bg="white",textvariable=nu)
numbere.grid(row=3,column=3)

#email of the student
email = Label(root ,text="Email ID",bg="#effffb",font = 20,bd=4)
email.grid(row = 4,column= 0)
emaile = Entry(root,font=20,bg="white",textvariable=em)
emaile.grid(row=4,column=3)



#gender of the person
gender = Label(root ,text="Gender",bg="#effffb",font = 20,bd=4)
gender.grid(row = 5,column= 0)
gendere = Entry(root,font=20,bg="white",textvariable=g)
gendere.grid(row=5,column=3)




#insert button
ins = Button(root,text="save",font=10,activebackground="yellow",
activeforeground="red",command=insert)
ins.grid(row=6,column=0)


#create the database
cr = Button(root,text="create",font=10,activebackground="yellow",
activeforeground="red",command=create)
cr.grid(row=8,column=0)
#create reset button
cr = Button(root,text="Reset",font=10,activebackground="yellow",
activeforeground="red",command=Res)
cr.grid(row=6,column=3)
cr = Button(root,text="LoginForm",font=10,activebackground="yellow",
activeforeground="red",command=form)
cr.grid(row=6,column=5)





#delete the cllection
de= Button(root,text="delete",font=10,activebackground="yellow",command=dele)
de.grid(row=10,column=0)
de1= Entry(root,font=10,textvariable=d1)
de1.grid(row=10,column=3)
de2= Entry(root,font=10,textvariable=d2)
de2.grid(row=11,column=3)
ke1 = Label(root ,text="key",bg="#effffb",font = 20,bd=4)
ke1.grid(row = 10,column= 4)
ke2 = Label(root ,text="value",bg="#effffb",font = 20,bd=4)
ke2.grid(row = 11,column= 4)


#fetch the data
fet = Button(root,text="fetch",font=10,activebackground="yellow",
activeforeground="red",command=fetch)
fet.grid(row=7,column=0)

root.title("Ragitrationform")


#update the collection
upd = Button(root,text="update",font=10,activebackground="yellow",
activeforeground="red",command=updat)
upd.grid(row=12,column=0)
upe = Entry(root,font=20,bg="white",textvariable=u1)
upe.grid(row=12,column=3)
upe1 = Entry(root,font=20,bg="white",textvariable=u2)
upe1.grid(row=13,column=3)
ke1 = Label(root ,text="ukey",bg="#effffb",font = 20,bd=4)
ke1.grid(row = 12,column= 4)
ke2 = Label(root ,text="uvalue",bg="#effffb",font = 20,bd=4)
ke2.grid(row = 13,column= 4)


#drop the collection
drp = Button(root,text="dropcollection",font=10,activebackground="yellow",
activeforeground="red",command=drop_c)
drp.grid(row=14,column=0)





#upload the image
img = Button(root,text="uploadimage",font=10,activebackground="yellow",
activeforeground="red",command=openfolder)
img.grid(row=15,column=3)

root.geometry('600x600')
root.mainloop()
