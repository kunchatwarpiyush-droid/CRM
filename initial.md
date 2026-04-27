# Requirements
## Summary
A full-featured CRM web application for a sales company built on UI Bakery (React/TypeScript/Tailwind/Shadcn) with mock data. The app covers the full sales lifecycle from Leads → Opportunities → Customers with a Kanban pipeline, reporting dashboards, appointment scheduling, communication logs, campaign tracking, and admin master-data management. It targets two roles — Admin and Salesperson — delivering a Zoho-style experience with sidebar navigation, CRUD modals, status color-coding, and CSV export.

## Use cases

- App Shell & Dashboard
  1) User opens the app and sees a sidebar with sections: Dashboard, Leads, Opportunities, Customers, Pipeline, Appointments, Communications, Campaigns, Reports, Master Data.
  2) Dashboard displays KPI cards: Total Leads, Open Leads, Opportunities, Customers (1178 pre-existing).
  3) Dashboard shows "Vertical Wise Sales" bar chart and "Salesperson Pipeline" bar chart.
  4) Dashboard shows a "Last Synced X minutes ago" indicator.
  5) Top bar includes a quick-action bar with shortcuts: Add Lead, Add Opportunity, Add Customer.

- Leads Management
  1) User navigates to Leads module and sees a searchable, filterable, paginated table of leads.
  2) User clicks "Add Lead" to open a modal form (Name, Phone, Email, Lead Source, Territory, Assigned Salesperson, Status).
  3) User submits the form; a new lead is saved to mock data with auto-timestamp and a toast confirmation is shown.
  4) User clicks a lead row to edit it in the same modal; changes are saved.
  5) User deletes a lead with confirmation dialog.
  6) User opens a lead's detail panel to add/view comments.
  7) Leads are color-coded by status (New, Contacted, Qualified, etc.).

- Opportunities Management
  1) User navigates to Opportunities and sees a table with fields: Linked Lead, Deal Value, Stage, Probability %, Expected Close Date.
  2) User adds/edits/deletes opportunities via modal form.
  3) User can add/view comments on each opportunity.
  4) Opportunity rows are color-coded by stage.

- Customers Management
  1) User navigates to Customers and sees a table with Name, Contact, Group, Territory.
  2) User adds/edits/deletes customers via modal form.
  3) Table supports search, filter by territory/group, and pagination.

- Sales Pipeline (Kanban)
  1) User navigates to Pipeline and sees a Kanban board with columns: Lead, Qualified, Proposal, Negotiation, Won, Lost.
  2) Each card shows lead/opportunity name, deal value, and assigned salesperson.
  3) User can drag-and-drop cards between columns (or use a "Move to Stage" dropdown as fallback).
  4) Column totals (count + deal value sum) are shown in column headers.

- Appointments & Communication Log
  1) User navigates to Appointments and sees a table of appointments (Date, Time, Assigned To, Notes) with add/edit/delete.
  2) User navigates to Communications and logs Call / Email / Follow-up entries linked to a lead or customer.
  3) Both modules support search, filter, and pagination.

- Campaigns Module
  1) User navigates to Campaigns and sees a list of campaigns.
  2) User creates a new campaign (Name, Start Date, End Date, Target).
  3) Campaign detail shows: Leads Generated, Conversions, Revenue.

- Reports & Analytics
  1) User navigates to Reports and sees a list: Sales Pipeline Analytics, Opportunity Summary by Stage, Prospects Engaged but Not Converted, First Response Time, Inactive Customers, Campaign Efficiency, Lead Owner Efficiency.
  2) User selects a report to view a chart and summary table.
  3) Custom Reports section shows category breakdowns: Audio Visual, AV2, Home Automation, IT Hardware, Rugged Computing, Security & Surveillance, Telecommunication — each with Winning % in Monthly / Yearly view toggle.
  4) Territory Wise Sales filter allows filtering revenue and conversion % by territory.

- Master Data (Admin Only)
  1) Admin navigates to Master Data and sees tabs: Territory, Customer Group, Contact, Prospect, Sales Person, Sales Stage, Lead Source.
  2) Admin adds/edits/deletes entries in each master-data list.
  3) Non-admin users do not see Master Data in the sidebar.

- Export & Utilities
  1) On any table view the user can click "Export CSV" to download the current filtered data as a CSV file.
  2) Every record stores a created/updated timestamp automatically.
  3) Status and stage changes are tracked with the assigned salesperson name.

## Plan

### App Shell & Dashboard
1. [x] Create app layout with a fixed left sidebar (Zoho-style) containing navigation links for all modules; add a top bar with quick-action buttons (Add Lead, Add Opportunity, Add Customer) and user info/logout.
2. [x] Implement client-side routing so each sidebar link renders the correct module view without page reload.
3. [x] Build the Dashboard page with four KPI cards (Total Leads, Open Leads, Opportunities, Customers) powered by mock data aggregations.
4. [x] Add a "Vertical Wise Sales" vertical bar chart (Recharts or inline SVG) showing revenue by vertical category.
5. [x] Add a "Salesperson Pipeline" horizontal bar chart showing open deal value per salesperson.
6. [x] Display a "Last Synced X minutes ago" label that updates every minute using a timestamp stored in state.

### Leads Management
1. [x] Create mock leads data array (≥15 records) with fields: id, name, phone, email, leadSource, territory, assignedSalesperson, status, createdAt, comments[].
2. [x] Build the Leads page with a data table: columns for all fields, status badge with color-coding (New=blue, Contacted=yellow, Qualified=green, Lost=red), search input, status filter dropdown, territory filter, pagination (10 per page).
3. [x] Build the Add/Edit Lead modal form using Shadcn Dialog + form inputs for all fields; on submit, upsert the mock data array and show a success toast.
4. [x] Add a Delete button with a Shadcn AlertDialog confirmation; on confirm remove from mock data and show toast.
5. [x] Add a Lead Detail side-panel (or expandable row) that shows lead info and a comments section: list of comments with author + timestamp, and a textarea + "Add Comment" button.

### Opportunities Management
1. [x] Create mock opportunities data array (≥10 records) with fields: id, linkedLeadId, linkedLeadName, dealValue, stage, probability, expectedCloseDate, createdAt, comments[].
2. [x] Build the Opportunities page with a data table; stage badge color-coding; search, stage filter, date range filter, pagination.
3. [x] Build Add/Edit Opportunity modal with all fields including a "Linked Lead" searchable select populated from leads mock data.
4. [x] Add Delete with confirmation and toast.
5. [x] Add comments panel same as Leads.

### Customers Management
1. [x] Create mock customers data array (≥20 records, 1178 total count shown in KPIs) with fields: id, name, contact, group, territory, createdAt.
2. [x] Build Customers page with table, search, group and territory filters, pagination.
3. [x] Build Add/Edit Customer modal and Delete with confirmation.

### Sales Pipeline (Kanban)
1. [x] Build the Kanban board component with six column cards (Lead, Qualified, Proposal, Negotiation, Won, Lost) derived from opportunities mock data grouped by stage.
2. [x] Each kanban card shows: lead/opportunity name, deal value formatted as currency, assigned salesperson avatar/initials.
3. [x] Show column header with stage name, card count, and total deal value sum.
4. [x] Implement drag-and-drop using HTML5 drag API (dragstart, dragover, drop) to move cards between columns and update the stage in mock data; show toast on move.
5. [x] Add a fallback "Move to Stage" select on each card for non-drag environments.

### Appointments & Communication Log
1. [x] Create mock appointments data (≥8 records) with fields: id, title, date, time, assignedTo, notes, createdAt.
2. [x] Build Appointments page with table, date filter, assignedTo filter, pagination; Add/Edit modal and Delete with confirmation.
3. [x] Create mock communications data (≥10 records) with fields: id, type (Call/Email/Follow-up), linkedTo, linkedType, subject, notes, date, createdAt.
4. [x] Build Communications page with table, type filter, search, pagination; Add/Edit modal and Delete with confirmation.

### Campaigns Module
1. [x] Create mock campaigns data (≥5 records) with fields: id, name, startDate, endDate, target, leadsGenerated, conversions, revenue, createdAt.
2. [x] Build Campaigns list page with table, search, date filter, pagination; Add/Edit modal (name, start/end dates, target) and Delete.
3. [x] Build Campaign Detail view showing KPI cards (Leads Generated, Conversions, Revenue, Conversion %) and a simple bar chart of monthly performance.

### Reports & Analytics
1. [x] Build a Reports landing page listing all 7 standard reports as clickable cards with icons and descriptions.
2. [x] Implement "Sales Pipeline Analytics" report: funnel/bar chart of lead counts and deal values per stage using mock data.
3. [x] Implement "Opportunity Summary by Stage" report: table grouped by stage with count, total deal value, average probability.
4. [x] Implement "Prospects Engaged but Not Converted" report: table of leads with status ≠ Won/Customer for >30 days.
5. [x] Implement remaining reports (First Response Time, Inactive Customers, Campaign Efficiency, Lead Owner Efficiency) as chart + table combos using mock data aggregations.
6. [x] Build Custom Reports section with a category selector (7 verticals) and Monthly/Yearly toggle; display winning percentage as a donut chart and summary table with mock data.
7. [x] Build Territory Wise Sales filter panel: territory multiselect that filters a revenue bar chart and conversion % table.

### Master Data (Admin Only)
1. [x] Create mock master data stores for: Territory, Customer Group, Contact, Prospect, Sales Person, Sales Stage, Lead Source — each as a simple array of {id, name, ...}.
2. [x] Build the Master Data page with a tab for each entity showing a list table with Add/Edit/Delete inline.
3. [x] Hide the Master Data sidebar link for non-Admin users based on the current user's role stored in app state (mock user role toggle for demo).

### Export & Utilities
1. [x] Implement a reusable `exportToCSV(data, filename)` utility function that converts an array of objects to CSV and triggers a browser download.
2. [x] Add an "Export CSV" button to all main table pages (Leads, Opportunities, Customers, Appointments, Communications, Campaigns).
3. [x] Ensure every record creation/update sets a `createdAt` / `updatedAt` ISO timestamp automatically in the mock data mutation functions.
4. [x] Implement toast notification system (Shadcn Toaster) for all create/update/delete/export actions with appropriate variant (success/error).
