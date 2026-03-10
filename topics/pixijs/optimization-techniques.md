# Optimization techniques

## Resource based

- **Minification and Compression:** Compressing js and assets like images and audio
- **Sprite Sheets and Texture Atlases:** Instead of loading individual images, pack multiple images into sprite sheets or texture atlases. Sprite sheets (arranged in a grid-like fashion) are often used for simple animations and individual frames of animation (each image or sprite is packed tightly together without any gaps, and each sprite is associated with metadata), while texture atlases are more commonly used for managing large collections of sprites or textures efficiently
- **Caching:** Utilize browser caching to store assets locally, reducing load times
- **Lazy Loading:** Load assets and resources only when they are needed
- **Object Pooling:** Reuse objects (such as bullets, enemies, or particles) instead of creating and destroying them frequently. This reduces memory allocation and garbage collection overhead.
- **Optimized Asset Formats:** Choose the most appropriate file formats for your assets. For example, use WebP for images and WebM for videos to take advantage of modern browser support and better compression
- **Unused assets removing:** PixiJS objects, such as textures, meshes, and other GPU-backed data, hold references that consume memory. To explicitly release these resources, call the `destroy` method on objects you no longer need. This ensures that the object’s GPU resources are freed immediately, reducing the likelihood of memory leaks and improving performance. In cases where PixiJS’s automatic texture garbage collection is insufficient, you can manually unload textures from the GPU using `texture.unload()`


## Code based:

- **GPU Acceleration:** Libraries like WebGL and Three.js provide access to the GPU for rendering 3D graphics efficiently
- **Optimized Loops:** Use efficient looping techniques, such as iterating backwards over arrays and caching array lengths, to minimize loop overhead
- **Debouncing and Throttling:** Limit the frequency of certain operations, like resizing the window or processing user input, to prevent performance bottlenecks.
- **Offloading Processing:** Move intensive calculations or tasks to web workers to avoid blocking the main thread, thus keeping the UI responsive
- **Performance Profiling:** Use browser developer tools to profile your game's performance and identify areas for improvement
