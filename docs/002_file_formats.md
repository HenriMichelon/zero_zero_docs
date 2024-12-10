Supported file formats
===========================================================================

Resources
---------------------------------------------------------------------------
Scenes resources such as meshes and their vertices, materials, textures, images, ...
can be loaded by ZeroZero from glTF or ZRes files.
They are generally loaded automatically by the scene loader when a resource JSON file 
is included in a JSON scene file.

### glTF
The glTF 2.0 support is mainly provided as a development tool since Blender can directly export
them with the [Blender Add-on](003_blender_add_on.md).<br>
**Note** that the glTF loader is not optimized : all resources are loaded in CPU memory before processing,
images are decompressed from JPEG/PNG formats in CPU memory then uploaded into VRAM uncompressed.

### ZRes
The binary ZRes file format is designed to allow textures images to be loaded directly into VRAM in
one big image atlas and in BCn compressed formats, decreasing both the loading times and the VRAM usage.<br>
The `gltf2zres` tools can be used to convert glTF files to ZRes files, including from
the [Blender Add-on](003_blender_add_on.md).

### JSON
The JSON format is used to describe the content of a glTF or a ZRes file when used in a scene.
It's an intermediary description format to allow the loading of a JSON scene file without
scanning the content of a resource file to search for meshes.<br>
They are created manually or with the [Blender Add-on](003_blender_add_on.md) when
exporting a Blender scene as a resource file.

Scenes
---------------------------------------------------------------------------

### JSON
ZeroZero have its own JSON format for describing a scene with or linked with resources (glTF ou ZRes files), 
the scene tree and the nodes and their properties.<br>
The simplest way of creating JSON scene files is to use the [Blender Add-on](003_blender_add_on.md).<br>
A JSON scene is added to an existing node with \ref z0::Loader::load. 
Scene hot-reload can easily be implemented by combining \ref z0::Node::removeAllChildren and \ref z0::Loader::load.

### glTF
Since the glTF format also contains a scene tree and nodes descriptions it can also be used
to load an entire scene with \ref z0::Loader::load.

### ZRes
Like the glTF format the ZRes format also contains a scene tree and nodes descriptions and can also be used
to load an entire scene with \ref z0::Loader::load.

Images
---------------------------------------------------------------------------

**ZeroZero** supports the following file formats when using the \ref z0::Image::load function :
- JPEG and PNG (others formats can be activated in `src/z0/libraries.cpp`)
- DDS with compressed images
- ~~KTX2 with compressed images~~ (currently deactivated until we add an option in `CMakeLists.txt`)
