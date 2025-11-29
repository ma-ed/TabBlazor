# TabBlazor AI Agent Instructions

TabBlazor is a Blazor implementation of the Tabler UI framework (tabler.io). This document provides comprehensive instructions for AI agents to create user interfaces using TabBlazor components.

## Table of Contents

- [Getting Started](#getting-started)
- [Project Setup](#project-setup)
- [Layout Components](#layout-components)
- [UI Components](#ui-components)
- [Form Components](#form-components)
- [Data Components](#data-components)
- [Services](#services)
- [Colors and Theming](#colors-and-theming)
- [Common Patterns](#common-patterns)
- [Complete Examples](#complete-examples)

---

## Getting Started

### Installation

Add TabBlazor to your project via NuGet:

```bash
dotnet add package TabBlazor
```

### Required CSS and JavaScript

Add these references to your `_Host.cshtml` (Server) or `index.html` (WebAssembly):

```html
<!-- Tabler CSS -->
<link rel="stylesheet" href="https://unpkg.com/@tabler/core@1.4.0/dist/css/tabler.min.css">

<!-- TabBlazor CSS -->
<link rel="stylesheet" href="_content/TabBlazor/css/tabblazor.min.css" />

<!-- TabBlazor JavaScript -->
<script src="_content/TabBlazor/js/tabblazor.js"></script>
```

### Service Registration

In `Program.cs` or `Startup.cs`, register TabBlazor services:

```csharp
using TabBlazor;

// In ConfigureServices or builder.Services
services.AddTabler();
// Or with options:
services.AddTabBlazor(options => {
    // Configure options here
});
```

### Required Imports

Add to `_Imports.razor`:

```razor
@using TabBlazor
@using TabBlazor.Services
```

### Layout Setup

Your main layout should include container components for modals, toasts, and offcanvas:

```razor
@inherits LayoutComponentBase

<ModalContainer />
<ToastContainer />
<OffcanvasContainer />

<div class="page">
    @Body
</div>
```

---

## Layout Components

### Row and RowCol (Grid System)

Create responsive grid layouts:

```razor
<Row>
    <RowCol Md="6" Lg="4">
        <!-- Content for first column -->
    </RowCol>
    <RowCol Md="6" Lg="4">
        <!-- Content for second column -->
    </RowCol>
    <RowCol Md="12" Lg="4">
        <!-- Content for third column -->
    </RowCol>
</Row>

<!-- Row with cards -->
<Row HasCards>
    <RowCol Sm="6" Lg="3">
        <Card>Card content</Card>
    </RowCol>
</Row>
```

**RowCol Parameters:**
- `Columns` (int): Base column width (1-12)
- `Xs`, `Sm`, `Md`, `Lg`, `Xl`, `XXl` (int): Responsive breakpoint widths
- `Auto` (bool): Auto-width column

### Navbar

Create navigation bars:

```razor
<Navbar Background="NavbarBackground.Dark" Direction="NavbarDirection.Horizontal">
    <a href="/" class="navbar-brand">
        <img src="logo.png" alt="Logo" class="navbar-brand-image">
        My App
    </a>
    
    <NavbarMenu>
        <NavbarMenuItem Href="/" Text="Home">
            <MenuItemIcon>
                <Icon IconType="@TablerIcons.Home" />
            </MenuItemIcon>
        </NavbarMenuItem>
        
        <NavbarMenuItem Text="Settings">
            <MenuItemIcon>
                <Icon IconType="@TablerIcons.Settings" />
            </MenuItemIcon>
            <SubMenu>
                <NavbarMenuItem Href="/settings/profile" Text="Profile" />
                <NavbarMenuItem Href="/settings/account" Text="Account" />
            </SubMenu>
        </NavbarMenuItem>
    </NavbarMenu>
</Navbar>
```

**Navbar Parameters:**
- `Background`: `NavbarBackground.Dark`, `NavbarBackground.Light`, `NavbarBackground.Transparent`
- `Direction`: `NavbarDirection.Horizontal`, `NavbarDirection.Vertical`
- `NavLinkMatch`: Controls active link matching

### Navigation (Sidebar)

```razor
<Navigation>
    <NavigationItem Text="Dashboard" Href="/dashboard">
        <Icon IconType="@TablerIcons.Dashboard" />
    </NavigationItem>
    <NavigationItem Text="Users" Href="/users">
        <Icon IconType="@TablerIcons.Users" />
    </NavigationItem>
</Navigation>
```

---

## UI Components

### Button

```razor
<!-- Basic buttons -->
<Button Text="Primary" BackgroundColor="TablerColor.Primary" />
<Button Text="Success" BackgroundColor="TablerColor.Success" />
<Button Text="Danger" BackgroundColor="TablerColor.Danger" />

<!-- Button types -->
<Button Type="ButtonType.Button" Text="Button" />
<Button Type="ButtonType.Submit" Text="Submit" />
<Button Type="ButtonType.Link" Text="Link" LinkTo="/page" />

<!-- Button sizes -->
<Button Size="ButtonSize.Small" Text="Small" />
<Button Size="ButtonSize.Large" Text="Large" />

<!-- Button shapes -->
<Button Shape="ButtonShape.Pill" Text="Pill" />
<Button Shape="ButtonShape.Square" Text="Square" />

<!-- Button states -->
<Button Disabled="true" Text="Disabled" />
<Button IsLoading="true" Text="Loading" />

<!-- Icon button -->
<Button IsIcon="true" BackgroundColor="TablerColor.Primary">
    <Icon IconType="@TablerIcons.Plus" />
</Button>

<!-- Button with click handler -->
<Button BackgroundColor="TablerColor.Primary" @onclick="HandleClick" Text="Click Me" />

<!-- Outline and ghost styles -->
<Button BackgroundColor="TablerColor.Primary" BackgroundColorType="ColorType.Outline" Text="Outline" />
<Button BackgroundColor="TablerColor.Primary" BackgroundColorType="ColorType.Ghost" Text="Ghost" />
```

**Button Parameters:**
- `Text` (string): Button text
- `BackgroundColor` (TablerColor): Button color
- `BackgroundColorType` (ColorType): `Default`, `Outline`, `Ghost`
- `Size` (ButtonSize): `Default`, `Small`, `Large`
- `Shape` (ButtonShape): `Default`, `Square`, `Pill`
- `Type` (ButtonType): `Button`, `Submit`, `Reset`, `Link`, `Input`
- `Disabled`, `IsLoading`, `IsIcon`, `Block` (bool)
- `LinkTo` (string): URL for link buttons

### ButtonList

Group buttons together:

```razor
<ButtonList>
    <Button Text="Save" BackgroundColor="TablerColor.Primary" />
    <Button Text="Cancel" BackgroundColor="TablerColor.Secondary" />
</ButtonList>
```

### Card

```razor
<!-- Basic card -->
<Card>
    <CardHeader>
        <CardTitle>Card Title</CardTitle>
    </CardHeader>
    <CardBody>
        Card content goes here
    </CardBody>
    <CardFooter>
        <Button Text="Action" BackgroundColor="TablerColor.Primary" />
    </CardFooter>
</Card>

<!-- Card with status -->
<Card StatusTop="TablerColor.Primary">
    <CardBody>Card with top status</CardBody>
</Card>

<Card StatusStart="TablerColor.Success">
    <CardBody>Card with left status</CardBody>
</Card>

<!-- Card sizes -->
<Card Size="CardSize.Small">Small card</Card>
<Card Size="CardSize.Medium">Medium card</Card>
<Card Size="CardSize.Large">Large card</Card>

<!-- Stacked cards -->
<Card Stacked>Stacked card effect</Card>

<!-- Card as link -->
<Card LinkTo="/details">Clickable card</Card>
```

**Card Parameters:**
- `Size` (CardSize): `Default`, `Small`, `Medium`, `Large`
- `Stacked` (bool): Stacked card effect
- `StatusTop`, `StatusStart` (TablerColor): Status indicator color
- `LinkTo` (string): Makes card a link

### Alert

```razor
<Alert BackgroundColor="TablerColor.Success" Title="Success!">
    Operation completed successfully.
</Alert>

<Alert BackgroundColor="TablerColor.Warning" Title="Warning" Dismissible>
    This is a dismissible warning alert.
</Alert>

<Alert BackgroundColor="TablerColor.Danger" Title="Error" Important>
    This is an important error alert.
</Alert>
```

**Alert Parameters:**
- `BackgroundColor` (TablerColor): Alert color
- `Title` (string): Alert title
- `Dismissible` (bool): Can be dismissed
- `Important` (bool): Important style

### Badge

```razor
<Badge BackgroundColor="TablerColor.Primary">Primary</Badge>
<Badge BackgroundColor="TablerColor.Success" Shape="BadgeShape.Pill">Pill</Badge>
<Badge BackgroundColor="TablerColor.Warning" BadgeType="BadgeType.Light">Light</Badge>
<Badge BackgroundColor="TablerColor.Danger" BadgeType="BadgeType.Outline">Outline</Badge>

<!-- Notification badge -->
<Badge BackgroundColor="TablerColor.Red" Notification>5</Badge>

<!-- Blinking badge -->
<Badge BackgroundColor="TablerColor.Green" Blink />
```

**Badge Parameters:**
- `BackgroundColor` (TablerColor): Badge color
- `Shape` (BadgeShape): `Default`, `Pill`
- `BadgeType` (BadgeType): `Default`, `Light`, `Outline`
- `Size` (BadgeSize): `Default`, `Large`
- `Notification`, `Blink` (bool)

### Avatar

```razor
<Avatar Data="https://example.com/avatar.jpg" />
<Avatar Size="AvatarSize.Large" BackgroundColor="TablerColor.Primary">JD</Avatar>

<!-- Avatar sizes -->
<Avatar Size="AvatarSize.Small">S</Avatar>
<Avatar Size="AvatarSize.Medium">M</Avatar>
<Avatar Size="AvatarSize.Large">L</Avatar>
<Avatar Size="AvatarSize.ExtraLarge">XL</Avatar>

<!-- Avatar shapes -->
<Avatar Rounded="AvatarRounded.Circle">AB</Avatar>
<Avatar Rounded="AvatarRounded.Rounded">CD</Avatar>
```

**Avatar Parameters:**
- `Data` (string): Image URL
- `Size` (AvatarSize): `Default`, `Small`, `Medium`, `Large`, `ExtraLarge`
- `Rounded` (AvatarRounded): `Default`, `Rounded`, `RoundedSmall`, `RoundedLarge`, `Circle`, `None`
- `BackgroundColor` (TablerColor)

### AvatarList

```razor
<AvatarList>
    <Avatar Data="avatar1.jpg" />
    <Avatar Data="avatar2.jpg" />
    <Avatar Data="avatar3.jpg" />
</AvatarList>
```

### Progress

```razor
<Progress Percentage="75" Color="TablerColor.Primary" />
<Progress Percentage="50" Color="TablerColor.Success" Size="ProgressSize.Small" />
<Progress Indeterminate Color="TablerColor.Info" />
<Progress Percentage="60" Text="60%" />
```

**Progress Parameters:**
- `Percentage` (int): Progress value (0-100)
- `Color` (TablerColor): Progress bar color
- `Size` (ProgressSize): `Default`, `Small`, `Large`
- `Indeterminate` (bool): Indeterminate animation
- `Text` (string): Text overlay

### Icon

```razor
<Icon IconType="@TablerIcons.Home" />
<Icon IconType="@TablerIcons.Settings" Size="32" />
<Icon IconType="@TablerIcons.User" Color="blue" />
<Icon IconType="@TablerIcons.Heart" TextColor="TablerColor.Danger" />
<Icon IconType="@TablerIcons.Star" Animation="IconAnimation.Pulse" />
```

**Icon Parameters:**
- `IconType` (IIconType): Icon from TablerIcons
- `Size` (int): Icon size in pixels (default: 24)
- `Color` (string): CSS color
- `TextColor` (TablerColor): Color from palette
- `StrokeWidth` (double?): Stroke width
- `Rotate` (int): Rotation degrees
- `Animation` (IconAnimation): `None`, `Pulse`, `Tada`, `Rotate`

### Dropdown

```razor
<Dropdown>
    <Button Text="Dropdown" BackgroundColor="TablerColor.Primary" IsDropdown />
    <DropdownTemplate>
        <DropdownMenu>
            <DropdownItem Href="/action1">Action 1</DropdownItem>
            <DropdownItem Href="/action2">Action 2</DropdownItem>
            <DropdownItem @onclick="HandleClick">Action 3</DropdownItem>
        </DropdownMenu>
    </DropdownTemplate>
</Dropdown>
```

**Dropdown Parameters:**
- `CloseOnClick` (bool): Close on item click (default: true)
- `Direction` (DropdownDirection): Direction to open

### Tabs

```razor
<Tabs>
    <Tab Title="Tab 1">
        Content for tab 1
    </Tab>
    <Tab Title="Tab 2">
        Content for tab 2
    </Tab>
    <Tab Title="Tab 3" Disabled>
        Disabled tab
    </Tab>
</Tabs>
```

### Accordion

```razor
<Accordion>
    <AccordionItem Title="Section 1">
        Content for section 1
    </AccordionItem>
    <AccordionItem Title="Section 2">
        Content for section 2
    </AccordionItem>
</Accordion>
```

---

## Form Components

### TablerForm (Form Validation)

```razor
@using System.ComponentModel.DataAnnotations

<TablerForm Model="@model" OnValidSubmit="HandleSubmit">
    <div class="mb-3">
        <label class="form-label">Name</label>
        <InputText class="form-control" @bind-Value="model.Name" />
        <TabValidationMessage For="@(() => model.Name)" />
    </div>
    
    <div class="mb-3">
        <label class="form-label">Email</label>
        <InputText class="form-control" @bind-Value="model.Email" />
        <TabValidationMessage For="@(() => model.Email)" />
    </div>
    
    <Button Type="ButtonType.Submit" BackgroundColor="TablerColor.Primary" Text="Submit" />
</TablerForm>

@code {
    private MyModel model = new();
    
    public class MyModel
    {
        [Required]
        [StringLength(100)]
        public string Name { get; set; }
        
        [Required]
        [EmailAddress]
        public string Email { get; set; }
    }
    
    private async Task HandleSubmit(EditContext context)
    {
        // Handle form submission
    }
}
```

### Checkbox

```razor
<Checkbox @bind-Value="isChecked" Label="Accept terms" />
<Checkbox @bind-Value="isEnabled" Label="Enable feature" Description="Enable this feature for advanced users" />
<Checkbox @bind-Value="isSwitch" Label="Toggle switch" Switch />
<Checkbox @bind-Value="isDisabled" Label="Disabled" Disabled />
```

**Checkbox Parameters:**
- `Value` (bool): Checkbox state
- `Label` (string): Label text
- `Description` (string): Additional description
- `Switch` (bool): Render as switch
- `Disabled` (bool): Disable checkbox

### Select

```razor
<Select Items="options" 
        @bind-SelectedValue="selectedOption"
        TextExpression="e => e.Name"
        ValueExpression="e => e.Id"
        Clearable />

@code {
    private List<Option> options = new() {
        new Option { Id = 1, Name = "Option 1" },
        new Option { Id = 2, Name = "Option 2" }
    };
    private int selectedOption;
}
```

### ItemSelect

```razor
<ItemSelect Items="items"
            @bind-SelectedValue="selectedItem"
            TextExpression="e => e.Name" />
```

### Datepicker

```razor
<Datepicker @bind-SelectedDate="selectedDate" />
<Datepicker @bind-SelectedDate="selectedDate" Format="yyyy-MM-dd" />
<Datepicker @bind-SelectedDate="selectedDate" Inline />

@code {
    private DateTime? selectedDate;
    // Or use DateTimeOffset?
    private DateTimeOffset? selectedDateOffset;
}
```

**Datepicker Parameters:**
- `SelectedDate` (DateTime? or DateTimeOffset?): Selected date
- `Format` (string): Date format string (default: "d")
- `Inline` (bool): Show inline instead of dropdown
- `Label` (string): Field label

### Typeahead

```razor
<Typeahead TItem="Customer" TValue="Customer"
           SearchMethod="SearchCustomers"
           @bind-SelectedValue="selectedCustomer"
           SelectedTextExpression="e => e.Name"
           MinimumLength="2"
           Debounce="300"
           SearchPlaceholderText="Search customers...">
    <ListTemplate>
        <div>@context.Name</div>
        <small class="text-muted">@context.Email</small>
    </ListTemplate>
</Typeahead>

@code {
    private Customer selectedCustomer;
    
    private async Task<IEnumerable<Customer>> SearchCustomers(string searchText)
    {
        // Return matching customers
        return customers.Where(c => c.Name.Contains(searchText, StringComparison.OrdinalIgnoreCase));
    }
}
```

**Typeahead Parameters:**
- `SearchMethod` (Func<string, Task<IEnumerable<TItem>>>): Search function
- `SelectedValue` (TValue): Selected value
- `SelectedTextExpression` (Func<TValue, string>): Display text
- `MinimumLength` (int): Min characters to search (default: 3)
- `Debounce` (int): Debounce in ms (default: 300)
- `MaximumItems` (int): Max results (default: 20)
- `ConvertExpression` (Func<TItem, TValue>): Convert item to value
- `ShowOptionOnFocus` (bool): Show options on focus

---

## Data Components

### Table

Full-featured data table with sorting, filtering, selection, and editing:

```razor
<Table Item="Order" 
       Items="orders" 
       PageSize="10"
       ShowCheckboxes
       MultiSelect
       Hover
       Responsive
       @bind-SelectedItems="selectedOrders"
       OnItemEdited="HandleEdit"
       OnItemDeleted="HandleDelete"
       OnItemAdded="HandleAdd"
       OnRowClicked="HandleRowClick">
    
    <HeaderTemplate>
        <strong>Orders</strong>
    </HeaderTemplate>
    
    <ChildContent>
        <Column Item="Order" Property="e => e.Id" Title="ID" Sortable Searchable />
        
        <Column Item="Order" Property="e => e.CustomerName" Title="Customer" Sortable Searchable Groupable>
            <EditorTemplate>
                <input type="text" class="form-control" @bind-value="@context.CustomerName" />
            </EditorTemplate>
        </Column>
        
        <Column Item="Order" Property="e => e.Amount" Title="Amount" Sortable Align="Align.End">
            <Template>
                $@context.Amount.ToString("N2")
            </Template>
        </Column>
        
        <Column Item="Order" Property="e => e.Status" Title="Status" Sortable Groupable>
            <Template>
                <Badge BackgroundColor="@GetStatusColor(context.Status)">@context.Status</Badge>
            </Template>
            <EditorTemplate>
                <Select Items="statusOptions" @bind-SelectedValue="@context.Status" />
            </EditorTemplate>
        </Column>
    </ChildContent>
    
    <RowActionTemplate>
        <Button IsIcon BackgroundColor="TablerColor.Info" @onclick="() => ViewDetails(context)">
            <Icon IconType="@TablerIcons.Eye" />
        </Button>
    </RowActionTemplate>
</Table>

@code {
    private List<Order> orders = new();
    private List<Order> selectedOrders = new();
    
    private async Task HandleEdit(Order order) { /* ... */ }
    private async Task HandleDelete(Order order) { /* ... */ }
    private async Task HandleAdd(Order order) { /* ... */ }
    private void HandleRowClick(Order order) { /* ... */ }
}
```

**Table Parameters:**
- `Items` (IList<Item>): Data source
- `PageSize` (int): Items per page (default: 20)
- `ShowCheckboxes`, `MultiSelect`, `Hover`, `Responsive` (bool)
- `Selectable` (bool): Allow row selection
- `ShowHeader`, `ShowTableHeader`, `ShowFooter` (bool)
- `EditMode` (TableEditMode): `Inline` or `Popup`
- `OnItemEdited`, `OnItemDeleted`, `OnItemAdded` (EventCallback<Item>)
- `OnRowClicked` (EventCallback<Item>)
- `SelectedItems` (List<Item>): Selected items
- `ConfirmDelete` (bool): Show delete confirmation

**Column Parameters:**
- `Property` (Expression<Func<Item, object>>): Property expression
- `Title` (string): Column header
- `Sortable`, `Searchable`, `Groupable` (bool)
- `Visible` (bool): Column visibility
- `Align` (Align): `Start`, `Center`, `End`
- `Width` (string): Column width

### QuickTable

High-performance virtualized table:

```razor
<QuickTable Items="@data" Virtualize ItemSize="50">
    <PropertyColumn Property="@(e => e.Id)" Title="ID" Sortable />
    <PropertyColumn Property="@(e => e.Name)" Title="Name" Sortable />
    <TemplateColumn Title="Actions">
        <Button IsIcon @onclick="() => Edit(context)">
            <Icon IconType="@TablerIcons.Edit" />
        </Button>
    </TemplateColumn>
</QuickTable>

<!-- With pagination -->
<QuickTable Items="@data" Pagination="@pagination">
    <PropertyColumn Property="@(e => e.Id)" Title="ID" />
    <PropertyColumn Property="@(e => e.Name)" Title="Name" />
</QuickTable>
<Paginator State="@pagination" />

@code {
    private IQueryable<MyItem> data;
    private PaginationState pagination = new() { ItemsPerPage = 10 };
}
```

**QuickTable Parameters:**
- `Items` (IQueryable<TGridItem>): Data source
- `ItemsProvider` (GridItemsProvider<TGridItem>): Async data provider
- `Virtualize` (bool): Enable virtualization
- `ItemSize` (float): Row height for virtualization
- `Pagination` (PaginationState): Pagination state
- `ResizableColumns` (bool): Allow column resizing

### DataGrid

Simple data grid layout:

```razor
<DataGrid>
    <DataGridItem Title="Name">John Doe</DataGridItem>
    <DataGridItem Title="Email">john@example.com</DataGridItem>
    <DataGridItem Title="Status">
        <Badge BackgroundColor="TablerColor.Success">Active</Badge>
    </DataGridItem>
</DataGrid>
```

### TreeView

```razor
<TreeView Items="treeItems"
          ChildSelector="e => e.Children"
          @bind-SelectedItem="selectedNode"
          MultiSelect
          CheckboxMode="CheckboxMode.Single"
          EnableDragAndDrop
          ItemDropped="HandleDrop">
    <Template>
        <Icon IconType="@(context.IsFolder ? TablerIcons.Folder : TablerIcons.File)" />
        @context.Name
    </Template>
</TreeView>

@code {
    private List<TreeNode> treeItems;
    private TreeNode selectedNode;
    
    private void HandleDrop(ItemDropped<TreeNode> e)
    {
        // Handle drag and drop
    }
}
```

**TreeView Parameters:**
- `Items` (IList<TItem>): Root items
- `ChildSelector` (Func<TItem, IList<TItem>>): Get children
- `ChildSelectorAsync` (Func<TItem, Task<IList<TItem>>>): Async children
- `SelectedItem` (TItem): Single selection
- `SelectedItems` (List<TItem>): Multi selection
- `CheckedItems` (List<TItem>): Checked items
- `MultiSelect`, `AlwaysExpanded`, `AlignTreeNodes` (bool)
- `CheckboxMode` (CheckboxMode): `None`, `Single`, `Recursive`
- `EnableDragAndDrop` (bool): Enable drag and drop
- `DefaultExpanded` (Func<TItem, bool>): Default expanded state

---

## Services

### Modal Service

```razor
@inject IModalService ModalService

@code {
    private async Task ShowModal()
    {
        // Show component in modal
        var component = new RenderComponent<MyModalContent>()
            .Set(e => e.Title, "My Title")
            .Set(e => e.Data, someData);
            
        var result = await ModalService.ShowAsync("Modal Title", component, new ModalOptions
        {
            Size = ModalSize.Large,
            ShowCloseButton = true,
            CloseOnClickOutside = false,
            Scrollable = true,
            StatusColor = TablerColor.Primary
        });
        
        if (!result.Cancelled)
        {
            // Handle result
            var data = result.Data;
        }
    }
    
    private async Task ShowDialog()
    {
        var confirmed = await ModalService.ShowDialogAsync(new DialogOptions
        {
            MainText = "Are you sure?",
            SubText = "This action cannot be undone.",
            IconType = TablerIcons.Alert_triangle,
            StatusColor = TablerColor.Warning,
            OkText = "Yes, delete",
            CancelText = "Cancel"
        });
        
        if (confirmed)
        {
            // User confirmed
        }
    }
}
```

**ModalOptions:**
- `Size` (ModalSize): `Small`, `Medium`, `Large`, `ExtraLarge`, `Full`
- `Fullscreen` (ModalFullscreen): `Never`, `Always`, `BelowSm`, `BelowMd`, etc.
- `ShowHeader`, `ShowCloseButton`, `Scrollable` (bool)
- `CloseOnClickOutside`, `CloseOnEsc`, `Draggable` (bool)
- `BlurBackground`, `Backdrop` (bool)
- `StatusColor` (TablerColor?)
- `VerticalPosition` (ModalVerticalPosition): `Default`, `Centered`

### Toast Service

```razor
@inject ToastService ToastService

@code {
    private async Task ShowToast()
    {
        await ToastService.AddToastAsync(new ToastModel(
            "Success",
            "Operation completed successfully"
        ));
        
        // With options
        await ToastService.AddToastAsync(new ToastModel(
            "Warning",
            "Please review your changes",
            options: new ToastOptions
            {
                Delay = 5,
                Position = ToastPosition.TopEnd,
                ShowProgress = true
            }
        ));
        
        // With custom content
        var component = new RenderComponent<MyToastContent>()
            .Set(e => e.Message, "Custom message");
        await ToastService.AddToastAsync("Title", "Subtitle", component);
    }
}
```

**ToastOptions:**
- `Delay` (int): Auto-close delay in seconds (0 = never)
- `Position` (ToastPosition): `TopEnd`, `TopStart`, `BottomEnd`, `BottomStart`
- `ShowHeader`, `ShowProgress`, `AllowUserRemove` (bool)

### Offcanvas Service

```razor
@inject IOffcanvasService OffcanvasService

@code {
    private async Task ShowOffcanvas()
    {
        var component = new RenderComponent<MySidePanel>()
            .Set(e => e.Data, myData);
            
        var result = await OffcanvasService.ShowAsync("Panel Title", component, new OffcanvasOptions
        {
            Position = OffcanvasPosition.End,
            Size = OffcanvasSize.Large
        });
    }
}
```

### TablerService

```razor
@inject TablerService TablerService

@code {
    private async Task UtilityMethods()
    {
        // Theme
        await TablerService.SetTheme(darkTheme: true);
        
        // Clipboard
        await TablerService.CopyToClipboard("Text to copy");
        var text = await TablerService.ReadFromClipboard();
        
        // File operations
        await TablerService.SaveAsBinary("file.pdf", "application/pdf", bytes);
        await TablerService.SaveAsFile("file.txt", "data:text/plain;base64,...");
        
        // UI helpers
        await TablerService.ScrollToFragment("section-id");
        await TablerService.ShowAlert("Alert message");
    }
}
```

---

## Colors and Theming

### TablerColor Enum

Available colors for components:

```csharp
TablerColor.Default    // No color applied
TablerColor.Primary    // Primary brand color
TablerColor.Secondary  // Secondary color
TablerColor.Success    // Green
TablerColor.Info       // Light blue
TablerColor.Warning    // Yellow/Orange
TablerColor.Danger     // Red
TablerColor.Light      // Light gray
TablerColor.Dark       // Dark gray

// Additional colors
TablerColor.Blue
TablerColor.Azure
TablerColor.Indigo
TablerColor.Purple
TablerColor.Pink
TablerColor.Red
TablerColor.Orange
TablerColor.Yellow
TablerColor.Lime
TablerColor.Green
TablerColor.Teal
TablerColor.Cyan
TablerColor.White
```

### ColorType Enum

Modify color application:

```csharp
ColorType.Default   // Solid background
ColorType.Outline   // Outlined style
ColorType.Ghost     // Ghost/transparent style
```

### Dark Theme

```razor
@inject TablerService TablerService

<Button @onclick="ToggleTheme">Toggle Theme</Button>

@code {
    private bool isDark;
    
    private async Task ToggleTheme()
    {
        isDark = !isDark;
        await TablerService.SetTheme(isDark);
    }
}
```

---

## Common Patterns

### Page Layout

```razor
@page "/my-page"

<Page>
    <PageHeader Title="Page Title" Subtitle="Page description">
        <Actions>
            <Button BackgroundColor="TablerColor.Primary" Text="New Item" @onclick="AddNew" />
        </Actions>
    </PageHeader>
    
    <Card>
        <CardBody>
            <!-- Page content -->
        </CardBody>
    </Card>
</Page>
```

### Dashboard Layout

```razor
<Row HasCards>
    <RowCol Sm="6" Lg="3">
        <Card>
            <CardBody>
                <div class="d-flex align-items-center">
                    <div class="subheader">Total Users</div>
                </div>
                <div class="h1 mb-0">1,234</div>
            </CardBody>
        </Card>
    </RowCol>
    <RowCol Sm="6" Lg="3">
        <Card>
            <CardBody>
                <div class="subheader">Revenue</div>
                <div class="h1 mb-0">$45,678</div>
            </CardBody>
        </Card>
    </RowCol>
</Row>
```

### CRUD Operations

```razor
<Card>
    <CardHeader>
        <CardTitle>Items</CardTitle>
        <div class="card-actions">
            <Button BackgroundColor="TablerColor.Primary" @onclick="AddItem">
                <Icon IconType="@TablerIcons.Plus" /> Add Item
            </Button>
        </div>
    </CardHeader>
    <CardBody>
        <Table Item="MyItem" 
               Items="items" 
               OnItemAdded="HandleAdd"
               OnItemEdited="HandleEdit"
               OnItemDeleted="HandleDelete"
               EditMode="TableEditMode.Popup">
            <Column Item="MyItem" Property="e => e.Name" Title="Name" Sortable>
                <EditorTemplate>
                    <InputText class="form-control" @bind-Value="context.Name" />
                </EditorTemplate>
            </Column>
        </Table>
    </CardBody>
</Card>

@code {
    private List<MyItem> items = new();
    
    private async Task HandleAdd(MyItem item) 
    {
        // Save to database
    }
    
    private async Task HandleEdit(MyItem item)
    {
        // Update in database
    }
    
    private async Task HandleDelete(MyItem item)
    {
        // Delete from database
    }
}
```

### Form with Validation

```razor
<Card>
    <CardHeader>
        <CardTitle>Edit Profile</CardTitle>
    </CardHeader>
    <CardBody>
        <TablerForm Model="@model" OnValidSubmit="HandleSubmit">
            <Row>
                <RowCol Md="6">
                    <div class="mb-3">
                        <label class="form-label">First Name</label>
                        <InputText class="form-control" @bind-Value="model.FirstName" />
                        <TabValidationMessage For="@(() => model.FirstName)" />
                    </div>
                </RowCol>
                <RowCol Md="6">
                    <div class="mb-3">
                        <label class="form-label">Last Name</label>
                        <InputText class="form-control" @bind-Value="model.LastName" />
                        <TabValidationMessage For="@(() => model.LastName)" />
                    </div>
                </RowCol>
            </Row>
            
            <div class="mb-3">
                <label class="form-label">Email</label>
                <InputText class="form-control" @bind-Value="model.Email" />
                <TabValidationMessage For="@(() => model.Email)" />
            </div>
            
            <div class="mb-3">
                <label class="form-label">Birth Date</label>
                <Datepicker @bind-SelectedDate="model.BirthDate" />
                <TabValidationMessage For="@(() => model.BirthDate)" />
            </div>
            
            <div class="mb-3">
                <Checkbox @bind-Value="model.AcceptTerms" Label="I accept the terms and conditions" />
            </div>
            
            <ButtonList>
                <Button Type="ButtonType.Submit" BackgroundColor="TablerColor.Primary" Text="Save" />
                <Button Type="ButtonType.Button" BackgroundColor="TablerColor.Secondary" Text="Cancel" @onclick="Cancel" />
            </ButtonList>
        </TablerForm>
    </CardBody>
</Card>
```

---

## Complete Examples

### Admin Dashboard Page

```razor
@page "/dashboard"
@inject IModalService ModalService

<Page>
    <PageHeader Title="Dashboard" Subtitle="Welcome back, John!">
        <Actions>
            <Dropdown>
                <Button BackgroundColor="TablerColor.Primary" IsDropdown Text="Actions" />
                <DropdownTemplate>
                    <DropdownMenu>
                        <DropdownItem @onclick="ExportData">Export Data</DropdownItem>
                        <DropdownItem @onclick="RefreshData">Refresh</DropdownItem>
                    </DropdownMenu>
                </DropdownTemplate>
            </Dropdown>
        </Actions>
    </PageHeader>

    <!-- Stats Cards -->
    <Row HasCards>
        <RowCol Sm="6" Lg="3">
            <Card>
                <CardBody>
                    <div class="d-flex align-items-center">
                        <Icon IconType="@TablerIcons.Users" Size="48" TextColor="TablerColor.Primary" />
                        <div class="ms-3">
                            <div class="text-muted">Total Users</div>
                            <div class="h2 mb-0">@stats.TotalUsers.ToString("N0")</div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </RowCol>
        <RowCol Sm="6" Lg="3">
            <Card>
                <CardBody>
                    <div class="d-flex align-items-center">
                        <Icon IconType="@TablerIcons.Shopping_cart" Size="48" TextColor="TablerColor.Success" />
                        <div class="ms-3">
                            <div class="text-muted">Orders Today</div>
                            <div class="h2 mb-0">@stats.OrdersToday</div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </RowCol>
        <RowCol Sm="6" Lg="3">
            <Card>
                <CardBody>
                    <div class="d-flex align-items-center">
                        <Icon IconType="@TablerIcons.Currency_dollar" Size="48" TextColor="TablerColor.Warning" />
                        <div class="ms-3">
                            <div class="text-muted">Revenue</div>
                            <div class="h2 mb-0">$@stats.Revenue.ToString("N0")</div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </RowCol>
        <RowCol Sm="6" Lg="3">
            <Card>
                <CardBody>
                    <div class="d-flex align-items-center">
                        <Icon IconType="@TablerIcons.Activity" Size="48" TextColor="TablerColor.Info" />
                        <div class="ms-3">
                            <div class="text-muted">Active Sessions</div>
                            <div class="h2 mb-0">@stats.ActiveSessions</div>
                        </div>
                    </div>
                </CardBody>
            </Card>
        </RowCol>
    </Row>

    <!-- Recent Orders Table -->
    <Row>
        <RowCol Lg="8">
            <Card>
                <CardHeader>
                    <CardTitle>Recent Orders</CardTitle>
                    <div class="card-actions">
                        <Button BackgroundColor="TablerColor.Primary" 
                                BackgroundColorType="ColorType.Ghost" 
                                Text="View All" 
                                LinkTo="/orders" 
                                Type="ButtonType.Link" />
                    </div>
                </CardHeader>
                <Table Item="Order" Items="recentOrders" PageSize="5" Hover>
                    <Column Item="Order" Property="e => e.Id" Title="Order #" />
                    <Column Item="Order" Property="e => e.CustomerName" Title="Customer" />
                    <Column Item="Order" Property="e => e.Amount" Title="Amount" Align="Align.End">
                        <Template>$@context.Amount.ToString("N2")</Template>
                    </Column>
                    <Column Item="Order" Property="e => e.Status" Title="Status">
                        <Template>
                            <Badge BackgroundColor="@GetStatusColor(context.Status)">@context.Status</Badge>
                        </Template>
                    </Column>
                    <RowActionTemplate>
                        <Button IsIcon BackgroundColor="TablerColor.Info" BackgroundColorType="ColorType.Ghost" 
                                @onclick="() => ViewOrder(context)">
                            <Icon IconType="@TablerIcons.Eye" />
                        </Button>
                    </RowActionTemplate>
                </Table>
            </Card>
        </RowCol>
        
        <RowCol Lg="4">
            <Card>
                <CardHeader>
                    <CardTitle>Quick Actions</CardTitle>
                </CardHeader>
                <CardBody>
                    <div class="d-grid gap-2">
                        <Button Block BackgroundColor="TablerColor.Primary" @onclick="CreateOrder">
                            <Icon IconType="@TablerIcons.Plus" /> New Order
                        </Button>
                        <Button Block BackgroundColor="TablerColor.Secondary" @onclick="AddCustomer">
                            <Icon IconType="@TablerIcons.User_plus" /> Add Customer
                        </Button>
                        <Button Block BackgroundColor="TablerColor.Info" BackgroundColorType="ColorType.Outline" @onclick="GenerateReport">
                            <Icon IconType="@TablerIcons.Report" /> Generate Report
                        </Button>
                    </div>
                </CardBody>
            </Card>
            
            <Card class="mt-3">
                <CardHeader>
                    <CardTitle>Recent Activity</CardTitle>
                </CardHeader>
                <CardBody>
                    @foreach (var activity in recentActivities)
                    {
                        <div class="d-flex mb-3">
                            <Avatar Size="AvatarSize.Small" BackgroundColor="@activity.Color">
                                @activity.Initials
                            </Avatar>
                            <div class="ms-2">
                                <div class="fw-bold">@activity.Title</div>
                                <div class="text-muted small">@activity.Time</div>
                            </div>
                        </div>
                    }
                </CardBody>
            </Card>
        </RowCol>
    </Row>
</Page>

@code {
    private DashboardStats stats = new();
    private List<Order> recentOrders = new();
    private List<Activity> recentActivities = new();
    
    protected override async Task OnInitializedAsync()
    {
        // Load data
    }
    
    private TablerColor GetStatusColor(string status) => status switch
    {
        "Completed" => TablerColor.Success,
        "Pending" => TablerColor.Warning,
        "Cancelled" => TablerColor.Danger,
        _ => TablerColor.Secondary
    };
    
    private async Task ViewOrder(Order order) { /* ... */ }
    private async Task CreateOrder() { /* ... */ }
    private async Task AddCustomer() { /* ... */ }
    private async Task GenerateReport() { /* ... */ }
    private async Task ExportData() { /* ... */ }
    private async Task RefreshData() { /* ... */ }
}
```

### Data Entry Form

```razor
@page "/customers/new"
@inject IModalService ModalService
@inject NavigationManager Navigation

<Page>
    <PageHeader Title="New Customer" Subtitle="Add a new customer to your database">
        <Actions>
            <Button BackgroundColor="TablerColor.Secondary" Text="Cancel" @onclick="GoBack" />
        </Actions>
    </PageHeader>

    <Card>
        <CardBody>
            <TablerForm Model="@customer" OnValidSubmit="HandleSubmit">
                <Row>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label required">First Name</label>
                            <InputText class="form-control" @bind-Value="customer.FirstName" />
                            <TabValidationMessage For="@(() => customer.FirstName)" />
                        </div>
                    </RowCol>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label required">Last Name</label>
                            <InputText class="form-control" @bind-Value="customer.LastName" />
                            <TabValidationMessage For="@(() => customer.LastName)" />
                        </div>
                    </RowCol>
                </Row>

                <Row>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label required">Email</label>
                            <InputText class="form-control" type="email" @bind-Value="customer.Email" />
                            <TabValidationMessage For="@(() => customer.Email)" />
                        </div>
                    </RowCol>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label">Phone</label>
                            <InputText class="form-control" @bind-Value="customer.Phone" />
                        </div>
                    </RowCol>
                </Row>

                <div class="mb-3">
                    <label class="form-label">Company</label>
                    <Typeahead TItem="Company" TValue="Company"
                               SearchMethod="SearchCompanies"
                               @bind-SelectedValue="customer.Company"
                               SelectedTextExpression="e => e.Name"
                               MinimumLength="2"
                               SearchPlaceholderText="Search companies...">
                        <ListTemplate>
                            <div>@context.Name</div>
                            <small class="text-muted">@context.Industry</small>
                        </ListTemplate>
                    </Typeahead>
                </div>

                <Row>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label">Country</label>
                            <Select Items="countries"
                                    @bind-SelectedValue="customer.Country"
                                    TextExpression="e => e.Name"
                                    ValueExpression="e => e.Code"
                                    Clearable />
                        </div>
                    </RowCol>
                    <RowCol Md="6">
                        <div class="mb-3">
                            <label class="form-label">Customer Type</label>
                            <Select Items="customerTypes"
                                    @bind-SelectedValue="customer.Type"
                                    TextExpression="e => e"
                                    ValueExpression="e => e" />
                        </div>
                    </RowCol>
                </Row>

                <div class="mb-3">
                    <label class="form-label">Notes</label>
                    <InputTextArea class="form-control" rows="3" @bind-Value="customer.Notes" />
                </div>

                <div class="mb-3">
                    <Checkbox @bind-Value="customer.IsActive" Label="Active customer" />
                </div>

                <div class="mb-3">
                    <Checkbox @bind-Value="customer.SendNewsletter" 
                              Label="Subscribe to newsletter" 
                              Description="Receive updates about new products and promotions" />
                </div>

                <hr />

                <ButtonList>
                    <Button Type="ButtonType.Submit" BackgroundColor="TablerColor.Primary" Text="Save Customer" IsLoading="@isSaving" />
                    <Button Type="ButtonType.Button" BackgroundColor="TablerColor.Secondary" Text="Cancel" @onclick="GoBack" />
                </ButtonList>
            </TablerForm>
        </CardBody>
    </Card>
</Page>

@code {
    private CustomerModel customer = new();
    private List<Country> countries = new();
    private List<string> customerTypes = new() { "Individual", "Business", "Enterprise" };
    private bool isSaving;

    protected override async Task OnInitializedAsync()
    {
        countries = await LoadCountries();
    }

    private async Task<IEnumerable<Company>> SearchCompanies(string search)
    {
        // Search companies from API/database
        return new List<Company>();
    }

    private async Task HandleSubmit(EditContext context)
    {
        isSaving = true;
        try
        {
            // Save customer
            await Task.Delay(1000); // Simulated save
            
            await ModalService.ShowDialogAsync(new DialogOptions
            {
                MainText = "Customer saved successfully!",
                IconType = TablerIcons.Check,
                StatusColor = TablerColor.Success,
                CancelText = ""
            });
            
            Navigation.NavigateTo("/customers");
        }
        finally
        {
            isSaving = false;
        }
    }

    private void GoBack() => Navigation.NavigateTo("/customers");
}
```

---

## Tips for AI Agents

1. **Always wrap content in layout components**: Use `Page`, `Card`, `Row`, `RowCol` for proper structure.

2. **Use appropriate color semantics**:
   - `Primary` for main actions
   - `Success` for positive/confirmation
   - `Warning` for caution
   - `Danger` for destructive actions
   - `Info` for informational

3. **Leverage built-in services**: Use `IModalService`, `ToastService`, `IOffcanvasService` for overlays.

4. **Form validation**: Always use `TablerForm` with `TabValidationMessage` for proper validation display.

5. **Table best practices**:
   - Use `QuickTable` for large datasets with virtualization
   - Use `Table` for full CRUD functionality
   - Define `EditorTemplate` for editable columns

6. **Responsive design**: Always use `Row` and `RowCol` with responsive breakpoints (`Sm`, `Md`, `Lg`, etc.).

7. **Icons**: Use `TablerIcons` for consistent iconography throughout the application.

8. **Component composition**: Combine components like `Card` + `Table`, `Dropdown` + `Button` for rich interfaces.

9. **State management**: Use `@bind-` for two-way binding and `EventCallback` for parent notifications.

10. **Loading states**: Use `IsLoading` on buttons and conditional rendering for better UX during async operations.
