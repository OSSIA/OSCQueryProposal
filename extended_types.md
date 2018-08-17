# EXTENDED_TYPE

## URLs

- `filepath`: string describing a UNC or POSIX file path
- `url`: string representing an URL or URI

## Multi-dimensional types

Following are some accepted values for the EXTENDED_TYPE attribute, for multi-dimensional types, which all use the same notation:
- Characters inside brackets enumerate the various possible values- for example, `position.[rp]` means that you can use `position.r`, and `position.y`.
-  Those types can be used jointly (for all dimensions in the same node) or separately (one or several per node), i.e. it's perfectly fine to have an OSC method that only accepts a single float for a given EXTENDED_TYPE, or any other combination of recognized EXTENDED_TYPE values in any order. A few examples are demonstrating this at the end of the document.


### Position

- `position.[xyz]`- A cartesian point, consisting of any combination of x, y, and z components.
  - `x`- A number value describing a distance.
  - `y`- A number value describing a distance.
  - `z`- A number value describing a distance.
- `position.[rpt]`- A point in space described using polar coordinates
  - `r`- A number value describing the radial distance.
  - `p`- A number value describing the azimuth angle.
  - `t`- A number value describing the inclination angle.

One cartesian coordinate (typically `z`) can be used in lieu of the inclination angle `t`, thus making the coordinate system “cylindrical”

The dimensions names used here for polar coordinates are those suggested by ISO 80000-2:2009/ISO 31-11.


### Orientation

- `orientation.[abcd]`- The orientation of an object described using the quaternion number system, which extends complex numbers , in the form "*a* + *b*i + *c*j + *d*k" where *a*, *b*, *c*, and *d* are real numbers, and i, j, and k are quaternion units.
  - `a`- A number value describing a distance.
  - `b`- A number value describing a distance.
  - `c`- A number value describing a distance.
  - `d`- A number value describing a distance.
- `orientation.[YPR]`- The orientation of an object described using euler angles.
  - `Y`- A number value describing the yaw angle.
  - `P`- A number value describing the pitch angle.
  - `R`- A number value describing the roll angle.
- `orientation.[xyzw]`- The orientation of an object described using an angle (w) relative to the 3-dimensional axis of vector xyz.
  - `x`- A number value describing the x component of the axis vector.
  - `y`- A number value describing the y component of the axis vector.
  - `z`- A number value describing the z component of the axis vector.
  - `w`- A number value describing the angle.

### Color

For all color spaces, an optional alpha channel value can be used:
 	- `a`- A number describing the alpha channel value.

- `color.[rgb]`- A color value described in the RGB color space, potentially including an alpha channel.
  - `r`- A number describing the red channel value.
  - `g`- A number describing the green channel value.
  - `b`- A number describing the blue channel value.
 
- `color.[hsv]`- A color value described in the HSV color space, potentially including an alpha channel.
  - `h`- A number describing the hue value.
  - `s`- A number describing the saturation value.
  - `v`- A number describing the "value" value (not a typo).

- `color.[cmyk]`- A color value described in the CMYK color space, potentially including an alpha channel.
  - `c`- A number describing the cyan value.
  - `m`- A number describing the magenta value.
  - `y`- A number describing the yellow value.
  - `k`- A number describing the black value.

- `color.[XYZ]`- A color value described in the CIE 1931 color space, potentially including an alpha channel.
  - `X`- A number value describing the x tristimulus value.
  - `Y`- A number value describing the y tristimulus value.
  - `Z`- A number value describing the z tristimulus value.


### Examples 

- An example of expressing all cartesian position coordinates in one node:
~~~json
"position": {
	"FULL_PATH": "/color/substractive",
	"TYPE": "fffff”,
	"EXTENDED_TYPE": [
		“color.c”,
		“color.m,
		“color.y”,
		“color.k”,
		“color.a”
	],
}
~~~
- As mentioned above, not all of these attributes are required to be used in the same OSC node - for example, `position.cart.[xyz]` potentially includes `position.cart.x`, `position.cart.y`, and `position.cart.z`, but you don't need to use all of these at the same time.  The following examples are all correct:
~~~json
"2d_position": {
	"FULL_PATH": "/2d_position",
	"TYPE": "ff",
	"EXTENDED_TYPE": [
		"position.x",
		"position.y"
	],
}
~~~
~~~json
"x": {
	"FULL_PATH": "/pos/x",
	"TYPE": "i",
	"EXTENDED_TYPE": "position.x"
},
"funky_2D": {
	"FULL_PATH": "/pos/funky_2D",
	"TYPE": "ff",
	"EXTENDED_TYPE": [ "position.z", "position.y" ]
}
~~~
