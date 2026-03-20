# Youth Account Parent Fund Management — UI Component Architecture

## 1. Jira Requirement Summary

**Story Description:**
AS a parent or guardian I WANT to allocate and manage funds for my child’s youth account SO THAT I can teach financial responsibility while maintaining visibility and control over spending

**Acceptance Criteria:**
- Scenario 1: Access youth account dashboard — Parent sees dashboard with current balance and recent activity
- Scenario 2: Allocate funds to youth account — Parent can transfer funds from their primary account to youth account
- Scenario 3: Set spending limit — Parent configures weekly spending limit, system saves/displays limit
- Scenario 4: View youth spending activity — Parent sees recent transactions
- Scenario 5: Handle insufficient balance — Error message shown if parent account lacks funds

**UI Tasks/Subtasks:**
- Design youth account activity view
- Design spending limit configuration interface
- Design fund transfer interaction for youth account
- Design youth account dashboard layout

---

## 2. HTML Structure Summary

**Layout (from ui_design.html and wireframe.html):**
- Sidebar navigation (Dashboard, Youth Account, Allocate Funds, Set Spending Limit, Spending Activity, Help/FAQ)
- Topbar/header (search, notifications, avatar)
- Main container with pages:
  - Main Dashboard: Parent and Youth account cards, transfer funds button
  - Youth Account Dashboard: Balance, weekly limit, quick actions, recent activity
  - Fund Transfer: Form (amount, source account), error handling, confirmation
  - Spending Limit Edit: Form (weekly limit), error handling, confirmation
  - Activity List: Transaction list, filter tabs
  - Success/Error popups

**UI Elements:**
- Cards for account balances, activity, limits
- Buttons for actions (Add Funds, Edit Limit, View Activity, Confirm, Cancel)
- Forms (input, select)
- Tabs for filtering activity
- Badges for transaction amounts
- Error bubbles/messages
- Avatar for parent/guardian

---

## 3. Reusable Components from Library

**Identified from documentation ZIP:**
- Card (aava-default-card, aava-card-header, aava-card-content, aava-card-footer, aava-card-actions)
- Button (aava-button)
- Badge (aava-badge)
- Avatar (aava-avatar)
- Sidebar (aava-sidebar)
- Tabs (aava-tabs)
- Dialog/Modal (aava-modal)
- Input (aava-textbox, aava-select, aava-textarea)
- Snackbar/Toast (aava-snackbar, aava-toast)
- Divider (aava-divider)
- Progress Bar (aava-progress-bar)
- Chip-Tag (aava-chip-tag)
- Tooltip (aava-tooltip)
- Popover (aava-popover)
- Stepper Input (aava-stepper-input)
- Timeline (aava-timeline)
- TreeView (aava-treeview)
- Skeleton Loader (aava-skeleton-loader)

---

## 4. Jira vs HTML Validation

**Matching Elements:**
- Youth account dashboard with balance, recent activity (Jira Scenario 1) — present in HTML
- Fund allocation form and confirmation (Jira Scenario 2) — present in HTML
- Spending limit configuration/edit (Jira Scenario 3) — present in HTML
- Activity list and transaction history (Jira Scenario 4) — present in HTML
- Error handling for insufficient balance (Jira Scenario 5) — present in HTML

**Missing Elements:**
- All Jira acceptance criteria are reflected in HTML structure

**Extra Elements:**
- Help/FAQ section (not explicitly in Jira, but useful)
- Educational tips in limit management (not in Jira, but enhances UX)

---

## 5. UI Component Architecture

**Screen: Main Dashboard**
- MainDashboardPage
  - SidebarComponent (aava-sidebar)
  - HeaderComponent (search, notifications, avatar)
  - ParentAccountCard (aava-default-card)
  - YouthAccountCard (aava-default-card)
    - TransferFundsButton (aava-button)

**Screen: Youth Account Dashboard**
- YouthAccountDashboardPage
  - SidebarComponent
  - HeaderComponent
  - BalanceCard (aava-default-card)
  - WeeklyLimitCard (aava-default-card)
    - EditLimitButton (aava-button)
    - ManageLimitButton (aava-button)
  - QuickActionsCard (aava-default-card)
    - AddFundsButton (aava-button)
    - ViewActivityButton (aava-button)
  - RecentActivityCard (aava-default-card)
    - ActivityList (aava-timeline or custom list)
    - TransactionBadge (aava-badge)
    - ViewAllButton (aava-button)

**Screen: Fund Transfer**
- FundTransferPage
  - SidebarComponent
  - HeaderComponent
  - FundTransferForm (aava-default-card)
    - AmountInput (aava-textbox)
    - SourceAccountSelect (aava-select)
    - ErrorBubble (aava-snackbar or custom error)
    - ContinueButton (aava-button)
    - CancelButton (aava-button)
  - TransferConfirmationDialog (aava-modal)
    - ConfirmTransferButton (aava-button)
    - BackButton (aava-button)
  - TransferSuccessDialog (aava-modal)
    - SuccessBadge (aava-badge)
    - ReturnToDashboardButton (aava-button)

**Screen: Spending Limit Edit**
- SpendingLimitEditPage
  - SidebarComponent
  - HeaderComponent
  - LimitEditForm (aava-default-card)
    - WeeklyLimitInput (aava-textbox)
    - ErrorBubble (aava-snackbar or custom error)
    - SaveLimitButton (aava-button)
    - CancelButton (aava-button)
  - LimitSuccessDialog (aava-modal)
    - SuccessBadge (aava-badge)
    - ReturnToDashboardButton (aava-button)

**Screen: Activity List**
- ActivityListPage
  - SidebarComponent
  - HeaderComponent
  - ActivityTabs (aava-tabs)
  - TransactionList (aava-timeline or custom list)
    - TransactionItem
      - TransactionBadge (aava-badge)
  - BackToDashboardButton (aava-button)

**Screen: Error Handling**
- ErrorDialog (aava-modal)
  - ErrorBubble (aava-snackbar)
  - BackButton (aava-button)

**Screen: Help/FAQ**
- HelpFAQPage
  - SidebarComponent
  - HeaderComponent
  - FAQCard (aava-default-card)
    - FAQItem
    - Divider (aava-divider)

---

## 6. Component Responsibilities

**SidebarComponent**
- Navigation between dashboard, youth account, fund transfer, limit edit, activity, help

**HeaderComponent**
- Search, notifications, avatar display

**ParentAccountCard / YouthAccountCard**
- Display account balances, account info, action buttons

**BalanceCard**
- Show youth account balance, last updated info

**WeeklyLimitCard**
- Display current weekly limit, edit/manage actions

**QuickActionsCard**
- Add funds, view activity

**RecentActivityCard**
- List recent transactions, show badges, view all button

**FundTransferForm**
- Input amount, select source, show errors, continue/cancel actions

**TransferConfirmationDialog / TransferSuccessDialog**
- Confirm transfer, show success, return to dashboard

**LimitEditForm / LimitSuccessDialog**
- Edit weekly limit, show success, return to dashboard

**ActivityTabs / TransactionList**
- Filter and display transactions

**ErrorDialog**
- Show error messages, guide resolution

**HelpFAQPage**
- Display FAQ items, educational tips

---

## 7. Data Flow / Props

**MainDashboardPage**
- ParentAccountCard (parentAccountData)
- YouthAccountCard (youthAccountData)
  - TransferFundsButton (onTransferFunds)

**YouthAccountDashboardPage**
- BalanceCard (youthAccountBalance)
- WeeklyLimitCard (weeklyLimit, onEditLimit, onManageLimit)
- QuickActionsCard (onAddFunds, onViewActivity)
- RecentActivityCard (activityList)
  - TransactionBadge (amount, type)
  - ViewAllButton (onViewAllActivity)

**FundTransferPage**
- FundTransferForm (amount, sourceAccount, onContinue, onCancel, error)
- TransferConfirmationDialog (transferDetails, onConfirm, onBack)
- TransferSuccessDialog (updatedBalance, onReturnToDashboard)

**SpendingLimitEditPage**
- LimitEditForm (weeklyLimit, onSave, onCancel, error)
- LimitSuccessDialog (newLimit, onReturnToDashboard)

**ActivityListPage**
- ActivityTabs (filter, onTabChange)
- TransactionList (transactions)
  - TransactionItem (date, merchant, amount, balance)
  - TransactionBadge (amount)
- BackToDashboardButton (onBack)

**ErrorDialog**
- ErrorBubble (errorMessage)
- BackButton (onBack)

**HelpFAQPage**
- FAQCard (faqItems)

---

## 8. Layout Structure

**Page Layout**
- SidebarComponent
- HeaderComponent
- Main Container
  - Screen-specific cards/forms/lists/dialogs

**Example: Youth Account Dashboard**
- SidebarComponent
- HeaderComponent
- Main Container
  - BalanceCard
  - WeeklyLimitCard
  - QuickActionsCard
  - RecentActivityCard

**Example: Fund Transfer**
- SidebarComponent
- HeaderComponent
- Main Container
  - FundTransferForm
  - TransferConfirmationDialog (modal)
  - TransferSuccessDialog (modal)

---

## 9. Component Mapping Table

| HTML Element                | Reusable Component         | Notes                         |
|----------------------------|---------------------------|-------------------------------|
| Card (account/activity)     | aava-default-card         | Use header/content/footer      |
| Button (actions)            | aava-button               | Variant, size, icon support    |
| Badge (transaction amount)  | aava-badge                | Neutral, success, warning      |
| Avatar (parent/guardian)    | aava-avatar               | Size, initials, image          |
| Sidebar navigation          | aava-sidebar              | Sectioned navigation           |
| Tabs (activity filter)      | aava-tabs                 | All/week/month                 |
| Dialog/Modal (confirmation) | aava-modal                | Success/error popups           |
| Input (amount, limit)       | aava-textbox, aava-select | Number/select inputs           |
| Error bubble/message        | aava-snackbar, aava-toast | Inline or modal error          |
| Divider                    | aava-divider              | Section separation             |
| Timeline/list (activity)    | aava-timeline             | Transaction history            |
| Stepper (fund transfer)     | aava-stepper-input        | Guided transfer flow           |

---

## 10. Notes & Recommendations
- All major UI elements are mapped to reusable components from the library
- No new custom components required unless for highly specialized visuals
- Accessibility, responsive design, and semantic structure are supported by component library
- Data flow aligns with parent-child relationships and prop passing
- Error handling and confirmation dialogs use modal/snackbar components
- Layout structure is modular and scalable for future enhancements

---

# END OF UI COMPONENT ARCHITECTURE
