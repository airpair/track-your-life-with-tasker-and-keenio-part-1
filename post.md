When I was a kid I was used to count everything around me. Actually I am still having such habit. :)

Everywhere I go I count objects around me. No particular reason for it, just that I get bored very quickly and counting things keep me busy with something to do. :)

I always been interested in numbers, statistics and analytics. Over the time I have also developed some simple web app helping me to track important parameters for me.

Recently I have stumbled upon a fantastic service called [keen.io](https://keen.io/ "keen.io")  and I have decided to build a simple app to keep track of my life events and parameters.

In this post I'll explain you what I have done and I'll share the app with you so you can take it and improve it in case you find it useful.

### Tools

The tools I have used for my tracking application are:
* keen.io: a very good data collection and analytics service in the cloud
* Tasker: the best app for Android which I have ever purchased

### Keen.io
Keen.io allows me to send event data to the cloud via a well designed REST API. 
Store such data in the cloud and create beautiful analytics dashboards. 

They have a free of charge plan for up to 50.000 event/month, clear and well written documentation, SDK for the major languages (JS, Ruby, Python, iOS, Android, Java, .Net and even Scala).

In short they provide everything I always been looking for to implement a simple and extensible tracking application.

For additional information I suggest you to look into the [documentation](https://keen.io/docs/ "documentation")

### Tasker
Tasker is defined as "Total Automation for Android" by its author.
This is totally true and I would add that Tasker is the factotum for Android. Whatever you have in mind can be more or less easily achieved with tasker and its plug-ins.

With Tasker [App Factory](http://tasker.dinglisch.net/userguide/en/appcreation.html "App Factory") you can even build native Android application that you can even distribute through the Play store.

For additional information I suggest you to look into the [user guide](http://tasker.dinglisch.net/userguide/en/ "user guide")

### TrackMe app
Nowadays you can find in the market many cool devices and apps that helps you to track different aspects of your life. There are tons of fitness bracelets, activity trackers, sleep trackers, whatever trackers. 

However those cool devices are all independent form each other. They all provide a separate app and analytic tool.

The only "smart" device which is always with you from morning to end of the day is your phone.

So why not using it as one single tracker device? 
With your smart phone you can track your fitness activities, your sleep etc...

This is exactly what TrackMe app is doing.


### Tasks and Scenes
Using Tasker tasks and scenes I have created a simple and easily extendable app to track whatever parameter is relevant for me.

The scenes are basic input dialog which collects a specific activity or parameters (i.e. my weight, the number of Km of my car, fuel consumption, etc...)

The tasks are basic set of instruction and command to execute. The basic action shows the scene, collect the value entered by the user (me) and send the value to keen.io to be stored in a specific collection.

So far I have created the following scenes:

* **trackme_dlg_gas**: scene to acquire gas or electricity counter number
<br>
<br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-17-19-05-30__.png)
</center>


* **trackme_dlg_denti**: scene to acquire information whether my daughter has washed her teeth or not
<br>
<br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-17-18-57-09.png)
</center>

* **trackme_dlg_dieta**: scene to acquire the daily point of a diet program I am following
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-1.png)
</center>
 

* **trackme_dlg_peso**: scene to acquire my weight 
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-1_peso.png)
</center>


* **trackme_dlg_rifornimento**: scene to acquire the information about my car when I refill the tank
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2_rifornimento.png)
</center>

* **trackme**:  the main app scene
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-1_trackme.png)
</center>

<br>
So far I have created the following tasks:
* TRACKME_PESO
* TRACKME_GAS
* TRACKME_ELETTRICITA
* TRACKME_DENTI
* TRACKME_DIETA
* TRACKME_RIFORNIMENTO
* TRACKME: the main task 

<br>
All the above tasks are executed when the relative icon in the main scene is tapped with the finger.

* TRACKME_KEEN_CONFIG: contains the keen.io configuration 
* TRACKME_KEEN_SENDER: sends through HTTP POST the event data information to cloud keen.io

The two above tasks do not have any scene associated. They are just used to interact with keen.io service.

Some of the above task and scenes are configured through the use of Tasker's variable.
This is to allow anyone to easily change important parameters.

As an example the title of each scene is not hard-coded but is defined in a variable. So you can change it without modify/editing the scene.

### Keen.io Configuration
In order to use this tasker app you first need to configure a couple of simple kee.io parameters.
You can find such information in your keen.io's account page.

What you need is your keen.io:

* Project ID
* API Key

Now you can open the TRACKME_KEEN_CONFIG task and set the following variables:

* %TRACKME_KEEN_PROJECT_ID: in the To field insert your keen.io Project ID
* %TRACKME_KEEN_API_KEY: in the To field insert your keen.io API Key

That's it!! At this stage your Track Me app is ready to use.

### Other Configurations
Each task which is associated with an image icon in the Track Me app has few variables can be customized according to your own preferences.

Let's analyze those variables:

* %TRACKME_DIAG_TITLE:  change the content of this variable to personalize the Title of the UI dialog associated to the task
* %TRACKME_KEEN_COLLECTION:  change this variable to personalize the name of the keen.io's collection you want to store the data in
* %TRACKME_KEEN_EVENT:  change the content of this variable to personalize the data structure of your data event you want to store on keen.io cloud

Next to those variables there are other text strings that can be changed in order to display your preferred text messages. (i.e. all my messages are in Italian, but you can change it with English text)

### Extending Track Me app
I provide a template scene called trackme_dlg_template.

In order to create a new tracker follow the below steps:

* duplicate the template scene
* customize the template scene as you prefer
* make sure your new scene properly set a variable called %TRACKME_DLG_VAL.  This is the data field which will go into the %TRACKME_KEEN_EVENT variable (I have used variables to pass data from scenes back to the task and to keen.io cloud)

The %TRACKME_DLG_VAL variable should be set according to the below:

1. NaN in case you want to abort the operation (i.e. pressing the Cancel button)
2. Value in case you want to send an event data to keen.io


* create or duplicate an existing task
* properly configure the newly created task
* edit the main trackme scene
* add a new image to main scene (select your preferred icon)
* associate such an image to the newly created task (see above)
* edit the text below the icon image in the main scene

That's it. You can extend Track Me app with as many tracker as you want in few minutes.

### Icons
In my Track Me app I have used a mix of built-in icon and icons from the **Glossy Silver HD** icon pack (freely available in Play Store)

Obviously this is my choice but nothing is preventing you to use a complete different icon set.


### Code
All the tasker scenes and tasks are available on my [git hub](https://github.com/mancusoa74/TRACKME "git hub")

Download it, use it, change it, improve it, do whatever your like and let me know your result. I can only learn from you!!! 

_**NOTE**: I provide on github the userbackup.xml file. This way you can very easily import the full Track Me application in your Tasker. Please note however that this will completely overwrite and existing profiles, tasks and scenes. So always make sure you make a proper backup of your Tasker objects. _

### Use
Let's now see a quick example on the usage of Track Me app

* run the trackme task: I do it by tapping on a icon on my home screen on Android phone (you can add it through tasker widget
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-1_main.png)
</center>
<br><br>


* Click one of the icons (Peso = Weight in this example)
* The proper UI dialog is now shown
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-1_peso2.png)
</center>
<br><br>


* Enter the weight though keyboard
* Press the Send (INVIA) button
* Now the dialog close and you will see again the main app
* A couple of confirmation message will be shown
<br><br>
<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-17-22-18-03.png)
</center>
<br><br>
 
_Sending Data_

<center>
![](https://openmerchantaccount.com/img/Screenshot_2015-01-17-22-18-06.png)
</center>
<br><br>

_Weight correctly registered_

At this stage your weight has been correctly sent and accepted by keen.io. It is now stored in your trackme_peso collection and it is available for further use (analytics).


If you regularly (daily or weekly) send your weight to keen.io you can easily answer to questions like those:
* what was my minimum weight in the last 6 months
* what was my maximum weight in the last 6 months
* what was my average weight in the last 6 months
* how many time I have gone above the 75 Kg in the last 6 months
* ...
* ...

Let's see now that the weight just sent to keen.io is properly stored.
Go to your keen.io account and select the project you have configured in %TRACKME_KEEN_PROJECT_ID

You should see something like that

![](https://openmerchantaccount.com/img/keen_view2.png)

Now click on _Last 10 Events_

![](https://openmerchantaccount.com/img/10_events.png)

As you can see there are 5 different events (weight) in my collection.

The #1 is the last sent. Click on it and you show see something like that

![](https://openmerchantaccount.com/img/event_detail.png)

Now we can see that the weight (80 Kg) we have inserted has been properly stored by keen.io

### Contribute
If you are interested in this concept feel free to contribute.
You can do it in many ways:
* spot errors
* make suggestion to improve the existing app.
* create new scenes and task
* suggest new trackers
* improve the graphical design
* ...


### Conclusion
The combination of such incredible tools like Tasker and keen.io allows me to quickly and easily keep track of the important aspect of my life.
It has never been easier than now to create useful application for our daily life. We should take advantage of that.

I hope the sharing of my work here will create some discussion. I am curious to read about new tracker and new aspect of our busy life to track and analyze.

In part 2 I will quickly show how to visualize and analyze the data collected and stored on keen.io.

Cheers!!



<img src="https://api.keen.io/3.0/projects/54bae2f990e4bd31acbe257d/events/trackme_airpair?api_key=8f78c2ac53f8fb11725b1262d0af9f339334d67581241b3d86469524b8cfc038091f8b1f9b2fd84f7e1a551900e87cc1f72cb9f835778aed02b3246b2f38a1f610fab167fda89e7cf3f906eac95dd4285135e72194e9e16e2bef7f40227c4ba98683419496c294396aeec368021a354e&data=ewogICAgImtlZW4iIDogewogICAgICAgICJhZGRvbnMiIDogWwogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAibmFtZSIgOiAia2VlbjppcF90b19nZW8iLAogICAgICAgICAgICAgICAgImlucHV0IiA6IHsKICAgICAgICAgICAgICAgICAgICAiaXAiIDogImlwX2FkZHJlc3MiCiAgICAgICAgICAgICAgICB9LAogICAgICAgICAgICAgICAgIm91dHB1dCIgOiAiaXBfZ2VvX2luZm8iCiAgICAgICAgICAgIH0KICAgICAgICBdCiAgICB9LAogICAgImlwX2FkZHJlc3MiIDogIiR7a2Vlbi5pcH0iLAogICAgInVzZXJfYWdlbnQiIDogIiR7a2Vlbi51c2VyX2FnZW50fSIsCiAgICAiaGl0IjogMSwKICAgICJwb3N0X2lkIjogMSwKICAgICJwb3N0IjogIlRyYWNrIHlvdXIgbGlmZSB3aXRoIFRhc2tlciBhbmQgS2Vlbi5pbyAtIFBhcnQgMSIKfQo="></img>

x