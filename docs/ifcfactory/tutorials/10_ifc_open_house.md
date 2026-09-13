# Tutorial: IfcOpenHouse

This page is a **guided walkthrough** of the large example script. Explanations are written here as normal text; **code
** is included from your local checkout
via [pymdown Snippet Sections](https://facelessuser.github.io/pymdown-extensions/extensions/snippets/#snippet-sections) (
`# --8<-- [start:name]` / `[end:name]` in the source file), so blocks stay aligned when lines move.

For the **full script in one block**, see [Example 10 — IfcOpenHouse](../examples/10_ifc_open_house.md).

The upstream reference is the classic IfcOpenShell *IfcOpenHouse* C++ sample. The Python file’s own module docstring
lists patterns (types, openings, booleans, roof). The sections below follow the file from imports through `main`.


## Materials

Named `Material` instances reused by walls, roof, door, glass, terrain, etc.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_materials"
```

---

## Dimensions and constants

Envelope sizes, gable and roof geometry, openings, window frame constant, and the stair **2D profile** (`Polygon`)
extruded later. Inline `#` comments in the snippet are part of the source file.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_constants"
```

---

## Window-type geometry helper

`_frame_bar` and `_openhouse_window_type_geometry` build frame bars and glazed panes for inline `IfcWindowType`
children (all extruded solids so representation types stay valid).

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_window_helper"
```

---

## Door-type geometry helper

Door-section constants and `_openhouse_door_type_geometry` (posts, rail, panel for the east-wall door type).

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_door_helper"
```

---

## `main`: decorated entry point

The `@create_basic_ifc_setup` decorator wires IFC context; `main` receives `model`, `site`, and `building` (the second
positional argument is unused: `_`).

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_main_header"
```

### Step 1 — Footing

Strip footing under the footprint; `Transform` shifts the box so the top sits near grade.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_01_footing"
```

### Step 2 — North wall

Simple `IfcWall` as a single `Box` extrusion.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_02_north_wall"
```

### Step 3 — South wall with openings and windows

Wall body minus two opening voids (`Boolean.Difference`), then two `IfcWindow` elements with inline `IfcWindowType`
geometry.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_03_south_wall"
```

### Step 4 — Gable math and shared solid

Clip normals, eave lines, and `_gable_solid` (extrusion minus two `HalfSpace` cuts) reused by east and west gable walls.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_04_gable_prep"
```

### Step 5 — East gable wall and door

Boolean opening in the gable solid, transforms for world alignment, `IfcDoor` + inline `IfcDoorType`.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_05_east_gable"
```

### Step 6 — West gable wall and window

Same shared `_gable_solid`, different opening and `IfcWindow` placement.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_06_west_gable"
```

### Step 7 — Roof slabs

South and north roof profiles as `Polygon` in (Z, Y), extruded and rotated into world space.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_07_roof"
```

### Step 8 — Stair flight

`STAIR_PROFILE` extruded and rotated; placed at the east end of the building.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_08_stair"
```

### Step 9 — Terrain on site

`numpy` grid, `MeshRepresentation`, attached to `site` with `terrain_mat`.

```python
--8<-- "ifcfactory/examples/10_ifc_open_house.py:tutorial_step_09_terrain"
```

---

