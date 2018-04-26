# GEOG 472/572: Geovisual Analytics
>
> **Instructor:** [Bo Zhao](http://ceoas.oregonstate.edu/profile/zhao/), zhao2@oregonstate.edu | **Office Hours:** T 3-4pm or by appt. @ [Strand Ag Hall 347A](https://www.google.com/maps/place/Strand+Agriculture+Hall,+170+SW+Waldo+Pl,+Corvallis,+OR+97331/@44.5656488,-123.2794268,17z/data=!3m1!4b1!4m5!3m4!1s0x54c040beaf30bd99:0x263a8015b6c0b3b5!8m2!3d44.5656481!4d-123.2772384)
>
> **TA:** [Jared Ritchey](http://ceoas.oregonstate.edu/profile/ritchey/), ritcheja@oregonstate.edu | **Office Hours:** T 5-6pm or by appt. @ [WLKN 210](https://www.google.com/maps/place/Wilkinson+Hall/@44.5682215,-123.2824915,17z/data=!3m1!4b1!4m5!3m4!1s0x54c040bb62b60cb5:0x27ea6238495f5669!8m2!3d44.5682215!4d-123.2803028)
>
> **Lecture:** [TR 11-11:50am](http://r25wv.ucsadm.oregonstate.edu/r25_wv/wv_servlet/wrd/run/wv_space.ByNameFindGroup?spid=118,spdt=today) @[WITH 205](http://r25wv.ucsadm.oregonstate.edu/r25_wv/wv_servlet/wrd/run/wv_space.Detail?RoomID=118) | **Lab:**  [T 6-7:50pm](http://dusk.geo.orst.edu/de/de_teach.html) @[WLKN 210](https://www.google.com/maps/place/Wilkinson+Hall/@44.5682215,-123.2824915,17z/data=!3m1!4b1!4m5!3m4!1s0x54c040bb62b60cb5:0x27ea6238495f5669!8m2!3d44.5682215!4d-123.2803028)
>
> **Catalog Course Description: GEOVISUALIZATION III: GEOVISUAL ANALYTICS (3).** Concepts and techniques underlying the production of maps by computer. Practical experience with a variety of computer mapping packages.

Welcome to GEOG 472/572: Geovisual Analytics! This course introduces geovisual analytical theories, advanced geovisual analytical methodologies, and some popular toolkits. In this course, students work collaboratively to solve a real-world problem using geovisual analytics. Also, This course is financially supported by [`Google Cloud Platform`](https://cloud.google.com/) :cloud:, each student of this course will have $50 budget for using the google cloud services.

No required textbook. Recommended Papers and online materials will be available on the course website, and some recommended books will be reserved in valley library. ***Students must complete required reading assignments before attending the corresponding lecture. In-class quizzes will cover the content of the reading assignments.***

Slocum,T. A., McMaster, R. M., Kessler, F. C., Howard, H. H., & Mc Master, R. B.(2008). [Thematic cartography and geographic visualization](https://www.amazon.com/Thematic-Cartography-Geovisualization-Terry-Slocum/dp/0132298341/ref=sr_1_fkmr0_1?ie=UTF8&qid=1522646663&sr=8-1-fkmr0&keywords=thematic+cartography+and+geovisualization+3rd+edition+pdf). Pearson; 3rd edition (April 14, 2008). ISBN-13: 978-0132298346


[**`A Terra Report about this course`**](http://terra.oregonstate.edu/2017/10/the-great-escape/)

## SYLLABUS


| **WK**    | **LECTURE  (T)**                                  | **LAB (T)**                                            | **LECTURE(R)**                 | **PROJECT**                                               |
| --------- | ------------------------------------------------- | ------------------------------------------------------ | ------------------------------ | --------------------------------------------------------- |
| **Wk 01**  | [Intro to this course](lectures/lec01/1-Intro.pdf)                            | [Lab1: Project Management for GeoViz](labs/lab01/) ([*`reading`*](labs/lab01/read.md))                    | [Geovisual Analytics Basics](lectures/lec02/) ([*`reading`*](lectures/lec02/read.md))            | [Introduction](project/intro.md), [*Project Prep*](project/prep.md)                                              |
| **Wk 02**  | [Brainstorm](lectures/lec03/)                                       | [GeoViz Programming Basics - Html, Css](lectures/lec04/) ([*`reading`*](lectures/lec04/part01/read.md)) and [jQuery](lectures/lec04/part02/) ([*`reading`*](lectures/lec04/part02/read.md)); [Lab2: GeoViz Programming Basics](labs/lab02/) ([*`reading`*](labs/lab02/read.md)) | [Interactive Maps using Leaflet](lectures/lec05/) ([*`reading`*](lectures/lec05/read.md)) | [Team-up](project/team-up.md)                                                   |
| **Wk 03**  | [D3 I](lectures/lec06/) ([*`reading`*](lectures/lec06/read.md))                                     | [Lab3: Interactive Map Design](labs/lab03/)                                       | [Spatial data Processing](lectures/lec07/)  ([*`reading`*](lectures/lec07/read.md))       | [*Proposal (`Due: 04/27, 5pm`)*](project/proposal.md)                                                  |
| **Wk 04**  | [D3 II](lectures/lec06) ([*`reading`*](lectures/lec08/read.md))                                            | Lab3 cont’d; [*debugging*:bug:](https://scotch.io/tutorials/debugging-javascript-with-chrome-devtools-breakpoints)                     | [D3 III](lectures/lec09/) ([D3 graphics](lectures/lec09/part01/), [DC.js](http://dc-js.github.io/dc.js/docs/stock.html)) ([*`reading`*](lectures/lec09/read.md))                         | Proposal revision; [:book:Name Convention](project/naming.md)                                         |
| **Wk 05**  | Layout Design using Bootstrap, GeoViz evaluation  ([*`reading`*](lectures/lec10/read.md)) | Lab4: Geoviz Module                                    | Color, Topography              | Sketch; Interface Design                                  |
| **Wk 06**  | SVG, Icons                                        | Lab5: Coordinated View or Storymap GeoViz                  | Word cloud                     | Design Scheme (Color, label, icon, and multimedia,  etc.) |
| **Wk 07**  | Real-time mapping, Heatmap                        | Fieldwork for Drone Mapping                            | GeoViz Critique                | Coding                                                    |
| **Wk 08**  | Geoviz of Structure-from-motion                   | Lab6: Point-cloud GeoViz                               | Hexagonal Geoviz               | Coding                                                    |
| **Wk 09**  | Network                                           | Lab6: cont’d                                           | Flow maps, Sankeys             | Fine-tuning                                               |
| **Wk 10** | Course Summary                                    | Project Q&A                                            | Final Presentation             | Presentation                                              |


> ***Note:*** :cloud: [*Google Cloud Platform?*](project/google-cloud-platfom.md) will be introduced in one of the lab sessions.

## LECTURES

You are expected to attend lectures twice a week. Most lectures have time allotted for discussions,in-class work and other activities. Your contribution in these generally, will be noted, and used to determine part of your final grade; just showing up won't count a whole lot toward this component.

Attending lectures and labs is important since these times provide you with access to the instructor and to other students. Keep in mind that not all lab assignment will be possible to finish in the allotted class time. Students will be expected to work on assignments outside of class during posted Lab hours. You are welcome to discuss the exercises amongst yourselves, in fact this is encouraged, but the final product you hand in must be your own work.

## LABS

During the term, there will be two lab assignments. The main purpose of the lab assignments is to learn how to apply and reflect upon the things we cover during the lectures, and to grasp proficient hands-on skills to solve real world problems. If you are having difficulty with these assignments you should ask for assistance, whether from fellow students, or from me. Whatever you do, ask someone but please note the academic integrity policy!

Lab assignments are required to be submitted electronically to Canvas unless stated otherwise. Efforts will be made to have them graded and returned within one week after they are submitted.Lab assignments are expected to be completed by the due date. *A late penalty of at least 10 percentage units will be taken off each day after the due date.*

If you have a genuine reason(known medical condition, a pile-up of due assignments on other courses, ROTC,athletics teams, job interview, religious obligations etc.) for being unable to complete work on time, then some flexibility is possible. However, if in my judgment you could reasonably have let me know beforehand that there would likely be a delay, and then a late penalty will still be imposed if I don't hear from you until after the deadline has passed. For unforeseeable problems,I can be more flexible. If there are ongoing medical, personal, or other issues that are likely to affect your work all semester, then please arrange to see me to discuss the situation. There will be NO make-up exams except for circumstances like those above.

## COURSE PROJECT

The final project is a major component of this course. For each group, there should be no more than three students. I recommend a group should be formed by graduate and undergraduate students. Each group will collaboratively work on a final project using geovisual analytics. The instructor will provide several topics for students to choose from. Students can also bring their own topics. Students in a group can work on a project of their common interests. Although the project topic is important, this project is more about how to apply the geovisual skills. So,students who want to team up as a group need to have a consensus that they are interested in using the similar geovisual tools and methods. Regarding the project topics, the instructor will provide a pool of topics to choose from during the first two weeks. In the rest of the term, students will concentrate on developing the project. The instructor and TA will provide necessary guidance in applying the geovisual skills for the projects. Since some of the topics are proposed by other faculty members in the university, a co-advisor/group member will join you to provide extra help.

Graduate students in GEOG 572 are required to provide **additional contributions** to the course.A graduate student can choose either making a presentation related to the lecture topic or being responsible for coordinating the project. The projects are expected to have advanced interactive features, introductory pages and other additional materials. All the final projects are expected to publish online, and the codes are expected to be shared on GitHub to contribute to both the open source community and academia.


## Libraries

1\. Leaflet

- css: https://unpkg.com/leaflet@1.3.1/dist/leaflet.css
- js: https://unpkg.com/leaflet@1.3.1/dist/leaflet.js

2\. jQuery

- js: https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js

3\. D3

- js v4: https://d3js.org/d3.v4.min.js
- js v5: https://d3js.org/d3.v5.min.js

4\. Dc.js

- css: http://dc-js.github.io/dc.js/css/dc.css
- js: http://dc-js.github.io/dc.js/js/dc.js

5\. crossfilter

- js: https://cdnjs.cloudflare.com/ajax/libs/crossfilter/1.3.12/crossfilter.min.js

6\. Chroma.js

- js: https://cdnjs.cloudflare.com/ajax/libs/chroma-js/1.3.6/chroma.min.js

7\. Leaflet Ajax

- js: https://cdnjs.cloudflare.com/ajax/libs/leaflet-ajax/2.1.0/leaflet.ajax.min.js

8\. Font awesome

- css: https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css

9\. Animate.css

- css: https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css


## RESOURCES

<img src="https://jakobzhao.github.io/img/brand.png" align="right" width="30%" height="30%"></img>

1\. [Students work from previous years](http://geoviz.ceoas.oregonstate.edu/geog4572-17sp.html)

2\. [Storymap.js - a map storytelling library](https://github.com/jakobzhao/storymap)

3\. [NeoCarto - a geovisual analytical framework](http://geoviz.ceoas.oregonstate.edu/neocarto/)


**Credits**

This course material is maintained by the [Cartography and Geovisualization Group at Oregon State University](http://geoviz.ceoas.oregonstate.edu). Some of the material in this course is based on the classes taught at MIT and Penn State University. We have heavily drawn on materials and examples found online and tried our best to give credit by linking to the original source. Please contact us if you find materials where the credit is missing or that you would rather have removed.
