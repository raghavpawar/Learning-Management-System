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


#### 2. Student and Teacher Dashboard(Frontend and Backend)
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

class Category(models.Model):
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

**2. Jitsi as a Service(JaaS)**(For an inbuilt video conferencing system)
Jitsi as a Service enables you to develop and integrate Jitsi Meetings functionailty into our applications. So we can host meetings that leverage the distributed Meetings infrastructure from datacenters around the world. 
To use Jitsi Meet in our Flutter apps, we need to use the **jitsi_meet** package. [Package reference](https://pub.dev/packages/jitsi_meet#:~:text=Jitsi%20Meet%20Plugin%20for%20Flutter,secure%20and%20scalable%20video%20conferences.%22). To install it, we can run this command:
```
$ flutter pub add jitsi_meet
```
or we can implicitly add it to our dependencies in our `pubspec.yaml` file

```
dependencies:
   jitsi_meet: ^4.0.0
```
and run `flutter pub get`.

After this we need to configure it for our Android and our iOs codebase. This plugin has various features that we can use for our conferences. 

##### To join a meeting
We have to provide a function that will look like this:

```
_joinMeeting() async {
    try {
	  FeatureFlag featureFlag = FeatureFlag();
	  featureFlag.welcomePageEnabled = false;
	  featureFlag.resolution = FeatureFlagVideoResolution.MD_RESOLUTION; // Limit video resolution to 360p
	  
      var options = JitsiMeetingOptions()
        ..room = "myroom" // Required, spaces will be trimmed
        ..serverURL = "https://someHost.com"
        ..subject = "Meeting with Gunschu"
        ..userDisplayName = "My Name"
        ..userEmail = "myemail@email.com"
        ..userAvatarURL = "https://someimageurl.com/image.jpg" // or .png
        ..audioOnly = true
        ..audioMuted = true
        ..videoMuted = true
        ..featureFlag = featureFlag;

      await JitsiMeet.joinMeeting(options);
    } catch (error) {
      debugPrint("error: $error");
    }
  }
```
Adding this will get us started to enable video conferencing feature in our Flutter apps.


**3.WBO**(For adding whiteboard functionality while having a video conference)
[Link to github repo](https://github.com/lovasoa/whitebophir)
This is a java script code that can be integrated in our flutter apps along with the **jitsi_meet** plugin. It is an online collaborative whiteboard that allows many users to draw simultaneously on a large virtual board.


**4. Google APIs**(For assignment reviews and submissions)
Google provides a list of APIs which can be used in our apps to integrate its services for better user flow and control. To provide assignments to the students, we can use the **Google Classroom API** which has three types of Classwork: Assignments, Questions and Materials. 
To access this, we can use the CourseWork resource, which has various fileds such as `courseId`, `title`, `description`, `maxPoints`, `assignment` and so on. [CourseWork resource](https://developers.google.com/classroom/reference/rest/v1/courses.courseWork).

For using it with out flutter apps, we also have an option to use the `googleapis` package which auto generates Dart libraries for accessing Google APIs. [Link to the package](https://pub.dev/packages/googleapis).


**5. Razorpay plugins**(For fee payment systems)
Razorpay is a payment gateway which is used by E-Commerce companies or websites to charge the customer for their product and services and they can collect online payment via netbanking, wallets, debit or credit cards and UPI. 
To use razorpay feature in our Flutter app, we can use the **rasorpay_flutter** plugin. To install it run command:
```
 $ flutter pub add razorpay_flutter
```
or add a line to the package's pubspec.yaml file:
```
dependencies:
  razorpay_flutter: ^1.2.5
```
and run `flutter pub get`.
Then all we need to do is create razorpay instances, attach event listeners, some handles and boom. A payment system is also integrated in our Flutter app. 
[Link to the package](https://pub.dev/packages/razorpay_flutter)


**5. D3.js library/syncfusion_flutter_charts package/google gallery for charts/plotly_js package**(For detailed reports)
These are some libraries and packages that we can use in our project to showcase detailed reports and statistics of our students and their engagement in the courses, monthly performance, etc.
D3.js is one of the most famous library for plotting beautiful charts, graphs and statistical reports. We can easily use it in our flutter app by creating a js file which contains all the code required for plotting the graphs and then using this line of code.

```
import 'dart:js' as js;

js.context['d3'].callMethod('select', [shadowRoot.querySelector('.chart')]);
```
This will invoke the d3 code after some tweaks in our widget's code and finally displaying beautiful graphs for our student's monthly performance. 


**6. Google Cloud/AWS libraries**(For database storage and cloud computing)
We need either of these two serices to manage the database of our students, when they are in a very large amount. These two services are very easy to use and with the services they provide, we can do everything that we want for our database. These are some of the code snippets that might come handy while integrating AWS with flutter(after we have set up an AWS account and created a database in it).

For creating a serverless project
```
serverless create --template aws-nodejs
```

```
functions:

  getAllFiles:
    handler: handler.getAllFiles
    events:
     - http:
         path: /getAllFiles
         method: get       

  uploadFile:
    handler: handler.uploadFile
    events:
     - http:
         path: /uploadFile
         method: post
```
Logic for getting all Files, from AWS storage:

```
module.exports.getAllFiles = async (event, context) => {

  let files = [];

  let params = {
    Bucket: process.env.BUCKET, /* required */
    Prefix: 'upload'
  };

  let result = await s3.listObjectsV2(params).promise();

  let data = result.Contents;
  Object.keys(data).forEach((key, index) => {

    let fileObject = data[key];

    files.push(`https://${result.Name}.s3.us-east-2.amazonaws.com/${fileObject.Key}`);
  });


  return {
    statusCode: 200,
    body: JSON.stringify({
      files: files,
      bucketName: `${result.Name}`,
      subFolder: `${result.Prefix}`,
    }, null, 2),
  };
};
```
Logic for uploading files to bucket:

```
module.exports.uploadFile = async (event, context) => {

  let request = event.body;
  let jsonData = JSON.parse(request);
  let base64String = jsonData.base64String;
  let buffer = Buffer.from(base64String, 'base64');
  let fileMime = fileType(buffer);

  if (fileMime == null) {
    return context.fail('The string supplied is not a file type.');
  }

  let file = getFile(fileMime, buffer); 
//Extract file info in getFile
```

```
 let params = file.params;

  let result = await s3.putObject(params).promise();

  return {
    statusCode: 200,
    body: JSON.stringify({
      url: `${file.uploadFile.full_path}`,
    }, null, 2),
  };
};
```


### Implementation of this tech stack in a Learning Management System?
If you have reached till here, then my friend, you have learned about most of the tech stacks that are required for building a user friendly Learning Management System Application. The implementation flow of these technologies and frameworks will be as follows:

1. UI development via flutter
2. Integrating Django framework and the AWS framework with the App
3. Adding services such as Jitsi Meet, Whiteboard, Razorpay, D3 libraries
4. Testing of the app along with development.



##### Thank You!










