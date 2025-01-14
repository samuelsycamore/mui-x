# Data Grid - Cells

<p class="description">Learn how to customize the rendered elements and values of a cell.</p>

## Customizing cells

The Data Grid provides several methods to customize the rendered elements and values of a cell.
Each of them has a different purpose and should be used in different situations.
Here is a summary of their differences:

### renderCell() function

The `renderCell()` function is the most powerful way to customize the content of a cell.
It allows you to render anything you want inside the cell.
It is the only way to render a React component inside a cell.
It is also the only way to customize the cell's behavior (for instance, add a click handler).
It is the most flexible way to customize a cell, but it is also the most expensive one.
It should be used only when the other options are not enough.

Here's an example for a cell that displays a button:

```tsx
const columns: GridColDef[] = [
  {
    field: 'date',
    headerName: 'Year',
    renderCell: (params: GridRenderCellParams<any, Date>) => (
      <strong>
        {params.value.getFullYear()}
        <Button
          variant="contained"
          size="small"
          style={{ marginLeft: 16 }}
          tabIndex={params.hasFocus ? 0 : -1}
        >
          Open
        </Button>
      </strong>
    ),
  },
];
```

See more about the `renderCell` function in [Column definition—rendering cells](/x/react-data-grid/column-definition/#rendering-cells).

### valueGetter() function

The `valueGetter()` function allows you to derive the cell value from the row data.
It is the most performant way to customize the cell content.
It is also the only way to customize the cell value without changing the row data.
It should be used when you need to derive the cell value from the row data. Common use cases are:

- Transforming the value (for example convert a decimal value to a percentage value)
- Deriving the value from multiple fields (for example concatenating first name and last name)
- Deriving the value from a nested field (for example `user.address.city`)

This value is also used internally in the Grid to filter, sort, and render (if no `renderCell` or `valueFormatter` is provided).
You can learn more about it in [Column definition—value getter](/x/react-data-grid/column-definition/#value-getter).

### valueFormatter() function

The `valueFormatter()` function allows you to format the cell value.
It could be used to customize the cell value without changing the row data.
It should be used when you need to format the cell value.

A few common use cases are:

- Formatting a date to a custom display format
- Formatting a decimal value to percentage and show `%` sign
- Formatting a boolean value to `Yes` or `No`

It only impacts the rendering part and does not impact the internal calculations like filtering or sorting.
Learn more in [Column definition—value formatter](/x/react-data-grid/column-definition/#value-formatter).