# Automated Inventory Reordering System

## Workflow

`Main.xaml` reads the `Inventory` worksheet from an Excel workbook, identifies rows where `CurrentStock <= ReorderPoint`, calculates `ReorderQuantity = TargetStock - CurrentStock`, and writes purchase requests to `PurchaseRequests.xlsx` on the `PurchaseRequests` worksheet.

## Input workbook

Create `Inventory.xlsx` in the project folder, or pass a different path through the `in_InventoryFile` workflow argument. The workbook must contain a sheet named `Inventory` with these headers:

- `SKU`
- `ItemName`
- `Supplier`
- `CurrentStock`
- `ReorderPoint`
- `TargetStock`

`Inventory_Sample.csv` contains example data that can be copied into the workbook.

## Output

The workflow creates `PurchaseRequests.xlsx` in the project folder and returns its path through `out_PurchaseRequestFile`. The output columns are SKU, item name, supplier, current stock, reorder point, target stock, reorder quantity, request date, and status.

## Reorder rule

A purchase request is generated when current stock is less than or equal to the reorder point. The requested quantity raises stock to the target stock level.

## Run

Run `Main.xaml` from UiPath Studio. For unattended use, place the source workbook in a stable Orchestrator Storage Bucket or configure the workflow argument to a controlled network/local path.
