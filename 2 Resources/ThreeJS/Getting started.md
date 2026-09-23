![628](https://threejs.org/manual/resources/images/threejs-structure.svg)

An three.js ap requires that you create a bunch of objects and connect them together.
It is often confused with WebGL, but WebGL is low level system that only draws points, lines and triangles,that is where three.js comes handy.

Important elements:

#renderer - main object, you pass in a #scene and #camera and it renders (draws) the portion of the 3D scene that is inside the #frustum of the camera as a 2D image to a canvas.

#scene - defines the root of the #scenegraph and contains properties like the background color and fog.  These objects define a hierarchical parent/child tree like structure and represent where objects appear and how they are oriented.

#mesh - representation of a specific #geometry with a specific #material

#geometry objects represent the vertex data of different geometries like sphere, cube etc

#material objects represent the surface properties used to draw #geometry including color and how shiny it is, it can reference one or more #texture objects which can be used to wrap and image onto the surface of a #geometry

#light

#near and #far in the PerspectiveCamera() settings represent the space in front of the camera that will be rendered. Anything before that range or after that range will be clipped (not drawn).

#frustum - fov, aspect, near and far settings define a _"frustum"_. A _frustum_ is the name of a 3d shape that is like a pyramid with the tip sliced off. In other words think of the word "frustum" as another 3D shape like sphere, cube, prism, frustum.

![366](https://threejs.org/manual/resources/frustum-3d.svg)

Anything inside the defined frustum will be drawn. Anything outside will not.

Everything is triangular!!!

![[Screenshot 2026-09-18 at 12.44.43.png]]

**The less subdivisions you choose the more likely things will run smoothly and the less memory they'll take.**