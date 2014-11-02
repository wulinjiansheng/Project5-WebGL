=======================================
CIS565: Project 5: WebGL
======================================
Fall 2014 <br />
Bo Zhang<br />

![Alt text](https://github.com/wulinjiansheng/Project5-WebGL/blob/master/Pics/All%20Effects.bmp)

##Overview

This is a WebGL project based on implementation of GLSL vertex shader and GLSL fragment shader.

-------------------------------------------------------------------------------
PART 1 :
-------------------------------------------------------------------------------
* Sin-wave based vertex shader:
![Alt text](https://github.com/wulinjiansheng/Project5-WebGL/blob/master/Pics/Vertex%20Wave.bmp)
* Ripple Shader:
![Alt text](https://github.com/wulinjiansheng/Project5-WebGL/blob/master/Pics/Ripple.bmp)

About ripple:
I implement the ripple shader based on this link: https://glsleffects.codeplex.com/wikipage?title=Ripple, the main idea is as fllowing:
```
        float dist = distance(vec2(position.x,position.y),vec2(CenterPointX,CenterPointY));
        float height = Amplitude*sin(dist/(Wavelength/10.0) + u_time)*pow(Attenuation,dist);
```
* "CenterPoint" is the source of ripple, all circles of a ripple should has the same center point.
* "Amplitude" the amplitude defines how big the was is. The range of sin(x) is [-1,1], so, the height of ripple should be amplitude*sin(x). The x is the distance between current point and the center point, will be discussed next.
* "Attenuation", the power of a wave will weak down as it travels, the attenuation factor defines how fast the wave will weak down.
* "Wavelength" is how far the adjacent two points of the same height is.

-------------------------------------------------------------------------------
-------------------------------------------------------------------------------
PART 2:
-------------------------------------------------------------------------------
Given Features:
* Reading and loading textures
* Rendering a sphere with textures mapped on
* Basic passthrough fragment and vertex shaders 
* A basic globe with Earth terrain color mapping
* Gamma correcting textures
* javascript to interact with the mouse
  * left-click and drag moves the camera around
  * right-click and drag moves the camera in and out

Basic Features:
* Bump mapped terrain
* Rim lighting to simulate atmosphere
* Night-time lights on the dark side of the globe
* Specular mapping
* Moving clouds

Extra Features:
* Procedural water rendering and animation using noise 
* Shade based on altitude using the height map

#### Procedural water rendering and animation using noise 
To implement this feature, I make a perlin noise generator based on this link(http://www.dreamincode.net/forums/topic/66480-perlin-noise/): 
The only different thing is that we can't use bitwise operators in glsl, so I use a rand generator for the findnoise(). I adjust the parameters and here is the final effect (See the waves on ocean):<br />
![Alt text](https://github.com/wulinjiansheng/Project5-WebGL/blob/master/Pics/Water.bmp)
<br />
<br />
#### Shade based on altitude using the height map
To implement this feature, I mix the user-chosen colors with the original color on land according to the altitude of the land. And here is the result with heightmap based shader:<br />
![Alt text](https://github.com/wulinjiansheng/Project5-WebGL/blob/master/Pics/HeightMap%20Shader.bmp)


Performance Evaluation
-------------------------------------------------------------------------------
Currently, the frame rate counter always shows 60 FPS no matter I enable all the extra effects or not.


Third Party Code
-------------------------------------------------------------------------------
* JavaScript Performance Monitor(https://github.com/mrdoob/stats.js)<br />
I use this to do the Performance Evaluation.


