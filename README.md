# Learning-Management-System

## Introduction
Hi, in this repository I will be explaining you all the tech stack and the requirements to build an awesome app for a Leaning Management System. All you need to do is just keep reading.

### About Learning Management System
Learning management system is an efficient operational software used for a variety of organizational activities. Some of them include administration, documentation, reporting, and creation of training programs. It is a highly adjustable and helpful tool useful for all types of businesses. Some of the famous examples of LMS applications are **Byju's**, **Unacademy**, and **Vedantu**. They have been able to create an impact on the student body of this nation through their brilliant tech stack and the business logic that they use for the growth of their company. 

Some of the basic features of an LMS include:
1. **Student dashboard**
   1. It includes features like User Registration, Log-in, Profile Manager, Courses Section, Payment methods to purchase courses, an Online Reader, Live Chat Support and many more.

2. **Teacher dashboard**
   1. It is a place where every teacher can manage the courses that they are providing, give assignments to the students and their review and grading. 
   2. Teachers can host exams, or short quizzes for the students.
   3. Can take doubt solving or one-to-one sessions.
   4. Can track the attendance of the students.
   5. ...and many more.

3. **Admin panel**
   1. This is the place from where the teacher, or the staff can manage their application backend.
   2. Their functions include, Defining user roles, Creating learning courses, Building custom certification, providing personal feedback for the learners, updating the content being displayed on the application, etc.

4. **Super-admin panel**
   1. This is the panel which has all the permissions in the system. 
   2. Their role includes managing admin roles, adding or removing admin positions, view and run reports, manage sensitive attributes, add and edit authorization server scope, claim, and policies.
   3. ...and the list goes on.

---

### How to make a Learning Management System Software
Enough with the talking, now we will dive deeper into what all do we need to start building an LMS software. 
I'll be listing down each and every step with their details and how they can be implemented.


#### 1. Design Pattern
##### The first thing that we require in the development phase of an LMS app is **Design Pattern**. So what is design pattern?

Design pattern could be defined as a common repeatable solution to recurring problems in software design. It has a **Low Level** scope as compared to a **Software Architecture**(which we will be dealing with later on) when it comes to the project internal code pattern. It is all about how the components of an app are built. 

###### Types of Design Pattern
There are 3 major types of design patterns that help in developing applications so that they have a strong architecture are:
**1.MVVM** (Model-View-ViewModel)
It is useful to move business logic from view to ViewModel and Model. ViewModel is the mediator between View and Model which carry all user events and return back the result. 

**2. MVC** (Model View Controller)
It makes the codebase neat and arranged with three of its components:
- Model:- Model comprises of the data source it may be from anywhere DB, API, JSON, etc. In some cases, it may consist of some business logic.
- View:- View is all about the user interface, i.e displaying data and taking inputs from the user.
- Controller:- It contains the business logic, i.e controlling what data will be shown to the user, user input handling etc. 
Down below here is a flowchart that easily explains the working of MVC.

![MVC Flowchart](https://miro.medium.com/max/875/0*rqVzTnMeBLz340_j.png)

It can be implemented very easily by using the latest version of **MVC Pattern** package under dependencies in `pubspec.yaml` file, and then creating the respective classes and adapting them into the view.

```
dependencies:
  mvc_pattern: ^7.2.0
```


#### 2. Student and Teacher Dashboard
The frontend of a student and teacher dashboard can be very easily made via Flutter with its easy-to-use widgets and its engaging customizable animations.
When it comes to the backend, we will be requiring various libararies and frameworks. 

**1. Django/Firebase/Node.js**
These are some of the backend frameworks which will help in creating the backend of the dashboards. We will be talking about Django here, and how can it be integrated with our app. 
One of the most important powerful parts of Django is the automatic admin interface. Best thing is that it can be customised very easily. It has three options: __superuser__, __staff__, and __admin__. We can create staff using `staff` flag. Any user assigned to this flag can login to the contributed admin app. From there they can control all the data to be showcased in the app.

For example: A teacher has to check the details of her course. So all she needs to do is to go to their application. Login(if signed out) into the teacher dashboard. Go to my courses and click on the particular course tab which she wants to see. This will trigger the backend that has been created in Django. It will be returning some data in JSON format, such as **number of students**, **total recorded lectures**, **calendar for the upcoming classes**, etc. which will get parsed in the `util` folder of the code and return data that can be displayed in widgets.

###### Integrating Django with Flutter

First we will set up a Django project
```python
python manage.py startapp search
```
Then we will create a model, which will basically translate to a SQL database behind the scenes.

```python
from django.db import models

class Cayegory(models.Model):
  name = models.CharField(max_length=50)
  
  def __str__(self):
    return self.name
class Course(models.model):
//required code
```

From here on we will add the functionality of the backend. Then we will write the functioning in the Flutter code. 

```Dart
import 'package:http/http.dart' as http;

class SearchService{
  static Future<String> searchDjangoApi(String query) async{
    String url = '//url of api';
    
    http.Response response = await http.get(Uri.encodeFull(url));
    
    return response.body;
  }
}
```



