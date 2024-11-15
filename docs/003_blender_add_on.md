Blender Add-on
===========================================================================

Since **ZeroZero** does not have an editor a Blender add-on is provided
to edit ZeroZero properties of scenes nodes and export a Blender scene
to a ZeroZero JSON+GLB or JSON+ZSCENE scene.<br>

Installation
------------------------------------------------------------------------
The add-on support Blender 4.2 and newer version.<br>
- Open the "Edit" -> "Preferences" dialog
- Click on the "Add-ons" tab
- Open the pop-up menu with the top-right "down arrow" icon
- Click "Install from Disk..."
- Select the python file `src/tools/blender/blender_zero_zero.py`

How to use
------------------------------------------------------------------------

Once installed the add-on add properties to the Blender's scene 
and the Blender's nodes.

### Scene properties
The ZeroZero scene properties are located in the *ZeroZero project* section
of the Blender scene properties :
![ZeroZero Scene properties](images/blender_add_on_scene.png)
<br>

The following properties can be edited :
- *Project* : the game/project root directory 
- *Scene* : the scene resource directory, relative to the project directory
- *Models* : the models resource directory, relative to the project directory
- *Export to ZScene* : convert the exported GLB file to a ZScene file then delete the GLB
- *gltf2zscene* : the directory of the gltf2zscene executable
- *Format* : compression format for color textures 
- *Threads* : number of threads for image conversion with gltf2zscene (0 = auto)
<br>

The *Export as ZeroZero scene* button exports the Blender scene in JSON+GLB format.<br> 
If the *Export to ZScene* option is activated, 
the GLB file is converted into a ZScene file then deleted. 
Refers to [File formats](002_file_formats.md) for the description of the file formats. 

### Nodes properties

#### All nodes
The ZeroZero node properties are located in the *ZeroZero Node* section
of the Blender node properties :
![ZeroZero Node properties](images/blender_add_on_node.png)
<br>

Here you can change the node class with a ZeroZero built-in class or
input a custom class name (must be registered with the `Z0_REGISTER_TYPE`macro in the game).<br>

You can add a property with the *Add Custom Property* button. 
Each property must have a *Name* and a *Value*. The variable `$$` can be used in the *Value* field to refer to the selected node name.
This properties must be supported by the `setProperty` function of the
corresponding class (including inheritance).
<br>

The following objects properties are exported in the GLB or ZScene file, you don't have to add them :
- *position*
- *rotation*
- *scale*

#### Lights nodes
You can create lights in the ZeroZero scene using empty nodes (see below)
but you can also create them with Blender lights object.<br>
All Blender light object are automatically converted to ZeroZero \ref z0::Light nodes.
The following blender properties are used during the export :
- *color*
- *position*
- *rotation*
- *Light type* : Point -> \ref z0::OmniLight, Sun -> \ref z0::DirectionalLight, Spot -> \ref z0::SpotLight
- *Shadow* : \ref z0::Light::setCastShadows()
- *Custom Distance*, *Distance* : \ref z0::OmniLight::setRange()
- *Beam Shape*, *Size* : \ref z0::SpotLight::setFov()

#### Empty nodes
You can add *Empty*, *Plain axes* nodes in blender to add any ZeroZero node in 
the final scene.<br>
Example for a \ref z0::Environment node :<br>
![Environement node](images/blender_add_on_empty.png)