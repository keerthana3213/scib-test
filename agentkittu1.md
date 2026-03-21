# UI Component Architecture for 'Parent can allocate and manage funds for a youth account'

## 1. Jira Requirement Summary

**Story Description:**
AS a parent or guardian I WANT to allocate and manage funds for my child’s youth account SO THAT I can teach financial responsibility while maintaining visibility and control over spending.

**Acceptance Criteria:**
1. Access youth account dashboard: Parent logs in, navigates to youth account section, sees dashboard with current balance and recent activity.
2. Allocate funds to youth account: Parent selects "Add Funds" and can transfer funds from primary to youth account.
3. Set spending limit: Parent configures a weekly spending limit, which is saved and displayed on dashboard.
4. View youth spending activity: Parent selects activity section to see recent transactions from youth account.
5. Handle insufficient balance: If parent tries to transfer funds without enough balance, show error message.

**UI Tasks / Subtasks:**
- Design youth account dashboard layout
- Design fund transfer interaction for youth account
- Design spending limit configuration interface
- Design youth account activity view

---

## 2. HTML Structure Summary

**Note:** No HTML files were found in the GitHub repository (`ui_design.html` missing, and no HTML files present). Therefore, the architecture is based on Jira requirements and component documentation only.

**Expected Layout (from requirements):**
- Header (with navigation, user info)
- Sidebar (for navigation between sections)
- Main container (dashboard)
  - Youth Account Card (balance, limits, actions)
  - Add Funds Dialog/Modal
  - Spending Limit Configuration
  - Activity List (recent transactions)
  - Error Snackbar/Toast (for insufficient funds)

---

## 3. Reusable Components from Library

- Header (`aava-header`)
- Sidebar (`aava-sidebar`)
- Card (`aava-default-card`, `aava-card-header`, `aava-card-content`, `aava-card-footer`, `aava-card-actions`)
- Button (`aava-button`)
- Avatar (`aava-avatars`)
- Dialog/Modal (`aava-dialog`, `aava-modal`)
- Tabs (`aava-tabs`)
- Snackbar/Toast (`aava-snackbar`, `aava-toast`)
- Chip/Tag (`aava-tag`, `aava-chip-tag`)
- Grid (`aava-grid`)
- Textbox/Textarea (`aava-textbox`, `aava-textarea`)
- Dropdown (`aava-dropdown`)
- Accordion (`aava-accordion`)

---

## 4. Jira vs HTML Validation

- **Matching Elements:** N/A (no HTML available)
- **Missing Elements:** All UI elements inferred from Jira only
- **Extra Elements:** None
- **Note:** UI structure is based on requirements and component documentation, not on actual HTML implementation.

---

## 5. UI Component Architecture

**Screen: Youth Account Dashboard**

```
YouthAccountDashboardPage
├── HeaderComponent (aava-header)
├── SidebarComponent (aava-sidebar)
├── MainContainer
│   ├── YouthAccountCard (aava-default-card)
│   │   ├── CardHeader (aava-card-header)
│   │   │   ├── AvatarComponent (aava-avatars)
│   │   │   └── AccountName/ChipTag (aava-chip-tag)
│   │   ├── CardContent (aava-card-content)
│   │   │   ├── BalanceDisplay
│   │   │   ├── SpendingLimitDisplay
│   │   │   └── RecentActivitySummary
│   │   ├── CardFooter (aava-card-footer)
│   │   │   └── ActionButtons (aava-button: Add Funds, Set Limit)
│   ├── ActivityList (aava-card or aava-accordion)
│   │   └── ActivityItem (transaction row, possibly with aava-chip-tag for status)
│   ├── AddFundsDialog (aava-dialog or aava-modal)
│   │   ├── AmountTextbox (aava-textbox)
│   │   ├── SourceAccountDropdown (aava-dropdown)
│   │   └── Confirm/CancelButtons (aava-button)
│   ├── SpendingLimitDialog (aava-dialog or aava-modal)
│   │   ├── LimitTextbox (aava-textbox)
│   │   └── Save/CancelButtons (aava-button)
│   └── ErrorSnackbar (aava-snackbar or aava-toast)
```

---

## 6. Component Responsibilities

- **HeaderComponent:**
  - Displays app logo, navigation tabs, user avatar, and quick actions (theme, language, etc.)
- **SidebarComponent:**
  - Provides navigation between dashboard, activity, settings, etc.
- **YouthAccountCard:**
  - Shows youth account name, avatar, balance, spending limit, and quick actions (add funds, set limit)
- **ActivityList:**
  - Lists recent transactions for the youth account
- **AddFundsDialog:**
  - Modal/dialog for transferring funds from parent to youth account
- **SpendingLimitDialog:**
  - Modal/dialog for configuring weekly spending limit
- **ErrorSnackbar:**
  - Displays error messages (e.g., insufficient funds)

---

## 7. Data Flow / Props

- **YouthAccountDashboardPage**
  - → YouthAccountCard (youthAccountData)
  - → ActivityList (transactions)
  - → AddFundsDialog (open, onSubmit, onCancel)
  - → SpendingLimitDialog (open, onSubmit, onCancel)
  - → ErrorSnackbar (message, open)
- **YouthAccountCard**
  - → AvatarComponent (avatarUrl, userName)
  - → CardHeader (accountName, chipTag)
  - → CardContent (balance, spendingLimit, recentActivity)
  - → CardFooter (onAddFunds, onSetLimit)
- **AddFundsDialog**
  - → AmountTextbox (value, onChange)
  - → SourceAccountDropdown (accounts, selectedAccount)
  - → ConfirmButton (onClick)
- **SpendingLimitDialog**
  - → LimitTextbox (value, onChange)
  - → SaveButton (onClick)
- **ActivityList**
  - → ActivityItem (transactionData)

---

## 8. Layout Structure

```
Page Layout
├── Header (aava-header)
├── Sidebar (aava-sidebar)
├── Main Container
│   ├── Youth Account Card (aava-default-card)
│   ├── Activity List (aava-card or aava-accordion)
│   ├── Add Funds Dialog (aava-dialog or aava-modal)
│   ├── Spending Limit Dialog (aava-dialog or aava-modal)
│   └── Error Snackbar/Toast (aava-snackbar or aava-toast)
```

---

## 9. Notes
- All components are mapped to reusable components from the provided documentation.
- No new components are required unless a specific custom layout is needed.
- Actual UI implementation should be validated against the final HTML when available.
- Accessibility, responsiveness, and theming are supported by the chosen components.
