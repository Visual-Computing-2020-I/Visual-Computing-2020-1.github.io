# Proyect
> Developing ...

# Image to ACII


```java
PImage img;  // this variable stores de image
String palette = "$@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\\|()1{}[]?-_+~<>i!lI;:,"+"\"^`'. ";
void setup() {
  //load the image
  //img = loadImage("example2.png");
  img = loadImage("batman.jpg");
  size(500,500);
  int r,g,b;
  int av;
  color c;
  StringBuilder s = new StringBuilder();
  // transform the image to gray scale
  for(int i=0; i<img.width; i++){
    for(int j=0; j<img.height;j++){
      c = img.get(i,j);  
      r=(int)red(c);
      g=(int)green(c);
      b=(int)blue(c);
      av=(r+g+b)/3;
      c=color(av);
      img.set(i,j,c);
    }
  }
  // get 6x6 box pixel and have an average, pass that average to the getAscii function
  // and append to s
  System.out.println("Palette length: "+palette.length());
  for(int j = 0;j<img.height;j+=6){
    for(int i = 0; i<img.width; i+=6){
      s.append(getAscii(i,j));
    }
    s.append("\n");
  }
  
  String asciiImage = new String(s);
  //System.out.println(asciiImage);  // write string to a file
  PrintWriter output = createWriter("test.txt");
  output.print(asciiImage);
  output.close();
}

//takes every 6x6 pixel matrix and get the average of its gray value on the ascii palette.
char getAscii(int x, int y){
  int grayColor = 0;
  int average =0;
  color c;
  for(int i=x;i<x+6;i++){
    for(int j=y;j<y+6;j++){
      c = img.get(i,j);
      average += blue(c);
    }
  }
  grayColor = average/36;
  int idx = (grayColor*palette.length())/256;
  return palette.charAt(idx);
}

void draw() {
  image(img, 0, 0);
}
```
# P5.js schetch example
<iframe src="https://visual-computing-2020-i.github.io/Visual-Computing-2020-1.github.io/Class1.html" width="600px" height="400px"> </iframe>
