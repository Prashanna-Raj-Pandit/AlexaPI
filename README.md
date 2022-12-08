# AlexaPI

https://user-images.githubusercontent.com/108394628/206355186-cc6848f8-4a3e-40c7-8d82-72c354738bbb.mp4



TABLE OF CONTENTS
- Acknowledgement
- Introduction
- Objectives
- Functions
- Working mechanism
- Key SDK components
- Making of
  - Prerequisites
  - Required hardware
  - Required software
  - Register your product with Amazon
- Setup your environment
- Build the AVS-Device-SDK
- Run the installed script
- Check for authorization
- Indicate the device state with sound 
- Modify focus manager
- Indicate the device state with LEDs
- Reboot Raspberry PI to AVS-device
- Home Automation
  - Create an account in Sinric
  - Create smart home devices
  - Connect ESP-8266 with AlexaPI using API of Sinric
  - Discover devices by Raspberry PI(AlexaPi)
  - Connect devices by PI
  - Sample check






## Acknowledgement

In the present world of competition there is a race of existence where people have will to rise for success. Project is like a bridge between theoretical and practical working. With this willing we joined this project. First of all, we would like to thank the supreme power; the Almighty God who is obviously the one has always guided us to work on the right path of life. Without his grace this project couldn’t become a reality. Next to him are our parents, whom we are greatly indebted for our brought up with love and encouragement to this state. At last but not the least we are thankful to all our teachers and friends who have been always helping and encouraging us. We have no valuable words to express our thanks, but our heart is full of the favors received from every person.

Thank you!














**Prashanna Raj Pandit**

**Dewashish Atal**

**Prashanna Karn**

**Neha Dahal**

## Introduction:

In this project, we are going to present how to make Alexa voice service device SDK from amazon. This can be made using the sample app that is included with the AVS device SDK from Amazon website.

**AlexaPI**, known simply as **Alexa**, is a [virtual assistant](https://en.wikipedia.org/wiki/Virtual_assistant "Virtual assistant") [AI](https://en.wikipedia.org/wiki/AI "AI") developed by [Amazon](https://en.wikipedia.org/wiki/Amazon_\(company\) "Amazon (company)"), first used in the [Amazon Echo](https://en.wikipedia.org/wiki/Amazon_Echo "Amazon Echo") and the Amazon Echo Dot [smart speakers](https://en.wikipedia.org/wiki/Smart_speaker "Smart speaker"). It is capable of voice interaction, music playback, making to-do lists, [setting alarms](https://en.wikipedia.org/wiki/Alarm_clock "Alarm clock"), streaming podcasts, playing audiobooks, and providing weather, traffic, sports, and other real-time information, such as [news](https://en.wikipedia.org/wiki/News "News"). Alexa can also control several [smart devices](https://en.wikipedia.org/wiki/Smart_device "Smart device") using itself as a [home automation](https://en.wikipedia.org/wiki/Home_automation "Home automation") system. Users are able to extend the Alexa capabilities by installing "skills" (additional functionality developed by third-party vendors, in other settings more commonly called [apps](https://en.wikipedia.org/wiki/Mobile_app "Mobile app") such as weather programs and audio features).

Most devices with Alexa allow users to activate the device using a wake-word (such as *Alexa*). Currently, interaction and communication with Alexa are available only in English, German, French, Italian, Spanish, Portuguese, Japanese, and Hindi. In Canada, Alexa is available in English and French (with the [Quebec](https://en.wikipedia.org/wiki/Quebec_French "Quebec French") accent).But this service is not in our country (i.e. NEPAL). 

2019 Amazon launched many new devices achieving many records while competing with the world's smart home industry. Since this service is not available in our country, this project is built in the vision of providing service in home automation. This project uses raspberry PI as the major microcontroller which receives audio from USB microphone and sends to Audio Input Processor.

## Objectives:

- To provide the service of voice interaction, music playback, making to-do list, setting alarm.
- To provide weather, traffic, sports and real time information such as news.
- To provide the service of home automation.

## Functions

**AlexaPI** can perform a number of pre-set functions out-of-the-box such as set timers, share the current weather, create lists, access [Wikipedia](https://en.wikipedia.org/wiki/Wikipedia "Wikipedia") articles, and many more things. Users say a designated "wake word" (the default is simply "Alexa") to alert an Alexa-enabled device of an ensuing function command. AlexaPi listens for the command and performs the appropriate function, or skill, to answer a question or command. When questions are asked, AlexaPI converts [sound](https://en.wikipedia.org/wiki/Sound "Sound") waves into text which allows it to gather information from various sources. Behind the scenes, the data gathered is then parsed by [Wolfram's](https://en.wikipedia.org/wiki/Wolfram_Research "Wolfram Research") technology to generate suitable and accurate answers.

In addition to performing pre-set functions, AlexaPI can also perform additional functions through third-party skills that users can enable. AlexaPI also favors in home automation. In this project AlexaPI is used to automate lights, cooling fans, doors and some normal home appliances sample. This can also be used to connect real home appliances.

Some of the major features are highlighted below:

- **Home automation:**

In the home automation space, AlexaPI can interact with several devices build and connected with ESP8266 module


- **Music**

AlexaPI supports a multitude of subscription-based and free streaming services on Amazon devices. These streaming services include: Prime Music, Amazon Music, Amazon Music Unlimited.

AlexaPI is able to stream media and music directly. To do this, Alexa's device should be linked to the Amazon account, which enables access to one's Amazon Music library, in addition to any audiobooks available in one's Audible library. Amazon Prime members have an additional ability to access stations, playlists, and over two million songs free of charge.


**Working Mechanism:**

Before we get into the first step of getting started with the Raspberry PI, we want to talk about the flow of information within the SDK.

When we say “ALEXA”, the Audio Signal Processor takes our voice and digitizes it, cleans it up and makes it easier to process. Later at this, it sends it to the Shared Data Stream (SDS) where it takes the data and splits it to two places: first place being the Wake Word Engine (WWE) and also the Audio Input Processor (AIP). When the data goes to the WWE it is detecting wake word or words that trigger it to listen for command. The Audio Stream “ALEXA” goes to the WWE which then senses wake word and it triggers the audio input processor. The Audio Input Processor handles audio input that is sent to AVS these include on device microphones, remote microphones and other audio input sources. The Audio Input Processor also includes the logic to switch between different audio input sources. Only one audio input source can be sent to AVS at a given time.

Next, the Audio Input Stream that contains “ALEXA” is sent to Alexa Communication Library or ACL. The ACL is the portion that keeps a persistent connection between AlexaPI and cloud to send and receive message as necessary. Once the message is sent to the cloud, Alexa in cloud processes the message and sends a message back called directive to instruct our product (i.e. AlexaPI) to take action. Now the ACL takes the directive that is just received from the cloud and passes it on to the Alexa Directive Sequencer Library or ADSL. The ADSL takes directives that come in and enforces the ordering of execution of incoming directive and routes them to Capability Agents for handling. Once the directive that just come in from the cloud is slotted to go. Next, it passes that directive off to the capability agents. A capability agent handles Alexa driven interaction and creates events. Each capability agent for corresponds to a specific interface exposed by the AVS API. In this case, we need speech synthesizer so the ADSL passes speech file to speech synthesizer. Speech synthesizer then plays the speech file through Audio Player. 

Now the Activity Focus Manager Library or AFML is interesting because it changes the different activities from the foreground to background. There are actually three different levels of priorities. For example, dialogues are higher priority that contain such as music. Suppose, we are listening to music and a dialogue comes in. The ADSL sends a dialogue directive to the speech synthesizer. The speech synthesizer tells AFML that it wants the foreground channel. AFML tells the audio player to go the background. The audio player ducks until it is informed that the speech synthesizer is done. When the speech synthesizer is done playing its audio, it informs AFML in turn notifies the audio player it can go back to the foreground.  


**AVS DEVICE SDK ARCHITECTURE**

![](Aspose.Words.c641257d-6591-4497-85b2-55a5d2034c52.001.png)

## Key SDK Components

**Audio Input Processor**

Handles the audio input to Alexa Voice Service from on-device microphones, remote microphones and other audio input sources.
#### **Wake Word Detection (WWD)**
Includes the hooks to add your own wake word engine to detect the Alexa wake word in an input stream.
#### **Alexa Communications Library (ACL)**
Serves as the main communications channel between the device and the Alexa Voice Service.
#### **Alexa Directive Sequencer Library (ADSL)**
Manages the order and sequence of [directives](https://developer.amazon.com/public/solutions/alexa/alexa-voice-service/reference/interaction-model#interfaces) from Alexa Voice Service.
#### **Capability Agents**
Handles Alexa-driven interactions; specifically, directives and events. Each capability agent corresponds to a specific interface exposed by the AVS API.
#### **Activity Focus Manager Library (AFML)**
Prioritizes the channel inputs and outputs as specified by the [AVS Interaction Model](https://developer.amazon.com/public/solutions/alexa/alexa-voice-service/reference/interaction-model#channels).

##Methodology (making of):

**Prerequisites**

**Required hardware**

- **Raspberry Pi** - Use a Raspberry Pi 3 or 4.
- **Micro SD card** - Minimum 8 GB.
- **USB 2.0 microphone** - Since Raspberry Pi does not have a built-in microphone. To interact with Alexa you must plug in an external microphone.
- **External speaker or headset** - Your audio source needs to connect to the Pi with 3.5mm audio cable.
- **USB keyboard and mouse** - Choose any compatible keyboard and mouse.
- **HDMI monitor** - Choose any compatible monitor. Alternatively, you can [remote SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) into your Pi.
- **Internet connection** - Ethernet connection or a 2.4 GHZ Wi-Fi.
- **ESP 8266(Node MCU)**- A Wi-Fi- module to connect raspberry PI
- **8 channel Relay** – A 8 channel relay to connect your devices.
- **LEDs**- LEDs to indicate the device state
- **Jumper cables**- jumper cables to connect devices. 

**Required software**

- **Raspbian Operating System** - [Raspbian Buster](https://www.raspberrypi.org/blog/buster-the-new-version-of-raspbian/) full 

**Register your product with Amazon**

Before we install the AVS Device SDK, we must [Register an AVS Product and Create a Security Profile](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/register-a-product.html). After our device is registered, we download a config.json file that contains our client ID and client secret. The client ID and client secret authorize our device, so we can retrieve access tokens from AVS. Our config.json file facilitate the authorization calls between your device and AVS.

**Set up your environment**

First we flash the raspian image file in the SD-card and thn insert the card n raspberry pi. After that we connect our raspberry to internet either via wifi or Ethernet cable. Next we download putty apk and and connect our raspberry pi in putty through its IP address. Now we put the config.json file in /home/pi folder and update and upgrade the raspberry pi. 

The first step is to run apt-get update and apt-get upgrade. This ensures that your Pi has an updated and upgraded list of packages.

*cd /home/pi/*

*sudo apt-get update*

*sudo apt-get upgrade*

## Build the AVS-device-SDK

Next, we get the AVS Device SDK configuration scripts from the AVS SDK Github repo. These scripts contain all the logic to build the SDK with single command. When we run them, they download the AVS Device SDK and install any required dependencies. These scripts get updated with each SDK release and automatically download the latest SDK for us.

We have to open terminal to the /home/pi directory. Enter the following command as single block statement.

wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/setup.sh \

wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/genConfig.sh \

wget https://raw.githubusercontent.com/alexa/avs-device-sdk/master/tools/Install/pi.sh
## **Run the Installed Script**
The **setup.sh** script builds the SDK and installs dependencies that allow our device to the following.

- Maintain an HTTP/2 connection with AVS.
- Play Alexa TTS and music.
- Record audio from the microphone.
- Store records in a database (persistent storage).

To run the install script, open a terminal and run **setup.sh** using your **config.json** file and a device serial number (DSN) as arguments. If you get an error, make sure your config.json file is in the same folder as the setup.sh script.

*cd /home/pi/*

sudo bash setup.sh config.json [-s 1234]

Once you've finished compiling, a success message appears — **[100%] Built Target SampleApp**. If your device freezes - don't worry, restart it by unplugging your Pi's power cord. When you get back to your desktop, re-run the above setup.sh command to finish your install.

**Check for authorization**

Once the AVS-Device-sdk is installed, now we need to authorize the sample app. For this we need a refresh token that the amazon provides us when we run the sample app for the first time.

In a terminal window, navigate to the /home/pi directory and run **startsample.sh**.

*cd /home/pi/*
*sudo bash startsample.sh*

Once the sample app starts, we'll see a series of rapidly scrolling debug messages in the terminal window stating, **Checking for authorization**. We need to Scroll through the debug messages and look for a box with a URL, it contains our Alexa authorization code.

After that we need to go to  [amazon.com/us/code](https://amazon.com/us/code) and enter the authorization code and get the sample app authorized. We should wait until the following doesn’t appear.

1. *###########################*
1. *#       Authorized!       #*
1. *###########################*
1. *########################################*
1. *#       Alexa is currently idle!       #*
1. *########################################*

we are now ready to use the sample app. The next time we start the sample app, we do not have to authorization your device.

**Notes:**	

- If we exit out of sample app with the k command, the CBLAuthDelegate database clears and we must reauthorize our client.
- If you want to move this authorization to another sample app installation, we must copy the **deviceInfo** object within AlexaClientSDKConfig.json to the new installation. we will also need to copy the file "/home/pi/sdk-folder/application-necessities/cblAuthDelegate.db" to the new installation, and update **AlexaClientSDKConfig.json** in the new installation so that the **cblAuthDelegate's databaseFilePath** property points to it.

To re-launch the sample app, run the following command. It includes the path to our configuration file and the Sensory wake word model.

*cd /home/pi/*

*sudo bash startsample.sh*

**Indicate device state with sounds:**
### **Modify UImanager file**
When we speak the wake word **"Alexa"**, we want an indicator that our product heard us. This may be an **LED activating** or changing color on the device. But what if someone puts our product up on a high shelf, around the corner, or somewhere we can't see it? Maybe there just wasn't a good place on our product to put some LEDs? In this case, we may want our device to play an **audio cue** to confirm when AlexaPI recognizes the wake word.

Amazon provides a **library** of sound clips for us to use when designing our product. Our commercial device should behave consistently with other AVS products so our customer can easily understand the device state. In this step, we'll modify the **User Interface Manager** to play a **Wake** sound each time Alexa's state changes to LISTENING.

First, we'll need to download the sound library. From [AVS Dashboard](https://developer.amazon.com/avs/home.html#/avs/home), clicking on our **Resources** tab next to **Analytics Dashboard** under Alexa Voice Service link.

Scrolling down until we see the **Alexa Sound Library for AVS** box, clicking on the **View** box, then "Download" to get the library onto our Pi. Navigate to our */home/pi/Downloads* folder in the file explorer, and right-click on the zipped archive and select **Extract Here**.

Now, we have local copies of the key sounds we'll use to inform users of your product state. Opening the **"Key Sounds for AVS"** folder and coping the file **med\_ui\_wakesound.wav**. Pasting a copy of this sound into our */home/pi/sounds* folder - this is the path we'll point to later when we're ready to play the sound!

` `**Note:** If our Alexa sample app is still running, then quit the application or closing the terminal window before we begin editing the SDK source code.

In the **File Manager**, navigate to */home/pi/avs-device-sdk/SampleApp/src/* and open **UIManager.cpp** with a text editor.

Near the top of the file where we see the other **#include** statements, add #include <cstdlib>. This will enable the play function that we'll add in the next step.

we'll need to find the right UX State and add a path to the **Wake Sound** .wav file to enable our audio cue. Near the bottom of **UIManager.cpp** in the printState() function, where it says case DialogUXState::LISTENING:, add the following command:

system("play /home/pi/sounds/med\_ui\_wakesound.wav");

Don't forget to **save your text file** before closing it! If you get a "Save As…" dialog and are unable to save the file as the same name, we'll need to update ownership permissions. In the terminal, type the following and hit return:

*sudo chown -R pi:pi /home/pi*

After successfully saving **UIManager.cpp** we'll need to **rebuild the Sample App** for the changes to take effect. First, quit out of your existing instance of the Sample App (if it's still running) by typing **q** in the terminal and hitting **return**. Still in the terminal window, input the following command to rebuild the Sample App:

*cd /home/pi/build/SampleApp*

*sudo make*

It'll take a minute to rebuild with the changes we made to UIManager.cpp. Once we get to 100%, restart your Sample App by initiating the **startsample.sh** script in a terminal:

*cd /home/pi/*

*sudo bash startsample.sh*

Every time we speak the wake word **"Alexa"** to our prototype (Alexa's state changes to **"Listening…"**) we should hear the **wake sound** play, indicating that our client device has opened a channel to the cloud. If we initiate a **multi-turn interaction**, we'll also hear the sound when Alexa is awaiting our answer. In the terminal window, we'll see the following message when our sound clip is successfully played.

Have fun modifying the **UI Manager** on our prototype - feel free to get creative and experiment with different sounds at various states. Share what we've built by sending us a link via the feedback button!

**Modify focus manager:**

**Modify Alexa Focus Manager Library**

Our device only has one speaker, but at any given time there might be multiple **Capability Agents** that wish to use it. The **Focus Manager** exists to ensure a consistent user experience and prevent the chaos of multiple agents speaking over each other at the same time. But how does it know what to give control of the speaker to? We've divided different functions (such as **Speech**, **Alarms**, and **Music**) into various **Channels** that take priority over each other in a structure determined by the Focus Manager.

What if our device's **specific use case** involved critical functions that we didn't want interrupted? For example, if we were building an Alexa-enabled navigation system, our user wouldn't want to miss Alexa's driving directions because an alarm went off and took control of our speaker. In this case, we'd want to put driving directions in the **highest priority** channel. Let's try an example interaction to learn about the behavior of our Sample App's **Focus Manager**.

**Initiate two competing Capability Agents**

Because Alexa lives in the cloud, all AVS products become **more capable** every day. As our customers start doing more with our device, the Focus Manager will come into play more frequently. Let's create a situation that will force the Focus Manager to take control of the **Media Player** according to the existing **Channel Priority** set in your Sample App.

1. Ask **"Alexa, set a timer for 20 seconds"**.
1. You should receive a confirmation from Alexa - "*Twenty seconds - starting now*".
1. Quickly, say **"Alexa, sing me a song!"**
1. Within a few seconds, Alexa will start to sing you a pretty great song…
1. … but before the song has a chance to finish - the alarm goes off! Unfortunately, your song stopped - it lost the **Focus** of the device.
1. Say **"Alexa, stop"** to get the Alarm to quit beeping.
1. Once your **Alarms** capability agent has stopped, your song will be allowed to retake the device's **Foreground** channel.

Imagine if that song was actually *driving directions*, about to instruct you to exit off the freeway - you might have just missed your turn. Let's modify our **Focus Manager** to increase the priority of the **Content** channel over the **Alarms** channel.

**Modify your Focus Manager Interface**

1. In your File Manager, navigate to */home/pi/avs-device-sdk/AVSCommon/SDKInterfaces/include/AVSCommon/SDKInterfaces*
1. Right-click on **FocusManagerInterface.h** and select **Text Editor** to open the file.
1. Scroll down and you should see the **channel priorities** listed under the FocusManagerInterface class. Lower numbers are higher priority. Notice how rather than **1st/2nd/3rd**, they're listed as **100/200/300**? This gives you the space to create **entirely new channels** and place them wherever you wish. For example, you could create a channel number for driving directions and give it a priority of **1-99** to even interrupt **Dialog**.
1. For this exercise, we want to bump up the priority of **Content** so that it doesn't get stepped on by **Alerts**. CONTENT\_CHANNEL\_PRIORITY is currently set to 300. Let's make it a higher priority than our 20-second Timer (which is in the **Alerts Channel**) by changing that 300 to 199.

Once you've increased the priority of the Content Channel, save your **FocusManagerInterface.h** file and close it.

**Rebuild your modified sample app**

We'll need to **rebuild the sample app** for the changes to take effect. First, quit out of our existing instance of the Sample App (if it's still running) by closing the window, Ctrl-C'ing out, or the more elegant typing "**q**" and hitting **return**. Open a terminal and input the following command to rebuild the Sample App:

*cd /home/pi/build/SampleApp*

*sudo make*

You'll see the modified libraries rebuilding - it might take a couple of minutes. When you get the message that your target SampleApp is 100% built, it's time to **re-launch the Sample App** and try the same interaction. Restart the Sample App by running this command in a terminal:

*cd /home/pi*

*sudo bash startsample.sh*

Now, **start a 20-second timer** again and ask Alexa for another song. This time, your song should keep playing even when your timer goes off. If you were building Alexa-enabled smart speakers for DJs, they might appreciate your device never interrupting a song.

Feel free to experiment with other priorities in the Focus Manager to create the **best user experience** for your product's *specific* use case. This can help differentiate your product from every other **Alexa-enabled device** on the market. Keep in mind that when you ship your own commercial Alexa-enabled products, they may have different **interaction models** or **capabilities**, but your customers will still expect your device to listen and respond instantly no matter what else is happening.

**Indicate device state with LEDs:**

Most AVS products differentiate themselves with **unique styling features**, but they all speak the same design language to ensure customers can easily interact with them. When we build our first Alexa-enabled device, we can follow [AVS' UX Guidelines](https://developer.amazon.com/docs/alexa/alexa-voice-service/ux-design-overview.html) to help your customers understand what's happening. Most Alexa-enabled products use LEDs to communicate the **"Attention State"** of the device.

![attention](Aspose.Words.c641257d-6591-4497-85b2-55a5d2034c52.002.png)

As we can see from the above table, attention state guidelines include **Blue LEDs** when Alexa recognizes the Wake Word (listening state), or **Red LEDs** when the user has turned off the microphones (privacy mode). In this workshop, we’ll use the AVS Device SDK to implement visual indicators of device state into your product.
### **Hook up your LEDs to the Raspberry Pi**
First we plug ribbon cable into the black breakout board and install it in the breadboard. Using two jumper wires, we attach them to the pins labeled **17** and **18** on the black breakout PCB. We can do this by plugging into the same row as them on the breadboard.

Install two **resistors** from your kit with color bands **red/red/black/gold**. This corresponds to **220** ohms which is enough to push some current through the LEDs without exploding them. Make sure the resistors **straddle** the middle of the breadboard.

Grab a **Red LED** and a **Blue LED** from your kit. Notice how one of the legs is shorter than the other? Put the **short leg** in the furthest right row on your breadboard - this should correspond to the **negative terminal** (GND) on the breakout board, marked as negative on both the black PCB and shown as a blue row on the breadboard.

The long leg of the LED should connect **through a resistor** to your jumper wires - wire **pin 17** to your Red LED's resistor, and **pin 18** to your Blue LED's resistor.

We need to check connections carefully **before** plugging the other end of the ribbon cable into the Raspberry Pi's header. Ensure your ribbon cable is aligned squarely on the Pi's header without any pins offset or sticking out.
### **Modify the AVS Device SDK to implement the Attention System**
` `**Note:** If we still have your Alexa sample app running, quit the application or close the terminal window before you begin editing the SDK source code.

Now let's write some software to activate the right pins on the Pi. In File Explorer, navigate to the folder *home/pi/avs-device-sdk/SampleApp/src*

We need to add the **WiringPi** library to the SampleApp project so that we can control output pins on our Raspberry Pi. Open the file **“main.cpp”** and add the include header statement at the top of the file as shown.

#include <wiringPi.h>

We will also initialize the library using the function **“wiringPiSetup”** and set up the GPIOs we plan on using to drive our Red and Blue LEDs. The Pi makes a couple dozen pins available for use, but for now, let's reserve two output pins for our tutorial. Still in **main.cpp**, scroll down to the int main function and add the following code:

*wiringPiSetup () ;*

*pinMode (0, OUTPUT) ;*

*pinMode (1, OUTPUT) ;*

**Save your text file** and close it. Still in the *home/pi/avs-device-sdk/SampleApp/src* folder, open the file “UIManager.cpp”. We need to include the WiringPi.h header file by adding #include <wiringPi.h> at the top of our file.

In our UIManager::microphoneOff() function, we should add digitalWrite (0, HIGH); to turn on the Red LED when your microphone is turned off:

Scroll down a bit to the UIManager::microphoneOn() function and add digitalWrite (0, LOW); to turn the Red LED back off when we exit Privacy Mode.

One more thing! We need to initialize that LED so it's not in an indeterminate state on startup. Scroll up to the UIManager::printWelcomeScreen() function and add digitalWrite (0, LOW); inside the brackets as shown.

Now let's add the Blue LED for Alexa's **Listening** state. Near the bottom of the file in the printState() function, where it says case DialogUXState::LISTENING:, add digitalWrite (1, HIGH); to drive the Pi's GPIO pin to 3.3V and turn on our LED.

Of course, we've got to switch the LED off when Alexa *isn't* listening. Let's do this by adding a digitalWrite (1, LOW); to states IDLE and THINKING. When we're finished, our states should include the code as shown below. Don't forget to save before closing.

For the final step, we'll need to make a change to the CMake file in order for the project to use the WiringPi library when we rebuild the Sample App. Open the file “CMakeLists.txt” from the same *home/pi/avs-device-sdk/SampleApp/src* folder and add target\_link\_libraries(SampleApp "-lwiringPi") at the bottom of the file as shown.
### **Rebuild the Sample app**
Open a terminal and input the following command to rebuild the Sample App to implement the changes we just made:

*cd /home/pi/build/SampleApp*

*sudo make*

We'll also need to re-input our credentials after adding wiringPi to the CMake file. We can do this by re-doing the initial install step. This should only take 30 seconds, and won't require you to re-authenticate.

*cd /home/pi/*

*sudo bash setup.sh config.json*

then we restart Sample App by initiating the **startsample.sh** script in a terminal:

*cd /home/pi/*

*sudo bash startsample.sh*

Now, say **"Alexa"** - we should see the Blue LED light up to indicate when our device is in the **"Listening"** state. Now we toggle our device in and out of **Privacy Mode** by typing **"m"** and hitting "return" in our Sample App – our Red LED should indicate the state.The **AVS Device SDK** allows us to easily implement the Attention State system in hardware. 

**Reboot Raspberry PI to AVS-device**

So till now we have built our AVS device SDK and also run the sample app. But here is a problem that whenever we want to run our sample app, we have to open terminal and write this cd /home/pi/ sudo bash startsample.sh command. So the correct command is actually sudo bash /home/pi/ startsample.sh. So no matter where we are in any directory, we can use this command to run our sample app. So next, we are going to modify our bash file by copying that command and pasting in it by running cd /home/pi/.bashrc /home/pi/.bashrc-original and then sudo nano /home/pi/.bashrc command. It is a hidden file that’s why it starts with dot. This command will take us to the bash file. Then going down to the bottom we just paste sudo bash /home/pi/ startsample.sh. Then we save the file and exit. After this when we open our terminal, we needn’t have to write our sample app code. It automatically runs the sample app. Then at last we open our terminal and reboot our Raspberry PI by sudo reboot command. And finally this makes our PI as a alexa built in device. After this we move to home automation part.

**Home automation**

This project mainly focuses on home automation to make a smart city. And we did this by building an alexa on Raspberry PI and hence connecting with Node mcu. Home automation or domotics is [building automation](https://en.wikipedia.org/wiki/Building_automation "Building automation") for a home, called a smart home or smart house. A home automation system will control lighting, climate, entertainment systems, and appliances. It may also include home security such as access control and alarm systems. When connected with the Internet, home devices are an important constituent of the [Internet of Things](https://en.wikipedia.org/wiki/Internet_of_Things "Internet of Things") ("IoT").

A home automation system typically connects controlled devices to a central hub or "gateway". The [user interface](https://en.wikipedia.org/wiki/User_interface "User interface") for control of the system uses either wall-mounted terminals, tablet or desktop computers, a mobile phone application, or a Web interface, that may also be accessible off-site through the Internet. Following points are  followed for home automation.

- Create an account in Sinric
- Create smart home devices
- Connect ESP-8266 with AlexaPI using API of Sinric
- Discover devices by Raspberry PI(AlexaPi)
- Connect devices by PI

For home automation, we are using a 8 channel relay with esp8266. After the connection is done we go to program our Node mcu through Arduino app. Here we first  have to include esp8266 library, arduinoJson.h and websocket.h library files. Then after to connect our Node mcu with AlexaPI, we have to create an account in sinric. Here Node mcu use the API key of sinric to communicate alexaPI and our devices. After the programming is done, we search for smart devices that we created recently in sinric through AlexaPI. After discovering devices we simply control it using voice command.



