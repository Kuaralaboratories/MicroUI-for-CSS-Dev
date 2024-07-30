# MicroUI for CSS Developers

Creating a layout similar to CSS in C++ using MicroUI involves utilizing the layout functions provided by MicroUI. These functions allow you to define rows and columns to position elements accordingly. Below, I'll outline the steps and provide example code to create a layout similar to what you might achieve with CSS.

### 1. Using `mu_layout_row`

To create a row-based layout similar to `flex-direction: row` in CSS, you can use `mu_layout_row`.

```c
mu_layout_row(ctx, 3, (int[]) { 50, 100, -1 }, 0);
```

Parameters:
- The first parameter is the context (`ctx`).
- The second parameter is the number of columns in the row.
- The third parameter is an array defining the widths of the columns (`50`, `100`, `-1`). `-1` means the column will take up the remaining space.
- The fourth parameter is the height of the row.

### 2. Using `mu_layout_begin_column` and `mu_layout_end_column`

To create a column-based layout similar to `flex-direction: column` in CSS, you can use `mu_layout_begin_column` and `mu_layout_end_column`.

```c
mu_layout_begin_column(ctx);
mu_layout_row(ctx, 1, (int[]) { -1 }, 0);
mu_label(ctx, "Label 1");
mu_label(ctx, "Label 2");
mu_layout_end_column(ctx);
```

These functions create a nested column layout.

### 3. Combining `mu_layout_row` and `mu_layout_column`

You can combine row and column layouts to create complex layouts.

### Example Code

Below is an example of a simple layout inside a window.

```c
static void layout_example(mu_Context *ctx) {
  if (mu_begin_window(ctx, "Layout Example", mu_rect(50, 50, 400, 300))) {
    
    // Row-based layout
    mu_layout_row(ctx, 3, (int[]) { 50, 100, -1 }, 25);
    mu_label(ctx, "Left");
    mu_button(ctx, "Center");
    mu_textbox(ctx, buffer, sizeof(buffer));
    
    // Column-based layout
    mu_layout_begin_column(ctx);
    mu_layout_row(ctx, 1, (int[]) { -1 }, 25);
    mu_label(ctx, "Column 1");
    mu_label(ctx, "Column 2");
    mu_layout_end_column(ctx);

    mu_end_window(ctx);
  }
}
```

In this example:
- A window is created (`mu_begin_window`).
- A row layout is defined using `mu_layout_row`. This row has three columns with specified widths: one 50 pixels wide, one 100 pixels wide, and the third taking up the remaining space.
- A column layout is defined using `mu_layout_begin_column` and `mu_layout_end_column`. Inside this column, there are two labels.

### General Structure

To create a CSS-like layout in MicroUI, use the above layout functions to define the structure. Use `-1` for flexible widths to ensure elements take up the remaining space. By combining these layout functions, you can design complex and user-friendly interfaces.

You can adapt these structures to suit your project needs and create more detailed layouts as required.
