# UI Component Implementation Specifications

---

# 1. YouthAccountDashboardPage

## Component Name

YouthAccountDashboardPage

## Purpose

Acts as the main container for the Youth Account Dashboard screen. It composes the layout by integrating Header, Sidebar, Main Content, and Footer components while managing feature data displayed in the feature cards.

## Dependencies

* HeaderComponent

* SidebarComponent

* FeatureCardComponent

* FooterComponent

* GridComponent

## Library Components Used

* Grid

* Card

* Button

* Icon

# TypeScript Specification

Inputs: None

Outputs: None

State:

features = [
  {
    title: 'Data Extraction Invoice',
    description: 'Extract structured data from invoices automatically.',
    icon: 'icon-invoice',
    actionLabel: 'Try Now'
  },
  {
    title: 'Financial Extraction',
    description: 'Extract key financial information from documents.',
    icon: 'icon-finance',
    actionLabel: 'Try Now'
  },
  {
    title: 'Compare Documents',
    description: 'Compare documents to identify differences.',
    icon: 'icon-compare',
    actionLabel: 'Try Now'
  }
];

# Methods

handleFeatureAction(feature) {
   console.log("Feature selected:", feature);
}

# HTML Structure

<app-header></app-header>
<div class="dashboard-layout">
  <app-sidebar></app-sidebar>
  <div class="main-content">
    <h1 class="page-title">Youth Account Dashboard</h1>
    <div class="feature-grid">
      <app-feature-card *ngFor="let feature of features" [feature]="feature" (action)="handleFeatureAction(feature)"></app-feature-card>
    </div>
  </div>
</div>
<app-footer></app-footer>

# CSS Specification

.dashboard-layout {
  display: flex;
  height: calc(100vh - 64px);
}

.main-content {
  flex: 1;
  padding: 32px;
}

.page-title {
  font-size: 28px;
  font-weight: 600;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  margin-top: 24px;
}

@media (max-width: 900px) {
  .feature-grid {
    grid-template-columns: 1fr;
  }
  .main-content {
    padding: 16px;
  }
}
