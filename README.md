# turtlePlus

| English | [简体中文](./README_zh.md) |
| ------- | -------------------------- |

------

## Features

### 1. Move Forward

Like turtle, the `fd` function is used to move the cursor and draw in a specified way. It is fully compatible with turtle and adds many new features.

- In turtle, line style control relies entirely on manually using `penup` and `pendown`. turtlePlus encapsulates this into commonly used modes: `LineModes.none`, `LineModes.solid`, and `LineModes.dotted`, representing no line (pen up), solid line, and dashed line. Of course, you can still use `penup` and similar methods for precise control.
- In simple GUI demonstrations, it is often necessary to label points. turtle natively supports marking points and writing text at stopping positions.

Function parameters and their meanings:

```
fd(length,
    line_width=DEFAULT.LINE_WIDTH,
    line_color=Colors.black, 
    line_mode=LineModes.solid,
    
    write_name="", name_align=Align.LEFT,
    name_vertical_align=VerticalAlign.TOP,

    if_dot_at_end=True,
    dot_color=Colors.black, 
    dot_diameter=DEFAULT.DOT_DIAMETER,
    dotted_line_length=DEFAULT.DOTTED_LINE_LENGTH,
    dotted_gap=DEFAULT.DOTTED_GAP
)
```

- `length` **[required]**: Distance to move forward.
- `line_width`: Width of the line drawn along the path.
- `line_color`: Color of the line.
- `line_mode`: Line style. Built-in options include solid, dotted, and none (no drawing).
- `write_name`: Whether to label the endpoint. Default is no label.
- `name_align`: Horizontal alignment of the label (default: left).
- `name_vertical_align`: Vertical alignment of the label (default: top).
- `if_dot_at_end`: Whether to draw a dot at the endpoint (default: true).
- `dot_color`: Color of the endpoint dot.
- `dot_diameter`: Radius of the endpoint dot.
- `dotted_line_length`: Length of each dash in a dotted line.
- `dotted_gap`: Gap between dashes.

------

### 2. Go to a Coordinate

You can use the `goto` function to move the cursor to a specified coordinate and draw.

Like `fd`, it supports many additional features.

```
goto(target_point,
     line_mode,
     line_width,
     line_color,
     
     write_name, name_height=DEFAULT.FONT_HEIGHT,
     name_align=Align.LEFT, name_vertical_align=VerticalAlign.TOP,
     name_color=DEFAULT.FONT_COLOR,
     
     if_dot_at_end=True, dot_color=Colors.black,
     dot_diameter=DEFAULT.DOT_DIAMETER,
     dotted_line_length=DEFAULT.DOTTED_LINE_LENGTH,
     dotted_gap=DEFAULT.DOTTED_GAP
)
```

- `target_point`: Target coordinate, a list in the form `[x, y]`.
- `line_width`: Width of the drawn line.
- `line_color`: Color of the line.
- `line_mode`: Line style (solid, dotted, or none).
- `write_name`: Whether to label the endpoint (default: no label).
- `name_height`: Font size of the label.
- `name_align`: Horizontal alignment (default: left).
- `name_vertical_align`: Vertical alignment (default: top).
- `name_color`: Font color.
- `if_dot_at_end`: Whether to draw a dot at the endpoint (default: true).
- `dot_color`: Color of the dot.
- `dot_diameter`: Radius of the dot.
- `dotted_line_length`: Length of each dash.
- `dotted_gap`: Gap between dashes.

------

### 3. Draw Text

The `write` function is used to render text in the drawing, for example to create diagrams like this:

<img src="./assets/image-20260323022253130.png" alt="image-20260323022253130" style="zoom: 25%;" />

Function parameters:

```
write(string,
      pos=None,
      align=Align.LEFT,
      vertical_align=DEFAULT.FONT_VERTICAL_ALIGN,
      font_height=DEFAULT.FONT_HEIGHT,
      font_color=DEFAULT.FONT_COLOR,
      font_family=DEFAULT.FONT_FAMILY,
      font_weight=DEFAULT.FONT_WEIGHT)
```

- `string`: Text to draw.
- `pos`: Position to draw the text.
- `align`: Horizontal alignment.
- `vertical_align`: Vertical alignment.
- `font_height`: Font size.
- `font_color`: Font color.
- `font_family`: Font family.
- `font_weight`: Font weight.

------

### 4. Scale Viewport

Since the size of drawings may not match screen resolution, turtle drawings may appear too large (overflowing the screen) or too small (hard to see). turtlePlus introduces viewport scaling to solve this issue.

Use the `set_scale()` function to scale the viewport.

```
set_scale(scale_value)
```

- `scale_value`: Scaling factor (must be greater than 0).

------

### 5. Auto Scaling

turtlePlus provides automatic scaling. By passing all points of the drawing, it calculates an appropriate scale so the figure fits the screen without manual adjustment.

```
auto_scaling(points_pos)
```

- `points_pos`: Coordinates of all points in the drawing.

The left image shows no scaling; the right shows scaling applied.

<img src="./assets/image-20260323024230638.png" style="zoom:25%;" />   <img src="./assets/image-20260323024249044.png" style="zoom:25%;" />

------

### 6. Calculate Distance

Calculates the distance between coordinates using the Pythagorean theorem.

⚠️ Not redundant — this function supports special coordinate formats and accounts for viewport scaling.

```
distance(point_1, point_2)
```

- `point_1`, `point_2`: The two coordinates.

------

### 7. Auto Offset Viewport

Sometimes drawings are not centered due to their shape, resulting in poor visual appearance. turtlePlus introduces viewport offset to fix this.

Use the `auto_offset` function to adjust the viewport.

```
auto_offset(points_pos, offset_mode)
```

- `points_pos`: All points of the drawing.
- `offset_mode`: Offset mode:
  - `Offset.at_start`: Center on the starting point
  - `Offset.center`: Center on the geometric center
  - `Offset.none`: No offset

For example, using `auto_offset(points, Offset.center)` centers the drawing:

<img src="./assets/image-20260323025337038.png" style="zoom:25%;" />   <img src="./assets/image-20260323025346619.png" style="zoom:25%;" />

------

### 8. Ensure Best Appearance

Automatically handles both viewport offset and scaling to achieve the best display.

```
ensure_appearance(points_pos, offset_mode=OffsetMode.none)
```

- `points_pos`: Points of the drawing
- `offset_mode`: Viewport offset mode

This function combines `auto_scaling` and `auto_offset` for optimal display.

<img src="./assets/image-20260323025421851.png" style="zoom:25%;" />