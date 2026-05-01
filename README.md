# User Management Screen - UI Specification Document

## 1. Purpose
This document explains the interface requirements and expected behavior for the **User Management Screen**.

The page is designed so that system administrators can manage all user-related actions in one place, such as:

- viewing the current list of users,
- creating new user accounts,
- editing user information,
- enabling or disabling accounts,
- and assigning user roles.

This document is intended to guide developers during the implementation of the screen.

---

## 2. Screen Layout

The interface is divided into three main parts.

### 2.1 Top Action Bar
This section appears at the top of the page and contains the main action controls:

- **+ New User button**
- **Hide Disabled User checkbox**
- **Save User button**

---

### 2.2 User List Panel (Left Side)
The left side contains a table that displays all stored user records.

The visible columns are:

- ID
- User Name
- Email
- Enabled

This area is mainly used for:
- browsing users,
- sorting records,
- filtering records,
- and selecting a user for editing.

---

### 2.3 User Detail Form (Right Side)
The right side contains the input form.

This form has two purposes:
- entering information for a completely new user, or
- modifying the details of a user selected from the table.

Because of this, the same panel should support both **New User mode** and **Edit User mode**.

---

## 3. Initial State (When the Page Loads)

When the screen is opened for the first time, the following should be visible:

1. The left table loads with all active users currently stored in the system.
2. The **Hide Disabled User** checkbox is checked by default.
3. The form on the right side opens in **New User mode**.
4. All form fields are empty.
5. The **Save User** button is visible, but saving should only happen if the entered data is valid.

---

## 4. Functional Requirements

### FR-1: Display Existing Users
The user table must display all available user records with the following information:

| Column | Description |
|--------|-------------|
| ID | Auto-generated unique identifier |
| User Name | Login name of the user |
| Email | Email address of the user |
| Enabled | Current account status (active/inactive) |

---

### FR-2: Creating a New User
When the administrator clicks **+ New User**, the system should:

- clear all fields in the right-side form,
- remove any selected row highlight from the table,
- keep the panel ready for new data entry,
- switch the form into new record mode.

---

### FR-3: Editing an Existing User
When a row from the left table is clicked:

- that row should become highlighted,
- the selected user's information should load into the right-side form.

The administrator can then change any editable values and save the updated information.

---

### FR-4: Saving User Information
When **Save User** is pressed, the system should behave according to the current form mode.

#### If the form is in New User mode:
- create a new user record,
- store it in the database,
- refresh the left table,
- display the new user entry.

#### If the form is in Edit User mode:
- update the selected user record,
- refresh the table with the changed information.

After saving successfully, a short confirmation message such as **"User saved successfully"** should be shown.

---

### FR-5: Hide Disabled User
The **Hide Disabled User** checkbox works as a display filter for the left table.

- **Checked:** only users with `Enabled = true` are shown.
- **Unchecked:** all users are shown, including disabled ones.

This option only changes what is visible in the table and should not remove any saved data.

---

### FR-6: Sorting and Filtering
Each table column header should support:

- ascending sort,
- descending sort,
- and filtering using the filter icon.

Sorting changes the order of visible records, while filtering narrows down which records are shown.

---

## 5. Form Field Specification

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| Username | Text input | Yes | Must be unique |
| Display Name | Text input | No | Name shown inside the system |
| Phone | Text input | No | Contact number |
| Email | Text input | Yes | Must follow valid email format |
| User Roles | Selectable dropdown/list | Yes | Guest, Admin, SuperAdmin |
| Enabled | Checkbox | No | Marks whether account is active |

---

## 6. User Roles

The **User Roles** field should allow the administrator to choose from the following options:

| Role | Access Level |
|------|--------------|
| Guest | Limited or read-only access |
| Admin | Permission to manage standard users |
| SuperAdmin | Full administrative access |

---

## 7. Validation Rules

Before any save action is completed, the following validations must be checked.

### Required Fields
These fields cannot be empty:
- Username
- Email
- User Roles

### Username Validation
- Username must be unique.
- It must not already exist in another user record.

### Email Validation
- Email must follow a standard format such as `name@domain.com`.

### Phone Validation
- Phone is optional.
- If entered, it may contain numbers, spaces, `+`, or `-`.

If validation fails:

- the user should remain on the same page,
- the invalid field should be visually highlighted,
- and an error message should be displayed.

Examples:
- "Username is required"
- "Invalid email format"
- "Username already exists"

---

## 8. Common Page Scenarios

### Scenario A - Adding a New User
1. Click **+ New User**
2. Empty form appears
3. Enter user information
4. Choose user role
5. Check Enabled if needed
6. Click **Save User**
7. New record appears in the left table

---

### Scenario B - Editing an Existing User
1. Click any user row in the left table
2. Existing information loads into the form
3. Modify the needed values
4. Click **Save User**
5. Updated information appears in the table

---

### Scenario C - Viewing Disabled Accounts
1. Uncheck **Hide Disabled User**
2. Disabled user records become visible
3. Check the box again to hide them

---

## 9. Additional UI Notes

- The currently selected row should always be visually highlighted.
- Labels and input boxes should remain aligned for readability.
- The left table should refresh immediately after every successful save.
- No full page reload should be required.
- All user management actions should be completed within this single screen.

---

## 10. Final Note
The main goal of this page is to keep user administration simple and efficient.  
With the table on the left and the editable form on the right, administrators should be able to complete all basic user management tasks without leaving the page.
