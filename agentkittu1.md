# UI Component Architecture: Parent Fund Management for Youth Account

---

## 1. Jira Requirement Summary

**Story:**
Parent can allocate and manage funds for a youth account

**Description:**
AS a parent or guardian I WANT to allocate and manage funds for my child’s youth account SO THAT I can teach financial responsibility while maintaining visibility and control over spending.

**Acceptance Criteria:**
1. Access youth account dashboard: Parent sees dashboard with current balance and recent activity.
2. Allocate funds: Parent can transfer funds from their primary account to the youth account.
3. Set spending limit: Parent can configure a weekly spending limit, which is displayed on the dashboard.
4. View youth spending activity: Parent can view recent transactions from the youth account.
5. Handle insufficient balance: If parent’s account lacks funds, show error message.

**UI Tasks (Subtasks):**
- Design youth account dashboard layout
- Design fund transfer interaction for youth account
- Design spending limit configuration interface
- Design youth account activity view

---

## 2. HTML Structure Summary

**Layout:**
- Sidebar navigation (Youth Account, Errors & Confirmations)
- Header with search, notifications, and avatar
- Main content area with multiple pages:
  - Dashboard: Account balance, spending limit, recent activity, quick actions
  - Add Funds: Fund transfer form (source, amount, templates, transfer limit)
  - Set Limit: Edit weekly spending limit
  - Activity: Transaction list
  - Error/Confirmation popups: Insufficient balance, transfer confirmation, success, invalid limit, dashboard load error

**Key UI Elements:**
- Sidebar menu (Dashboard, Add Funds, Set Limit, Activity)
- Header (search bar, notification bell, avatar chip)
- Cards for balance, limit, activity, and tips
- Buttons for actions (Add Funds, Set Limit, View Activity, Transfer, Save, Retry, etc.)
- Snackbar/alert for errors
- Dialogs for confirmations and success
- Input fields (amount, new limit, source account)
- Badges for templates, limits, and notifications

---

## 3. Reusable Components from Library

- **Sidebar** (`AavaSidebarComponent`)
- **Header** (composed of Search Bar, Notification Icon, Avatar Chip)
- **Card** (`AavaDefaultCardComponent`, `AavaCardHeaderComponent`, `AavaCardContentComponent`, `AavaCardFooterComponent`, `AavaCardActionsComponent`)
- **Button** (`AavaButtonComponent`)
- **Snackbar** (`SnackbarService`)
- **Dialog/Modal** (`AavaDialogService`)
- **Avatar** (`AavaAvatarsComponent`)
- **Badge** (`AavaBadgesComponent`)
- **Tabs** (if needed for future extensibility)
- **Textbox/Input** (for amount, limit)
- **Dropdown** (for source account)

---

## 4. Jira vs HTML Validation

**Matching Elements:**
- Dashboard, Add Funds, Set Limit, Activity, and error/confirmation flows are present in both Jira and HTML.
- All acceptance criteria are represented in the HTML structure.
- UI tasks are reflected in the HTML (dashboard, transfer, limit, activity views).

**Missing Elements:**
- None. All Jira requirements are covered in the HTML.

**Extra Elements:**
- Financial literacy tips card (not explicitly in Jira, but enhances user experience).
- Some error/confirmation flows (e.g., dashboard load error) are additional robustness features.

---

## 5. UI Component Architecture

**Screen: Parent Fund Management (Youth Account)**

```
ParentFundMgmtPage
├── SidebarNav (AavaSidebarComponent)
│   ├── MenuItem: Dashboard
│   ├── MenuItem: Add Funds
│   ├── MenuItem: Set Limit
│   ├── MenuItem: Activity
│   └── MenuItem: Error/Confirmation Flows
├── MainContent
│   ├── HeaderBar
│   │   ├── SearchBar (AavaTextboxComponent)
│   │   ├── NotificationIcon (with Badge)
│   │   └── AvatarChip (AavaAvatarsComponent + AavaBadgesComponent)
│   ├── PageRouter (controls which page is active)
│   │   ├── DashboardPage
│   │   │   ├── Card: Account Balance (AavaDefaultCardComponent)
│   │   │   ├── Card: Spending Limit (AavaDefaultCardComponent)
│   │   │   ├── Card: Recent Activity (AavaDefaultCardComponent)
│   │   │   ├── Card: Financial Literacy Tips (AavaDefaultCardComponent)
│   │   │   └── ButtonGroup (AavaButtonComponent: Add Funds, Set Limit, View Activity)
│   │   ├── FundTransferPage
│   │   │   ├── Dialog/Modal: Fund Transfer (AavaDialogService or AavaDefaultCardComponent)
│   │   │   │   ├── Dropdown: Source Account (AavaDropdownComponent)
│   │   │   │   ├── Textbox: Amount (AavaTextboxComponent)
│   │   │   │   ├── BadgeGroup: Templates (AavaBadgesComponent)
│   │   │   │   ├── Badge: Transfer Limit (AavaBadgesComponent)
│   │   │   │   └── ButtonGroup (AavaButtonComponent: Transfer, Cancel)
│   │   ├── SetLimitPage
│   │   │   ├── Dialog/Modal: Set Limit (AavaDialogService or AavaDefaultCardComponent)
│   │   │   │   ├── InfoRow: Current Limit
│   │   │   │   ├── Textbox: New Limit (AavaTextboxComponent)
│   │   │   │   ├── InfoRow: Guidance
│   │   │   │   └── ButtonGroup (AavaButtonComponent: Save, Cancel)
│   │   ├── ActivityPage
│   │   │   └── Card: Transaction List (AavaDefaultCardComponent)
│   │   ├── Snackbar/Alert (SnackbarService): Error/Success messages
│   │   ├── Dialog/Modal (AavaDialogService): Confirmation, Success, Error
```

---

## 6. Component Responsibilities

- **SidebarNav**: Navigation between dashboard, fund transfer, limit, activity, and error/confirmation flows.
- **HeaderBar**: Displays search, notifications (with badge), and user avatar (with badge).
- **DashboardPage**:
  - Shows account balance, spending limit, recent activity, and tips in cards.
  - Provides quick action buttons for Add Funds, Set Limit, and View Activity.
- **FundTransferPage**:
  - Allows parent to select source account, enter amount, use templates, see transfer limit, and initiate/cancel transfer.
  - Shows confirmation and success dialogs as needed.
- **SetLimitPage**:
  - Allows parent to view current limit, enter new limit, see guidance, and save/cancel changes.
  - Shows confirmation and error dialogs as needed.
- **ActivityPage**:
  - Displays a list of recent transactions in a card layout.
- **Snackbar/Alert**:
  - Shows error messages (e.g., insufficient balance, invalid limit, dashboard load error).
- **Dialog/Modal**:
  - Used for confirmations (transfer, limit update), success, and error flows.

---

## 7. Data Flow / Props

- **ParentFundMgmtPage** → SidebarNav (activePage)
- **ParentFundMgmtPage** → MainContent (user, notifications, activePage)
- **HeaderBar**
  - Receives: user (for Avatar), notifications (for Badge)
- **DashboardPage**
  - Receives: accountBalance, spendingLimit, recentActivity, tips
  - Passes: onAddFunds, onSetLimit, onViewActivity (button handlers)
- **FundTransferPage**
  - Receives: sourceAccounts, transferTemplates, transferLimit
  - Passes: onTransfer, onCancel
- **SetLimitPage**
  - Receives: currentLimit, guidance
  - Passes: onSaveLimit, onCancel
- **ActivityPage**
  - Receives: transactions
- **Snackbar/Alert**
  - Receives: message, type (error, warning, info, success)
- **Dialog/Modal**
  - Receives: dialogType, dialogProps (title, message, actions)

---

## 8. Layout Structure

```
Page Layout
├── SidebarNav (left)
├── MainContent (right)
│   ├── HeaderBar (top)
│   └── PageRouter (below header)
│       ├── DashboardPage
│       ├── FundTransferPage
│       ├── SetLimitPage
│       ├── ActivityPage
│       └── Snackbar/Dialog overlays (as needed)
```

---

## 9. Component Mapping Table

| UI Element                | Reusable Component           | Notes                                    |
|--------------------------|------------------------------|------------------------------------------|
| Sidebar                  | AavaSidebarComponent         | Navigation, branding, menu, footer       |
| Header                   | Custom (uses Avatar, Badge)  | SearchBar, NotificationIcon, AvatarChip  |
| Card                     | AavaDefaultCardComponent     | For balance, limit, activity, tips       |
| Button                   | AavaButtonComponent          | All actions                              |
| Snackbar/Alert           | SnackbarService              | Error/success messages                   |
| Dialog/Modal             | AavaDialogService            | Confirmation, success, error             |
| Avatar                   | AavaAvatarsComponent         | User identity                            |
| Badge                    | AavaBadgesComponent          | Notifications, templates, limits         |
| Input/Textbox            | AavaTextboxComponent         | Amount, new limit                        |
| Dropdown                 | AavaDropdownComponent        | Source account selection                 |

---

## 10. Notes on Reuse and Extensibility

- All major UI elements are mapped to reusable components from the Play library.
- No new custom components are required for the current scope; only composition and configuration.
- The architecture supports future extensibility (e.g., tabs, additional dialogs, more dashboard cards).
- All error and confirmation flows use Dialog and Snackbar components for consistency.
- The layout and component structure are modular and maintainable.

---

## 11. Accessibility & Theming

- All components follow accessibility best practices (ARIA, keyboard navigation, focus management).
- Theming and design tokens are used throughout for consistent look and feel.
- Responsive design is supported by all core components.

---

## 12. Performance & Best Practices

- Use OnPush change detection for all container components.
- Lazy load dialog/modal content as needed.
- Debounce rapid actions (e.g., transfer, save limit).
- Optimize avatar and badge updates for notification changes.

---

# END OF ARCHITECTURE
