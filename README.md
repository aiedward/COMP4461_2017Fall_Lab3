# Robot Programming
> Lab materials for how to program Pepper with Choregraphe.<br>
> Venue: Room 4221, Teaching Lab 1, Academic Building.<br>
> Date: Nov. 3, 2017

[![Choregraphe][chor-image]][chor-url]
[![License][license-image]][license-url]
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com)

<!-- [![Inline docs](http://inch-ci.org/github/sunzhida/COMP4461_2017Fall_Lab2.svg?branch=master)](http://inch-ci.org/github/sunzhida/COMP4461_2017Fall_Lab2) -->
<!-- [![Build Status][travis-image]][travis-url] -->

In this lab, we will introduce how to program with [Pepper](https://www.ald.softbankrobotics.com/en/robots/pepper) robot by Choregraphe. In this repository, there is a demo created by Choregraphe for you to get started.

## Table of Contents

- [Overview](#overview)
- [Configuration](#configuration)
- [Implementation](#implementation)
- [Tips](#tips)
- [Contribute](#contribute)
- [Meta](#meta)

## Overview

### What is _Pepper_?

[Pepper](https://en.wikipedia.org/wiki/Pepper_(robot)) is a humanoid robot by Aldebaran Robotics and SoftBank designed with the ability to read emotions. The [official website](http://doc.aldebaran.com/2-4/family/pepper_technical/index_pep.html) provides a technical overview of the Pepper robot, and you can find out its structure as well as the other technical details from the instruction. You can also refer to an
<img src="./images/PEPPERbrochure_EN.pdf" alt="official brochure"  width="100%"> to obtain more general information. During the development, you can interact with Pepper through [contact and tactile sensors](http://doc.aldebaran.com/2-4/family/pepper_technical/contact-sensors_pep.html).

![](images/imagePepperSpec_EN.jpg)

#### Hardware

The Pepper robot is 120 cm tall, and weights in 28 kg. It can move around freely through 360 degrees. The Pepper also features [20 degrees of freedom](http://doc.aldebaran.com/2-5/family/pepper_technical/motors_pep.html), which means it can move in 20 different ways. It has six motors in each arm, two in the neck, two in the hips, one for the knee, and another three for the wheels (as it has 20 motors in total). Pepper robot can move in any direction while rotating at the same time.

Pepper can express itself through [speech](http://doc.aldebaran.com/2-5/family/pepper_technical/loudspeaker_pep.html), [visual display](http://doc.aldebaran.com/2-5/family/pepper_technical/tablet_pep.html), and colorful [LEDs](http://doc.aldebaran.com/2-5/family/pepper_technical/leds_pep.html). It perceives the world through two [cameras](http://doc.aldebaran.com/2-5/family/pepper_technical/video_pep.html), four [microphones](http://doc.aldebaran.com/2-5/family/pepper_technical/microphone_pep.html) and a 3D [sensor](http://doc.aldebaran.com/2-5/family/pepper_technical/video_3D_pep.html) on his head, as well as several [touch sensors](http://doc.aldebaran.com/2-5/family/pepper_technical/contact-sensors_pep.html) on his body. To navigate safely, the Pepper robot leverages [laser sensors](http://doc.aldebaran.com/2-5/family/pepper_technical/laser_pep.html) and [sonars](http://doc.aldebaran.com/2-5/family/pepper_technical/sonar_pep.html) around the base. Pepper robot uses an embedded PC with an Intel Atom [card](http://doc.aldebaran.com/2-5/family/pepper_technical/motherboard_pep.html).

#### Software

Pepper robot can detect sound, people, obstacles based on its perception algorithms. The OS is a modified Gentoo distribution called OpenNAO with [NAOqi OS](https://www.ald.softbankrobotics.com/en/robots/tools) on top of it. The robotics OS runs all the software from hardware control to AI decision making.

N.B.: You can also find out [more](https://www.ald.softbankrobotics.com/en/robots/pepper/find-out-more-about-pepper) about Pepper.

### What is _Choregraphe_?

[Choregraphe](hhttp://doc.aldebaran.com/2-5/software/choregraphe/choregraphe_overview.html) is a multi-platform development application with graphical user interface. It allows you to create animations and behaviors on Pepper, test them on a simulated robot or directly on a real one, monitor and control Pepper, etc.

## Configuration

### How to install _Choregraphe_ 2.5.5?

By clicking on the [link](https://developer.softbankrobotics.com/us-en/downloads/pepper) of Choregraphe download page, you will get a license key as:

```
654e-4564-153c-6518-2f44-7562-206e-4c60-5f47-5f45
```

Keep it, and later we will use this key to activate our application. Download the install package that suits your operating system, and then follow the images below to install the application on your machine.

- Step one: <br><img src="./images/1.png" alt="step 1" width="50%">
- Step two: <br><img src="./images/2.png" alt="step 2" width="50%">
- Step three: <br><img src="./images/3.png" alt="step 3" width="50%">
- Step four: <br><img src="./images/4.png" alt="step 4" width="50%">
- Step five: <br><img src="./images/5.png" alt="step 5" width="50%">

N.B.: You can also refer to the official [installation guide](http://doc.aldebaran.com/2-5/software/choregraphe/installing.html).

### How to use _Choregraphe_?

Before starting the application, we need to connect to the '**NaoRobotNet**' (the password will be announced during the class). Then the initial interface of the application looks like below:

<img src="./images/interface.png" alt="interface" width="50%">

For each part of the interface, i.e., toolbar and other panels, please refer to the detailed explanation from the official [website](http://doc.aldebaran.com/2-5/software/choregraphe/interface.html). There is also a chart which describes each button in details.

## Implementation

After you get the `Demo` folder, please open the `.pml` file with Choregraphe, and you will see a project created by the same application previously. This project is created for the demonstration of Engineering School on [Information Day](https://infoday.ust.hk/), 2017. We will explain this demo in details:

### Flowchart

We design the workflow as below:

![](images/workflow.png)

### Detailed explanation for each component

For each component, the detailed design is as below:

| No. | Speech | Screen | Gesture | Sound | Remarks |
| :------| :------ | :------ | :------ | :------ | :------ |
| 1 | Hi! Welcome to the Engineering Commons. | Embrace_change ||||
| 2.1 | Do you want to see me dance? | Embrace_change ||||
| 2.2 || Embrace_change | Lift forearm to 90 degrees || If `yes`, go to 2.3, otherwise go to 3.1 |
| 2.3 || Embrace_change | Disco dance | Saxophone music ||
| 3.1 | Do you want to know more about today's Engineering admission events? | Embrace_change ||||
| 3.2 || Embrace_change | Lift forearm to 90 degrees || If `yes`, go to 3.3, otherwise go to 4.1 |
| 3.3 | Scan me to download the app! Engineering related talks will be held in Lecture Theatre J... K... and H. Besides, Consultation sessions will be provided for both DSE and non-DSE applicants. | Info Day app QR code | Related gestures |||
| 4.1 | Do you want to see something cool? | Info Day app QR code ||||
| 4.2 || Info Day app QR code | Lift forearm to 90 degrees ||If `yes`, go to 4.3, otherwise go to 5.1 |
| 4.3 | On campus today, you can watch robots battle against each other. You can even sign up to play! | Robomaster_image ||||
| 4.4 || Robomaster_image | Gorilla action | Machine gun sound||
| 4.5 | You can see an electric vehicle built by our students| EVcar_image||||
| 4.6 || EVcar_image | Driving action | Car sound||
| 4.7 | You can visit the labs to see experiments. | Lab_image ||||
| 4.8 | You can take pictures with the 3D trick art and explore the world of tomorrow through Augmented Reality. | HKUST.SENG_AR_LiPHY_app ||||
| 4.9 || HKUST.SENG_AR_LiPHY_app | Camera action | Shutter sound ||
| 4.10 | You can scan special lights for information. | HKUST.SENG_AR_LiPHY_app ||||
| 4.11 || HKUST.SENG_AR_LiPHY_app | Eyes light up |||
| 4.12 | For the 3D trick art, scan the HKUST.SENG AR app QR code shown on the left. For special lights, scan the Lie Fly app QR code on the right. | HKUST.SENG_AR_LiPHY_app | Speaking gestures |||
| 5.1 | If you need help finding information today, feel free to reach out to our Engineering Student Ambassadors. | ESA_image ||||
| 5.2 | Enjoy your day at the most beautiful campus in Hong Kong. See you around! | HKUST_image | Related gestures |||

Based on the scheme, we can add and change related gestures, screen image or speech text accordingly.

### Live demo

After we finished editing the program, we can upload the program to the Pepper robot while it is in the rest mode. Then we can click the `play` button to test the program on Pepper.

In the _Demo_ folder, the additional sound and image files are stored in the `html` subfolder, while the main program is in the `show.pml` file. You can start your program based on that.

## Tips

- [SoftBank Robotics Documentation](http://doc.aldebaran.com/)
- [Choregraphe Suite](http://doc.aldebaran.com/2-5/software/choregraphe/index.html)

## Contribute

We would love you for the contribution to **Lab3**, check the ``LICENSE`` file for more information.

## Meta

[Zhida Sun](http://zsunaj.student.ust.hk/). Distributed under the MIT license. See ``LICENSE`` for more information.

[chor-image]:https://img.shields.io/badge/Choregraphe-2.5.5-008C96.svg
[chor-url]: https://developer.softbankrobotics.com/us-en/downloads/pepper
[py-image]:https://img.shields.io/badge/Python-2.7-008C96.svg?style=flat
[py-url]: https://www.python.org/downloads/
[qi-image]:https://img.shields.io/badge/SDK-2.4.3-008C96.svg?style=flat
[qi-url]: https://community.ald.softbankrobotics.com/en/resources/software/language/en-gb/robot/pepper-3
[license-image]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: ./LICENSE.md
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[codebeat-image]: https://codebeat.co/badges/c19b47ea-2f9d-45df-8458-b2d952fe9dad
[codebeat-url]: https://codebeat.co/projects/github-com-vsouza-awesomeios-com
