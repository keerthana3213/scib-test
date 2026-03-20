# UI Component Architecture for Youth Account Dashboard

## 1. Jira Requirement Summary

**Story:**
Parent can allocate and manage funds for a youth account

**Description:**
As a parent or guardian, I want to allocate and manage funds for my child’s youth account so that I can teach financial responsibility while maintaining visibility and control over spending.

**Acceptance Criteria:**
1. Access youth account dashboard: Parent logs in, navigates to youth account section, sees dashboard with current balance and recent activity.
2. Allocate funds to youth account: Parent selects “Add Funds”, can transfer funds from their primary account to the youth account.
3. Set spending limit: Parent configures a weekly spending limit, system saves and displays the limit on the dashboard.
4. View youth spending activity: Parent selects activity section, system displays recent transactions from the youth account.
5. Handle insufficient balance: If parent’s account lacks funds, system displays an error message.

**UI Tasks / Subtasks:**
- Design youth account dashboard layout
- Design fund transfer interaction for youth account
- Design spending limit configuration interface
- Design youth account activity view

---

## 2. HTML Structure Summary

**Note:** The HTML structure could not be fetched from GitHub (`index.html` not found). The architecture below is based on Jira requirements and reusable component documentation.

**Expected Layout:**
- Header (with navigation, user avatar, and actions)
- Main Container
  - Balance Card (shows current balance)
  - Add Funds Card (with transfer form/button)
  - Spending Limit Card (shows and configures limit)
  - Activity Section (list of recent transactions)
  - Error/Notification area (for insufficient funds, etc.)

---

## 3. Reusable Components from Library

- Header
- Card (Default, Header, Content, Footer, Actions)
- Button
- Tabs
- Avatar
- Snackbar
- Dialog
- Modal
- Grid
- Timeline
- Badge
- Chip-Tag
- Dropdown
- Sidebar
- Search-Bar
- Pagination
- Stepper-Input

---

## 4. Jira vs HTML Validation

- **Matching Elements:**
  - All required dashboard features are mapped to components (see architecture below).
- **Missing Elements:**
  - HTML structure could not be validated (index.html missing in GitHub repo).
- **Extra Elements:**
  - None detected (HTML not available).

---

## 5. UI Component Architecture

**Screen:** Youth Account Dashboard

```
YouthAccountDashboardPage
├── HeaderComponent (AavaHeaderComponent)
│   ├── Logo
│   ├── Tabs (AavaTabs) [Overview, Activity, Settings]
│   └── UserActions (Avatar, Icons, Dropdown)
├── MainContainer
│   ├── BalanceCard (AavaDefaultCard)
│   │   ├── CardHeader ("Current Balance")
│   │   └── CardContent (Balance amount, Badge for status)
│   ├── AddFundsCard (AavaDefaultCard)
│   │   ├── CardHeader ("Add Funds")
│   │   └── CardContent (Transfer form: Dropdown for source account, Textbox for amount, Button)
│   │   └── CardFooter (Button: "Transfer")
│   ├── SpendingLimitCard (AavaDefaultCard)
│   │   ├── CardHeader ("Spending Limit")
│   │   └── CardContent (Stepper-Input/Textbox for limit, Button: "Save Limit")
│   ├── ActivitySection (AavaDefaultCard)
│   │   ├── CardHeader ("Recent Activity")
│   │   └── CardContent (Timeline/List of transactions)
│   ├── Snackbar/Toast (for notifications/errors)
│   └── Dialog/Modal (for confirmation/error details)
└── Sidebar (optional, for navigation)
```

---

## 6. Component Responsibilities

**HeaderComponent**
- Displays logo, navigation tabs (Overview, Activity, Settings), user avatar, and quick actions (icons, dropdown).

**BalanceCard**
- Shows current youth account balance and status badge.

**AddFundsCard**
- Allows parent to select source account, enter amount, and transfer funds to youth account.
- Shows error dialog/snackbar if insufficient funds.

**SpendingLimitCard**
- Allows parent to view and set a weekly spending limit for the youth account.

**ActivitySection**
- Displays a timeline or list of recent transactions from the youth account.

**Snackbar/Toast**
- Shows notifications for success, errors (e.g., insufficient funds), and confirmations.

**Dialog/Modal**
- Used for confirmation dialogs or detailed error messages.

**Sidebar**
- (Optional) For navigation between dashboard sections.

---

## 7. Data Flow / Props

**YouthAccountDashboardPage**
- Passes user, account, and transaction data to child components.

**HeaderComponent**
- Receives: `user`, `tabs`, `activeTabId`
- Emits: `tabChange`, `userAction`

**BalanceCard**
- Receives: `balance`, `status`

**AddFundsCard**
- Receives: `accounts`, `onTransfer`
- Emits: `transferRequest`

**SpendingLimitCard**
- Receives: `currentLimit`, `onSaveLimit`
- Emits: `limitChange`

**ActivitySection**
- Receives: `transactions`

**Snackbar/Toast**
- Receives: `message`, `type`

**Dialog/Modal**
- Receives: `open`, `title`, `content`, `onClose`

---

## 8. Layout Structure

```
Page Layout
├── Header (AavaHeaderComponent)
├── Main Container (Grid/Flex)
│   ├── Balance Card
│   ├── Add Funds Card
│   ├── Spending Limit Card
│   └── Activity Section
├── Snackbar/Toast (overlay)
├── Dialog/Modal (overlay)
└── Sidebar (optional)
```

---

## Notes
- All major UI elements are mapped to reusable components from the provided library.
- No new components are required; all can be composed from existing documented components.
- HTML structure could not be validated due to missing file in GitHub.
- The architecture is modular, scalable, and aligns with Jira requirements and available UI library.
