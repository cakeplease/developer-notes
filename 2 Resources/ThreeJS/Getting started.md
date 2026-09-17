![628](https://threejs.org/manual/resources/images/threejs-structure.svg)

An three.js ap requires that you create a bunch of objects and connect them together.
It is often confused with WebGL, but WebGL is low level system that only draws points, lines and triangles,that is where three.js comes handy.

Important elements:

#renderer - main object, you pass in a #scene and #camera and it renders (draws) the portion of the 3D scene that is inside the frustum of the camera as a 2D image to a canvas.

#scene - defines the root of the #scenegraph and contains properties like the background color and fog.  These objects define a hierarchical parent/child tree like structure and represent where objects appear and how they are oriented.

#mesh - representation of a specific #geometry with a specific #material