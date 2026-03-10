# Common terms used in Pixi.js and across web game dev

### Texture 
Represents image data (GPU resource reference). Usually created from: BaseTexture, Image, or Spritesheet frame. Can represent a full image, or a sub-rectangle of atlas. Lightweight descriptor, not renderable by itself. Texture is GPU-bound data. Think: **"what to draw"**

### Sprite 
Sprite is a displayObject, eenderable entity placed on stage. Has transform (position, scale, rotation, anchor, alpha). Holds a reference to a Texture. Sprite is scene graph node. Think: **"how and where to draw it"**

### Particle
Particles are a fundamental component in game development that are often implemented as **lightweight, animated sprites that simulate the behavior of small, independent entities**. Used to create a wide range of effects such as smoke, fire, explosions, rain, snow, and magical spells. 
Performance Considerations: Particle systems can be computationally expensive when dealing with a large number of particles. Optimize it with sprite batching, object pooling, and GPU acceleration


### Mesh
Mesh in PixiJS is a low-level renderable object using custom geometry and shaders.
- Sprite is a specialized mesh for textured quads.
- Use Mesh when you need non-rectangular geometry or custom GPU effects.
- It gives control over vertices, UVs, indices, and shader logic.

A mesh is a low-level rendering primitive composed of:
- Geometry: Vertex positions, UVs, indices, and other attributes
- Shader: A GPU program that defines how the geometry is rendered
- State: GPU state configuration (e.g. blending, depth, stencil)

With these elements, you can build anything from simple quads to curved surfaces and procedural effects.

All meshes in PixiJS are built using the MeshGeometry class. This class allows you to define the vertex positions, UV coordinates, and indices that describe the mesh's shape and texture mapping.

### Draw Call 
Is a command sent from the CPU to the GPU to render a specific object or group of objects onto the screen (sprites, text, shapes, etc). Draw calls are often executed within a game/rendering loop, where engine iterates through all the objects that need to be rendered and issues draw calls for each of them.
Efficient management of draw calls is crucial for performance optimization in games and graphics-heavy applications. Minimizing the number of draw calls, by, for example, batching together similar objects, can significantly improve performance, as excessive draw calls can lead to increased CPU and GPU overhead. Both Phaser and PixiJS provide mechanisms for optimizing draw calls, such as **sprite batching** and **using texture atlases** to reduce the number of texture swaps.

