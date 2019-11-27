import wblut.math.*;
import wblut.processing.*;
import wblut.core.*;
import wblut.hemesh.*;
import wblut.geom.*;

HE_Mesh mesh,wire;
WB_Render render;
WB_Plane[] planes;
int numPlanes;
int thisPlane;

HE_MeshCollection slices;
HE_MeshCollection theseSlices;

float drawCount;
boolean savedFiles;
boolean renderWire;

boolean doThis;
boolean doneEVERYTHING;

void setup() {
  size(2000,2000,P3D);
  //fullScreen(P3D);
  smooth(8);
  
  //poor Beethoven ... sliced up like that
  mesh=new HE_Mesh(new HEC_Beethoven().setScale(11));
  
  numPlanes = 5;
  planes=new WB_Plane[numPlanes];
  for(int i=0;i<numPlanes;i++){
    planes[i]=new WB_Plane(0,0,0,0, 0,1,-200+i*100); 
  } 
  
  theseSlices = new HE_MeshCollection();
  
  render=new WB_Render(this);
  renderWire=true;
  drawCount = 0;
  
  savedFiles = false;   
  doThis = true;
  doneEVERYTHING = false;
  thisPlane = 0;
}

void draw() {
  
  if (doThis & !doneEVERYTHING){
    doThis = false;
    println("starting the slices");
    HEMC_SplitMesh multiCreator=new HEMC_SplitMesh();
    multiCreator.setPlane(planes[thisPlane]);
    multiCreator.setCap(true);
    //multiCreator.setOffset(5);
    multiCreator.setMesh(mesh);
    slices=new HE_MeshCollection();
    slices.createThreaded(multiCreator);
  }
  
  background(0);
  directionalLight(255, 255, 255, 1, 1, -1);
  directionalLight(127, 127, 127, -1, -1, 1);
  translate(width/2, height/2, 0);
  rotateY(map(mouseX, 0, width, -PI, PI));
  rotateX(map(mouseY, 0, height, PI, -PI));
  
  pushMatrix();
    
    stroke(150,150,255);
    render.drawEdges(mesh);
    
    noStroke();
    fill(255,150,150);
    
    if (slices.isFinished() && !doneEVERYTHING){
      theseSlices.add(slices.getMesh(1).copy());
      thisPlane ++; 
      if (thisPlane < numPlanes){
        doThis = true;
        mesh = slices.getMesh(int(drawCount));
        //render.drawFaces(slices.getMesh(int(drawCount)));
      } else {
        doneEVERYTHING = true;
        println("done EVERY THING!");
        theseSlices.add(slices.getMesh(0).copy());
      }
    } 
    
    if (theseSlices.size()>0){
      println("there are "+theseSlices.size()+" slices");
      for (int i=0; i<theseSlices.size(); i++){
        translate(100,0,0);
        render.drawFaces(theseSlices.getMesh(i));
      }
    }
  
  popMatrix();
  
  if (doneEVERYTHING){
    if (!savedFiles){
      for (int i=0; i< theseSlices.size(); i++){
        HET_Export.saveToOBJ(theseSlices.getMesh(i), sketchPath(),"beet"+i+".obj");
      }
      savedFiles = true;
    }
  }
  
  slices.update();
}


