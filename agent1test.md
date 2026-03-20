# UI Component Architecture for Youth Account Dashboard

## 1. Jira Requirement Summary

**Story Description:**
AS a parent or guardian I WANT to allocate and manage funds for my child’s youth account SO THAT I can teach financial responsibility while maintaining visibility and control over spending

**Acceptance Criteria:**
- Scenario 1 – Access youth account dashboard: Given the parent is logged into the banking web application When the parent navigates to the youth account section Then the system should display the youth account dashboard with current balance and recent activity
- Scenario 2 – Allocate funds to youth account: Given the parent is on the youth account dashboard When the parent selects “Add Funds” Then the system should allow the parent to transfer funds from their primary account to the youth account
- Scenario 3 – Set spending limit: Given the parent is viewing the youth account management section When the parent configures a weekly spending limit Then the system should save and display the limit on the dashboard
- Scenario 4 – View youth spending activity: Given the parent is viewing the youth account dashboard When the parent selects the activity section Then the system should display recent transactions made from the youth account
- Scenario 5 – Handle insufficient balance during fund allocation: Given the parent attempts to transfer funds When the selected parent account does not have sufficient balance Then the system should display an error message indicating insufficient funds

**UI Tasks / Subtasks:**
- Design youth account dashboard layout
- Design fund transfer interaction for youth account
- Design spending limit configuration interface
- Design youth account activity view

---

## 2. HTML Structure Summary

**Note:** HTML fetch failed (404 error). Unable to retrieve index.html from GitHub. UI structure inferred from Jira requirements and component documentation.

**Expected Layout (based on requirements):**
- Header (with navigation, user avatar, search bar)
- Main container (dashboard)
  - Current balance display
  - Add Funds button
  - Spending limit configuration
  - Recent activity/transaction list
  - Error snackbar/modal for insufficient funds
- Footer (optional)

---

## 3. Reusable Components from Library

**Extracted from documentation ZIP:**
- Header (AavaHeaderComponent)
- Card (AavaDefaultCardComponent, AavaCardHeaderComponent, AavaCardContentComponent, AavaCardFooterComponent, AavaCardActionsComponent)
- Button (AavaButtonComponent)
- Avatar (AavaAvatarsComponent)
- Tabs (AavaTabsComponent)
- Snackbar (SnackbarService)
- Modal (AavaModalComponent)
- Drawer (AavaDrawerComponent)
- Grid (AavaGridComponent)
- Timeline (AavaTimelineComponent)
- Chip-Tag (AavaTagComponent)
- Search-Bar (AavaSearchBarComponent)

---

## 4. Jira vs HTML Validation

- **Matching Elements:**
  - Dashboard, fund allocation, spending limit, activity view, error handling (all described in Jira)
- **Missing Elements:**
  - HTML structure not available (index.html fetch failed)
- **Extra Elements:**
  - None (no HTML to compare)

---

## 5. UI Component Architecture

**Screen:** Youth Account Dashboard

YouthAccountDashboardPage
├── HeaderComponent (AavaHeaderComponent)
│   ├── Logo
│   ├── NavigationTabs (AavaTabsComponent)
│   ├── SearchBar (AavaSearchBarComponent)
│   └── UserAvatar (AavaAvatarsComponent)
├── MainContainer
│   ├── BalanceCard (AavaDefaultCardComponent)
│   │   ├── CardHeader (AavaCardHeaderComponent)
│   │   │   └── BalanceDisplay
│   │   ├── CardContent (AavaCardContentComponent)
│   │   │   └── AccountDetails
│   │   └── CardFooter (AavaCardFooterComponent)
│   ├── AddFundsSection
│   │   ├── AddFundsButton (AavaButtonComponent)
│   │   └── FundTransferModal (AavaModalComponent)
│   ├── SpendingLimitSection
│   │   ├── SpendingLimitCard (AavaDefaultCardComponent)
│   │   │   ├── CardHeader (AavaCardHeaderComponent)
│   │   │   └── CardContent (AavaCardContentComponent)
│   │   └── LimitConfigButton (AavaButtonComponent)
│   │   └── LimitConfigDrawer (AavaDrawerComponent)
│   ├── ActivitySection
│   │   ├── ActivityTabs (AavaTabsComponent)
│   │   └── ActivityTimeline (AavaTimelineComponent)
│   │   └── ActivityCardList (AavaGridComponent)
│   │       ├── ActivityCard (AavaDefaultCardComponent)
│   │       │   ├── CardHeader (AavaCardHeaderComponent)
│   │       │   ├── CardContent (AavaCardContentComponent)
│   │       │   └── CardFooter (AavaCardFooterComponent)
│   │       └── ChipTag (AavaTagComponent)
│   └── ErrorSnackbar (SnackbarService)
└── FooterComponent (optional)

---

## 6. Component Responsibilities

**HeaderComponent**
- Displays logo, navigation tabs, search bar, and user avatar.

**BalanceCard**
- Shows current youth account balance and account details.

**AddFundsSection**
- Provides Add Funds button and modal for fund transfer interaction.

**SpendingLimitSection**
- Displays and configures weekly spending limit using card, button, and drawer.

**ActivitySection**
- Shows recent youth account transactions using tabs, timeline, and card grid.

**ErrorSnackbar**
- Displays error messages (e.g., insufficient funds) as transient notifications.

---

## 7. Data Flow / Props

YouthAccountDashboardPage
  -> HeaderComponent (userData, navigationTabs, searchQuery)
HeaderComponent
  -> UserAvatar (avatarUrl, profileText, badgeCount)
  -> NavigationTabs (tabs, activeTabId)
  -> SearchBar (searchQuery)
MainContainer
  -> BalanceCard (balance, accountDetails)
  -> AddFundsSection (parentAccount, youthAccount, transferAmount)
  -> SpendingLimitSection (spendingLimit, onLimitChange)
  -> ActivitySection (activityList, filterTabs)
  -> ErrorSnackbar (errorMessage)
ActivitySection
  -> ActivityTabs (tabs, activeTabId)
  -> ActivityTimeline (activityList)
  -> ActivityCardList (activityList)
ActivityCard
  -> ChipTag (transactionType, status)

---

## 8. Layout Structure

Page Layout
├── Header
│   ├── Logo
│   ├── Navigation Tabs
│   ├── Search Bar
│   └── User Avatar
├── Main Container
│   ├── Balance Card
│   ├── Add Funds Section
│   ├── Spending Limit Section
│   ├── Activity Section
│   │   ├── Activity Tabs
│   │   ├── Activity Timeline
│   │   └── Activity Card List
│   └── Error Snackbar
└── Footer (optional)

---

**Note:** All components are mapped to reusable AAVA Play library components wherever possible. No new custom components are proposed unless required by business logic.

**Missing HTML:** HTML structure could not be validated due to fetch failure. UI architecture is based on Jira requirements and component documentation.
