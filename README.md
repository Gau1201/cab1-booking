# cab1-booking
from tkinter import *
import sqlite3
import tkinter.messagebox
 
conn = sqlite3.connect('carbooking.db')
c = conn.cursor()
 
 
ids = []
 
 
class Application:
def __init__(self, windows):
self.windows = windows
 
self.left = Frame(windows, width=800, height=720, bg='navajo white')
self.left.pack(side=LEFT)
 
self.right = Frame(windows, width=600, height=720, bg='navajo white')
self.right.pack(side=RIGHT)
 
self.title = Label(self.left, text="Car Booking", font=(
'georgia 40 bold'), fg='black', bg='navajo white')
self.title.place(x=0, y=0)
self.n = Label(self.left, text="Owner's Name", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.n.place(x=0, y=100)
 
 
self.a = Label(self.left, text="Age", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.a.place(x=0, y=140)
 
 
self.gen = Label(self.left, text="Gender", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.gen.place(x=0, y=180)
 
self.loc = Label(self.left, text="Location", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.loc.place(x=0, y=220)
 
self.t = Label(self.left, text="Entry Time", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.t.place(x=0, y=260)
 
 
self.phoneNumber = Label(self.left, text="Phone Number", font=(
'georgia 18 bold'), fg='black', bg='navajo white')
self.phoneNumber.place(x=0, y=300)
 
self.nametextentry = Entry(self.left, width=30)
self.nametextentry.place(x=250, y=100)
 
self.agetextentry = Entry(self.left, width=30)
self.agetextentry.place(x=250, y=140)
 
self.gendertextentry = Entry(self.left, width=30)
self.gendertextentry.place(x=250, y=180)
 
self.locationtextentry = Entry(self.left, width=30)
self.locationtextentry.place(x=250, y=220)
 
self.timetextentry = Entry(self.left, width=30)
self.timetextentry.place(x=250, y=260)
 
self.phonetextentry = Entry(self.left, width=30)
self.phonetextentry.place(x=250, y=300)
 
self.submit = Button(self.left, text="Add Booking", width=20,
height=2, bg='white', command=self.add_appointment)
self.submit.place(x=300, y=340)
 
 
sql2 = "SELECT ID FROM appointments "
self.result = c.execute(sql2)
for self.row in self.result:
self.id = self.row[0]
ids.append(self.id)
 
 
self.new = sorted(ids)
self.final_id = self.new[len(ids)-1]
 
self.logs = Label(self.right, text="Booking logs", font=(
'georgia 28 bold'), fg='black', bg='navajo white')
self.logs.place(x=70, y=10)
 
self.box = Text(self.right, width=150, height=40)
self.box.place(x=20, y=60)
self.box.insert(END, "Total Bookings till now : " +
str(self.final_id) + " \n")
 
def add_appointment(self):
self.value_1 = self.nametextentry.get()
self.value_2 = self.agetextentry.get()
self.value_3 = self.gendertextentry.get()
self.value4 = self.locationtextentry.get()
self.value5 = self.timetextentry.get()
self.value6 = self.phonetextentry.get()
 
if self.value_1 == '' or self.value_2 == '' or self.value_3 == '' or self.value4 == '' or self.value5 == '':
tkinter.messagebox.showinfo("Warning", "Please Fill Up All Boxes")
else:
sql = "INSERT INTO 'appointments' (name, age, gender, location, scheduled_time, phone) VALUES(?, ?, ?, ?, ?, ?)"
c.execute(sql, (self.value_1, self.value_2, self.value_3,
self.value4, self.value5, self.value6))
conn.commit()
tkinter.messagebox.showinfo(
"Success", "Booking for " + str(self.value_1) + " has been created")
self.box.insert(END, 'Booking fixed for ' +
str(self.value_1) + ' at ' + str(self.value5))
 
 
 
root = Tk()
b = Application(root)
 
root.geometry("1366x768")
 
root.resizable(False, False)
 
root.mainloop()
