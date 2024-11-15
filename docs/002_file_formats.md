Supported file formats
===========================================================================

Scenes
---------------------------------------------------------------------------

### JSON
**ZeroZero** have its own JSON format for describing a scene with resources (glTF ou ZScene files),
meshes references linked to resources and the scene's nodes and their properties.<br>
The simplest way of creating JSON scene files is to use the [Blender Add-on](003_blender_add_on.md).
A JSON scene can be loaded with \ref z0::Loader::addScene.


### glTF
The \ref z0::GlTF class can load glTF 2.0 files containing nodes, meshes, materials and textures with \ref z0::Loader::load.<br>
The glTF support is mainly provided as a development tool since Blender can directly export 
a scene in JSON+GLB scene file format via the [Blender Add-on](003_blender_add_on.md).
During the creation phase, scene hot-reload can easily be implemented with \ref z0::Node::removeAllChildren and 
\ref z0::Loader::addScene or \ref z0::Loader::load.<br>
**Note** that the glTF loader is not optimized : all resources are loaded in CPU memory before processing,
images are decompressed from JPEG/PNG formats in CPU memory then uploaded into VRAM uncompressed.

### ZScene
The \ref z0::ZScene class can load files in the ZeroZero's ZScene file format with \ref z0::Loader::load.<br>
It's a binary file format created to allow textures to be loaded directly into VRAM in
BCn compressed formats, decreasing both the loading times and the VRAM usage.<br>
The `gltf2zscene` (`src/tools/gltf2zscene`) tools can be used to convert
glTF files to ZScene files.<br>
Since ZScene files can be used as resources files in the JSON scenes files, glTF and Zscene files can be interchanged without modifying code or JSON scene files 
(except from the file name extension), allowing the use of glTF files during the creation phase
and the ZScene files in the releases. 

Images
---------------------------------------------------------------------------

**ZeroZero** supports the following file formats when using the \ref z0::Image::load function :
- JPEG and PNG (others formats can be activated in `src/z0/libraries.cpp`)
- DDS with compressed images
- ~~KTX2 with compressed images~~ (currently deactivated until we add an option in `CMakeLists.txt`)
