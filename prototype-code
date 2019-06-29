// intro movie clipped from https://www.videvo.net/video/old-fashioned-film-leader-countdown/1351/
//Play with Me and We
//Special thanks to Professor Zeven Rodriguez!

import gab.opencv.*;
import processing.video.*;
import java.awt.*;

Capture video;
OpenCV opencv;

int counter = 0;
//int invert = 0;
int savedTimer;
int totalTime = 0;

int totalTime2 = 100;
int savedTimer2 = 0;
int imgCounter = 0;


ArrayList<Contour> contours;

ArrayList<PImage> images =new ArrayList<PImage>();

boolean loadImg = false;


PImage dst;
PImage img;

int mode = 0;

//int mode = 1;
//int mode = 2;
//int mode = 3;

//int mode = (1,2,3);

//PImage[] images = new PImage[6]; //can i leave new Image [] empty? don't know how many will be just yet.
//copy of copy of someone else's code
//https://forum.processing.org/one/topic/loading-pimage-into-an-array.html

boolean startTime = false;

Movie myMovie;

//Movie movie; 

void setup() {
  size(1280, 480);
  video = new Capture(this, 640/2, 480/2);
  opencv = new OpenCV(this, 640/2, 480/2);
  opencv.loadCascade(OpenCV.CASCADE_FRONTALFACE);  

  myMovie = new Movie(this, "countdown-video-480.mov");
  //  myMovie.loop();a

  video.start();
}

void draw() {


  if (startTime == true) {

    int passedTime = millis() - savedTimer;
    // Has five seconds passed?
    if (passedTime > totalTime) {
      println(totalTime + " milliseconds have passed!");
      background(random(255)); // Color a new background
      savedTimer = millis(); // Save the current time to restart the timer!

      if (mode < 3) {
        mode++;
      }
    }

    // do all millis stuff
  }
  if (mode == 1) {
    // video countdown
    println("mode1");
    totalTime = 3000;
    myMovie.play();
    image(myMovie, 0, 0);
  } else if (mode == 2) {
    println("mode2");

    myMovie.stop();


    totalTime = 2000;

    //video processing and recording

    scale(2);
    opencv.loadImage(video);

    opencv.gray();
    //opencv.erode();

    opencv.threshold(85);
    // opencv.invert();
    //filter (invert);

    dst = opencv.getOutput();

    contours = opencv.findContours();

    //unfiltered
    image(video, 0, 0 );
    //filtered
    image(dst, 320, 0);

    noFill();
    strokeWeight(3);

    for (Contour contour : contours) {
      fill(0, 255, 0);
      contour.draw();

      fill(255, 0, 0);
      beginShape();
      for (PVector point : contour.getPolygonApproximation().getPoints()) {
        vertex(point.x, point.y);
      }
      endShape();
    }

    String filename = "data/image" + counter + ".png";
    counter++;
    saveFrame(filename);
  } else if (mode == 3) {
    println("mode3");

  if(loadImg == true){
     for(int i = 0; i < counter; i++) {
      String curFile = "image" + i + ".png";
      //println(curFile);
      PImage curImage = loadImage(curFile);
      images.add(curImage);
      
    }
    
        println("done?");

    loadImg = false;
  }
  
  
     int passedTime2 = millis() - savedTimer2;
    // Has five seconds passed?
    if (passedTime2 > totalTime2) {
      println(totalTime2 + " milliseconds have passed!");
      savedTimer2 = millis(); // Save the current time to restart the timer!
   // println(counter);

     imgCounter++;
     if(imgCounter > images.size()-1){
       imgCounter = 0;
     }
    }
  
  PImage currentImage = images.get(imgCounter);
  
  image(currentImage,0,0);
 

    //playback
    //for (int i = 0; i < images.length; i++) {
    //  images [i] = loadImage ("image"+i+".png");
    //}
    startTime = false;
  }
}


//void movieEvent(Movie m) {
//  m.read();
//}

void captureEvent(Capture c) {
  c.read();
}

void movieEvent(Movie m) {
  m.read();
}

void mousePressed() {

  String filename = "data/image" + counter + ".png";
  counter++;
  saveFrame(filename);
}

void keyPressed() {
  //mode = 1;
  startTime = true;
  savedTimer = millis();
  savedTimer2 = millis(); 

  myMovie.jump(0);
  loadImg = true;

  if (mode == 3) {
    mode = 1;
  }
}
