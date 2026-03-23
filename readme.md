# Blender to Babylon.js exporter

This is an unofficial fork of the [BabylonJS Blender Exporter](https://github.com/BabylonJS/BlenderExporter), updated to work with Blender 4.2+ and Blender 5.x. The upstream project appears to be unmaintained and does not work with modern Blender versions.

## Status

The `dev` branch contains all fixes and is the recommended branch to use. It requires **Blender 4.2.0** or later.

### Fixes on `dev`

- **Blender 4.0+ Principled BSDF compatibility** - Updated all socket name references to match the Blender 4.0 Principled BSDF v2 rework (Subsurface Weight, Specular IOR Level, Coat Weight, Emission Color, etc.). Fixes [#74](https://github.com/BabylonJS/BlenderExporter/issues/74).
- **Export scene custom properties** - Scene-level custom properties are now exported as `"metadata"` in the .babylon file. From [alekop's PR #73](https://github.com/BabylonJS/BlenderExporter/pull/73).
- **Export material custom properties** - Material-level custom properties are now exported as `"metadata"`. From [alekop's commit](https://github.com/alekop/BlenderExporter/commit/cdd201ccd007e086e74fef6d408bf7277c062258).
- **Fix mesh custom properties export** - Custom properties were read from the mesh data block (`bpyMesh.data`) instead of the object (`bpyMesh`), causing all user-set custom properties on mesh objects to be silently dropped.
- **Fix JSON escaping in string properties** - String values containing double quotes (e.g. JSON stored as a custom property) are now properly escaped, preventing invalid JSON output.
- **Support boolean custom properties** - Boolean custom properties were silently dropped during export. Added `bool` type handling (before `int`, since `bool` is a subclass of `int` in Python) to all custom property export paths.
- **Default isPickable to True** - Changed mesh `isPickable` default from `False` to `True` to match the BabylonJS runtime default, so raycasting works out of the box.
- **Fix backFaceCulling export** - Read `backFaceCulling` from Blender's native `use_backface_culling` material setting instead of an unused custom property. Always write it to the output since Blender defaults to double-sided while BabylonJS defaults to single-sided.

## Installation

Copy (or symlink) the `src/babylon_js/` directory into your Blender addons folder:

- **macOS:** `~/Library/Application Support/Blender/<version>/scripts/addons/`
- **Linux:** `~/.config/blender/<version>/scripts/addons/`
- **Windows:** `%APPDATA%\Blender Foundation\Blender\<version>\scripts\addons\`

Then enable the addon in Blender: **Edit > Preferences > Add-ons**, search for "Babylon".

## Documentation
See the [exporters documentation](https://doc.babylonjs.com/extensions/Exporters) to:

- know [how to install](https://doc.babylonjs.com/extensions/Exporters/Blender)
- learn the [features](https://doc.babylonjs.com/extensions/Exporters/Blender#installation)
- read some [tips](https://doc.babylonjs.com/extensions/Exporters/Blender_Tips)

## Changelog

Changelog can be [found here](https://github.com/BabylonJS/BlenderExporter/blob/master/changelog.md).
