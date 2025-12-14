# JIMSAN Outgrowers Management System - Implementation Plan

## Executive Summary

This document outlines a comprehensive upgrade plan for the JIMSAN Outgrowers Management System. The upgrade transforms the current multi-purpose agricultural platform into a focused, robust Outgrower Management System that accurately reflects JIMSAN Smart Agri Limited's operational workflow based on the manual forms analysis.

**Key Transformation Goals:**
1. Remove E-commerce and Consultancy modules (out of scope)
2. Implement Lead Farmer hierarchy (critical business model)
3. Introduce loan-based input distribution with recovery tracking
4. Add comprehensive inventory management with supplier tracking
5. Implement role-based access aligned with organizational structure

---

## 1. Analysis Summary

### 1.1 Manual Workflow Forms Identified

| Form | Purpose | Digital Equivalent Needed |
|------|---------|---------------------------|
| Farmers Performance Progress Form | Weekly crop monitoring (weeks 1-4, 5-8, 9-12, 13-16) with disease tracking | Crop Progress Module |
| Lead Farmer Cluster Inputs Evaluation | Track inputs distributed to farmers under a lead farmer | Input Distribution Module |
| Lead Farmer Loan Inputs Evaluation | Loan request for seeds, fertilizers, chemicals with cost calculation | Loan Request Module |
| Loan Recovery Form | Track loan repayment through product yield purchase | Loan Recovery Module |
| Goods Received Note | Inventory receipt from suppliers | Goods Received Module |
| Store Card | Track inventory in/out/balance per item | Inventory Ledger |
| Official Receipt | Payment receipt generation | Receipt Module |
| Sales Invoice | Customer invoicing | Invoice Module |
| Local Purchase Calculation | Purchase cost calculation with markup | Purchase Calculation Module |

### 1.2 Current System Gaps

| Gap | Current State | Required State |
|-----|---------------|----------------|
| **Lead Farmer Hierarchy** | Direct farmer management | Farmers under Lead Farmers |
| **Loan Tracking** | Simple contract system | Full loan lifecycle (request, disbursement, recovery) |
| **User Roles** | admin, field_officer, input_manager, finance_officer | super_admin, admin, finance_officer, lead_farmer, farmer |
| **Supplier Management** | None | Full supplier tracking with GRN |
| **Inventory Ledger** | Basic stock count | Full in/out/balance tracking per item |
| **Loan Recovery** | None | Product yield purchase for loan recovery |
| **E-commerce Module** | Present | To be removed |
| **Consultancy Module** | Present | To be removed |
| **Inspector Role** | Field officer only | Dedicated inspector for crop monitoring |
| **Multi-level Approvals** | None | Farmer > Lead Farmer > Inspector > Manager workflow |

### 1.3 Manual System Weaknesses to Address

1. **Paper-based tracking** - Prone to loss, damage, and manipulation
2. **Manual calculations** - Error-prone for loan values and recovery
3. **No real-time visibility** - Delayed reporting and decision making
4. **Signature verification** - Cannot validate authenticity remotely
5. **Data aggregation** - Difficult to consolidate data across clusters
6. **Historical tracking** - Limited ability to track changes over time
7. **No alerting** - Missing deadlines and low stock unnoticed

---

## 2. Proposed System Architecture

### 2.1 Module Structure

```
JIMSAN Outgrowers Management System
├── Core Modules
│   ├── Authentication & Authorization
│   ├── User Management (5 roles)
│   ├── Dashboard (role-specific)
│   └── System Settings
│
├── Outgrower Management
│   ├── Lead Farmer Management
│   ├── Farmer Management
│   ├── Cluster Management
│   └── Farm Registration
│
├── Contract & Loan Module
│   ├── Farming Seasons
│   ├── Loan Input Requests
│   ├── Loan Approval Workflow
│   ├── Input Allocation
│   └── Loan Tracking
│
├── Inventory Management
│   ├── Supplier Management
│   ├── Goods Received Notes (GRN)
│   ├── Inventory Items (Seeds, Fertilizers, Chemicals)
│   ├── Store Cards (Ledger)
│   └── Stock Movements
│
├── Distribution Management
│   ├── Input Distribution Planning
│   ├── Distribution Execution
│   ├── Delivery Confirmation
│   └── Distribution Reports
│
├── Crop Monitoring
│   ├── Weekly Progress Reports
│   ├── Crop Health Tracking
│   ├── Disease/Defect Management
│   ├── Inspector Assignments
│   └── Photo Documentation
│
├── Harvest & Recovery
│   ├── Harvest Recording
│   ├── Yield Assessment
│   ├── Loan Recovery Processing
│   ├── Balance Calculations
│   └── Farmer Settlement
│
├── Financial Management
│   ├── Receipt Generation
│   ├── Invoice Management
│   ├── Payment Processing
│   ├── Local Purchase Calculations
│   └── Financial Reports
│
└── Reporting & Analytics
    ├── Dashboard Analytics
    ├── Cluster Performance
    ├── Lead Farmer Reports
    ├── Loan Portfolio Reports
    └── Export (PDF, Excel)
```

### 2.2 User Roles & Permissions

| Role | Description | Key Permissions |
|------|-------------|-----------------|
| **Super Administrator** | System owner, full access | All CRUD operations, user management, system settings, audit logs |
| **Admin** | Day-to-day operations manager | Manage farmers, contracts, distributions, view reports (no system settings) |
| **Finance Officer** | Financial operations | Process payments, generate receipts/invoices, loan recovery, financial reports |
| **Lead Farmer** | Cluster coordinator | View/manage farmers in cluster, submit input requests, view distributions, submit progress reports |
| **Farmer** | End user (limited access) | View own profile, contract status, input received, payment history |

---

## 3. Database Schema Changes

### 3.1 Tables to Remove

```sql
-- E-commerce tables
DROP TABLE IF EXISTS products;
DROP TABLE IF EXISTS product_categories;
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS order_items;

-- Consultancy tables
DROP TABLE IF EXISTS consultancy_services;
DROP TABLE IF EXISTS consultants;
DROP TABLE IF EXISTS consultation_bookings;
```

### 3.2 New Tables to Create

#### Lead Farmers Table
```sql
CREATE TABLE lead_farmers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    lead_farmer_code VARCHAR(20) UNIQUE NOT NULL,
    user_id INT NULL,  -- Links to users table for portal access
    full_name VARCHAR(100) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    email VARCHAR(100),
    address TEXT,
    state_id INT NOT NULL,
    lga_id INT NOT NULL,
    bank_name VARCHAR(100),
    account_number VARCHAR(20),
    account_name VARCHAR(100),
    photo_path VARCHAR(255),
    is_active TINYINT(1) DEFAULT 1,
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (state_id) REFERENCES states(id),
    FOREIGN KEY (lga_id) REFERENCES lgas(id),
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (created_by) REFERENCES users(id)
);
```

#### Farmer-Lead Farmer Relationship
```sql
ALTER TABLE farmers ADD COLUMN lead_farmer_id INT NULL;
ALTER TABLE farmers ADD FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id);
```

#### Suppliers Table
```sql
CREATE TABLE suppliers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    supplier_code VARCHAR(20) UNIQUE NOT NULL,
    company_name VARCHAR(150) NOT NULL,
    contact_person VARCHAR(100),
    phone VARCHAR(20) NOT NULL,
    email VARCHAR(100),
    address TEXT,
    state_id INT,
    lga_id INT,
    bank_name VARCHAR(100),
    account_number VARCHAR(20),
    account_name VARCHAR(100),
    tax_id VARCHAR(50),
    is_active TINYINT(1) DEFAULT 1,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

#### Goods Received Notes
```sql
CREATE TABLE goods_received_notes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    grn_number VARCHAR(30) UNIQUE NOT NULL,
    supplier_id INT NOT NULL,
    received_date DATE NOT NULL,
    received_by INT NOT NULL,
    checked_by INT,
    total_items INT DEFAULT 0,
    notes TEXT,
    status ENUM('pending', 'verified', 'completed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (supplier_id) REFERENCES suppliers(id),
    FOREIGN KEY (received_by) REFERENCES users(id),
    FOREIGN KEY (checked_by) REFERENCES users(id)
);
```

#### GRN Items
```sql
CREATE TABLE grn_items (
    id INT PRIMARY KEY AUTO_INCREMENT,
    grn_id INT NOT NULL,
    item_type ENUM('seeds', 'fertilizer', 'chemical') NOT NULL,
    item_id INT NOT NULL,
    item_code VARCHAR(50),
    description VARCHAR(255),
    quantity_ordered DECIMAL(10,2) NOT NULL,
    quantity_received DECIMAL(10,2) NOT NULL,
    quantity_outstanding DECIMAL(10,2) GENERATED ALWAYS AS (quantity_ordered - quantity_received) STORED,
    unit_price DECIMAL(12,2),
    total_value DECIMAL(12,2) GENERATED ALWAYS AS (quantity_received * unit_price) STORED,
    remarks TEXT,
    FOREIGN KEY (grn_id) REFERENCES goods_received_notes(id) ON DELETE CASCADE
);
```

#### Loan Input Requests
```sql
CREATE TABLE loan_input_requests (
    id INT PRIMARY KEY AUTO_INCREMENT,
    request_number VARCHAR(30) UNIQUE NOT NULL,
    lead_farmer_id INT NOT NULL,
    season_id INT NOT NULL,
    total_farmers INT NOT NULL,
    total_hectares DECIMAL(10,2) NOT NULL,

    -- Seed Requests (JSON for flexibility)
    seed_requests JSON,  -- {"maize": 100, "rice": 50, "soya_beans": 0, ...}

    -- Fertilizer Requests
    fertilizer_requests JSON,  -- {"npk": 200, "urea": 100, "others": "..."}

    -- Agro Chemical Requests
    chemical_requests TEXT,

    -- Calculated Values (office use)
    total_seed_value DECIMAL(14,2) DEFAULT 0,
    total_fertilizer_value DECIMAL(14,2) DEFAULT 0,
    total_chemical_value DECIMAL(14,2) DEFAULT 0,
    grand_total DECIMAL(14,2) DEFAULT 0,

    -- Workflow
    status ENUM('draft', 'submitted', 'under_review', 'approved', 'rejected', 'disbursed') DEFAULT 'draft',
    submitted_at TIMESTAMP NULL,
    reviewed_by INT,
    reviewed_at TIMESTAMP NULL,
    approved_by INT,
    approved_at TIMESTAMP NULL,
    approval_notes TEXT,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id),
    FOREIGN KEY (season_id) REFERENCES farming_seasons(id),
    FOREIGN KEY (reviewed_by) REFERENCES users(id),
    FOREIGN KEY (approved_by) REFERENCES users(id)
);
```

#### Cluster Input Distributions
```sql
CREATE TABLE cluster_input_distributions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    distribution_number VARCHAR(30) UNIQUE NOT NULL,
    loan_request_id INT NOT NULL,
    lead_farmer_id INT NOT NULL,
    farmer_id INT NOT NULL,

    -- Seed Distribution
    seed_type VARCHAR(50),
    seed_quantity_kg DECIMAL(10,2) DEFAULT 0,
    seed_value DECIMAL(12,2) DEFAULT 0,

    -- Fertilizer Distribution
    npk_bags DECIMAL(10,2) DEFAULT 0,
    urea_bags DECIMAL(10,2) DEFAULT 0,
    other_fertilizer VARCHAR(100),
    other_fertilizer_qty DECIMAL(10,2) DEFAULT 0,
    fertilizer_value DECIMAL(12,2) DEFAULT 0,

    -- Chemical Distribution
    chemical_type VARCHAR(100),
    chemical_quantity DECIMAL(10,2) DEFAULT 0,
    chemical_value DECIMAL(12,2) DEFAULT 0,

    total_value DECIMAL(14,2) DEFAULT 0,

    distributed_by INT,
    distribution_date DATE,
    farmer_signature TINYINT(1) DEFAULT 0,
    lead_farmer_signature TINYINT(1) DEFAULT 0,
    remarks TEXT,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (loan_request_id) REFERENCES loan_input_requests(id),
    FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id),
    FOREIGN KEY (farmer_id) REFERENCES farmers(id),
    FOREIGN KEY (distributed_by) REFERENCES users(id)
);
```

#### Crop Progress Reports
```sql
CREATE TABLE crop_progress_reports (
    id INT PRIMARY KEY AUTO_INCREMENT,
    report_number VARCHAR(30) UNIQUE NOT NULL,
    farmer_id INT NOT NULL,
    lead_farmer_id INT NOT NULL,
    season_id INT NOT NULL,

    -- Farm Details
    farm_location VARCHAR(255),
    hectares DECIMAL(10,2),
    crop_type VARCHAR(50),
    date_planted DATE,
    fertilizer_application_date DATE,
    chemical_application_date DATE,

    -- Weekly Progress (JSON structure)
    week_1_4 JSON,  -- {"crop_health": "", "observation": "", "comments": ""}
    week_5_8 JSON,
    week_9_12 JSON,
    week_13_16 JSON,

    -- Crop Defects
    defects JSON,  -- [{"disease": "", "treatment": "", "preventive_measures": "", "action_taken": "", "remarks": ""}]

    inspector_id INT,
    inspector_comments TEXT,
    jimsan_official_comments TEXT,

    -- Signatures
    farmer_signed_at TIMESTAMP NULL,
    lead_farmer_signed_at TIMESTAMP NULL,
    inspector_signed_at TIMESTAMP NULL,

    status ENUM('draft', 'submitted', 'reviewed', 'completed') DEFAULT 'draft',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    FOREIGN KEY (farmer_id) REFERENCES farmers(id),
    FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id),
    FOREIGN KEY (season_id) REFERENCES farming_seasons(id),
    FOREIGN KEY (inspector_id) REFERENCES users(id)
);
```

#### Loan Recovery Records
```sql
CREATE TABLE loan_recovery_records (
    id INT PRIMARY KEY AUTO_INCREMENT,
    recovery_number VARCHAR(30) UNIQUE NOT NULL,
    lead_farmer_id INT NOT NULL,
    season_id INT NOT NULL,
    loan_request_id INT NOT NULL,

    -- Lead Farmer Info (snapshot)
    contact_address TEXT,
    total_farmers INT,
    total_hectares DECIMAL(10,2),

    -- Recovery Items (products purchased)
    recovery_items JSON,  -- [{"product_type": "", "yield_kg": 0, "purchase_price": 0, "total": 0}]

    -- Summary
    total_input_value DECIMAL(14,2) NOT NULL,  -- Original loan amount
    total_output_value DECIMAL(14,2) NOT NULL,  -- Value of products recovered
    balance_outstanding DECIMAL(14,2) GENERATED ALWAYS AS (total_input_value - total_output_value) STORED,

    lead_farmer_comment TEXT,
    managing_director_comment TEXT,

    -- Signatures
    lead_farmer_signed_at TIMESTAMP NULL,
    md_signed_at TIMESTAMP NULL,

    status ENUM('draft', 'submitted', 'under_review', 'approved', 'settled') DEFAULT 'draft',
    settlement_date DATE,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

    FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id),
    FOREIGN KEY (season_id) REFERENCES farming_seasons(id),
    FOREIGN KEY (loan_request_id) REFERENCES loan_input_requests(id)
);
```

#### Store Cards (Inventory Ledger)
```sql
CREATE TABLE store_cards (
    id INT PRIMARY KEY AUTO_INCREMENT,
    item_type ENUM('seeds', 'fertilizer', 'chemical', 'equipment') NOT NULL,
    item_id INT NOT NULL,
    item_name VARCHAR(100) NOT NULL,
    item_store_number VARCHAR(50),

    -- Opening balance
    opening_balance DECIMAL(12,2) DEFAULT 0,
    opening_balance_date DATE,

    is_active TINYINT(1) DEFAULT 1,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    UNIQUE KEY unique_item (item_type, item_id)
);
```

#### Store Card Transactions
```sql
CREATE TABLE store_card_transactions (
    id INT PRIMARY KEY AUTO_INCREMENT,
    store_card_id INT NOT NULL,
    transaction_date DATE NOT NULL,
    voucher_number VARCHAR(50),
    description VARCHAR(255),
    quantity_in DECIMAL(12,2) DEFAULT 0,
    quantity_out DECIMAL(12,2) DEFAULT 0,
    balance DECIMAL(12,2) NOT NULL,
    reference_type ENUM('grn', 'distribution', 'adjustment', 'return') NOT NULL,
    reference_id INT,
    recorded_by INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (store_card_id) REFERENCES store_cards(id),
    FOREIGN KEY (recorded_by) REFERENCES users(id)
);
```

#### Official Receipts
```sql
CREATE TABLE official_receipts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    receipt_number VARCHAR(30) UNIQUE NOT NULL,
    received_from VARCHAR(150) NOT NULL,
    amount DECIMAL(14,2) NOT NULL,
    amount_in_words VARCHAR(255),
    payment_for TEXT NOT NULL,

    payment_method ENUM('cash', 'cheque', 'bank_transfer', 'pos') NOT NULL,
    amount_due DECIMAL(14,2),
    amount_paid DECIMAL(14,2),
    balance DECIMAL(14,2) GENERATED ALWAYS AS (amount_due - amount_paid) STORED,
    payment_type ENUM('full', 'part') DEFAULT 'full',

    received_by INT NOT NULL,
    manager_approved_by INT,

    receipt_date DATE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (received_by) REFERENCES users(id),
    FOREIGN KEY (manager_approved_by) REFERENCES users(id)
);
```

#### Sales Invoices
```sql
CREATE TABLE sales_invoices (
    id INT PRIMARY KEY AUTO_INCREMENT,
    invoice_number VARCHAR(30) UNIQUE NOT NULL,
    customer_name VARCHAR(150) NOT NULL,
    customer_address TEXT,
    customer_phone VARCHAR(20),

    invoice_date DATE NOT NULL,
    terms VARCHAR(100),
    due_date DATE,

    -- Items stored as JSON
    items JSON,  -- [{"description": "", "qty_kg": 0, "unit_price": 0, "amount": 0}]

    subtotal DECIMAL(14,2) NOT NULL,
    discount_allowed DECIMAL(14,2) DEFAULT 0,
    total_amount DECIMAL(14,2) NOT NULL,
    total_in_words VARCHAR(255),

    bank_details TEXT,

    status ENUM('draft', 'sent', 'paid', 'overdue', 'cancelled') DEFAULT 'draft',

    created_by INT NOT NULL,
    approved_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (created_by) REFERENCES users(id),
    FOREIGN KEY (approved_by) REFERENCES users(id)
);
```

#### Local Purchase Calculations
```sql
CREATE TABLE local_purchase_calculations (
    id INT PRIMARY KEY AUTO_INCREMENT,
    lpc_number VARCHAR(30) UNIQUE NOT NULL,
    lpo_number VARCHAR(30),  -- Reference to purchase order
    supplier_farmer_name VARCHAR(150) NOT NULL,

    calculation_date DATE NOT NULL,

    -- Items
    items JSON,  -- [{"description": "", "qty_kg": 0, "unit_cost": 0, "date": "", "actual_cost": 0, "markup": 0, "total_cost": 0}]

    total_amount DECIMAL(14,2) NOT NULL,
    total_in_words VARCHAR(255),

    store_officer_id INT,
    manager_id INT,

    status ENUM('draft', 'approved', 'processed') DEFAULT 'draft',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (store_officer_id) REFERENCES users(id),
    FOREIGN KEY (manager_id) REFERENCES users(id)
);
```

### 3.3 Table Modifications

#### Users Table - Update Role ENUM
```sql
ALTER TABLE users
MODIFY COLUMN role ENUM('super_admin', 'admin', 'finance_officer', 'inspector', 'lead_farmer', 'farmer')
NOT NULL DEFAULT 'farmer';

-- Add new columns
ALTER TABLE users ADD COLUMN lead_farmer_id INT NULL;
ALTER TABLE users ADD COLUMN farmer_id INT NULL;
ALTER TABLE users ADD FOREIGN KEY (lead_farmer_id) REFERENCES lead_farmers(id);
ALTER TABLE users ADD FOREIGN KEY (farmer_id) REFERENCES farmers(id);
```

---

## 4. Implementation Phases

### Phase 1: Foundation & Cleanup (Priority: Critical)

**Objective:** Remove unnecessary modules and establish base structure

**Tasks:**
1. **Remove E-commerce Module**
   - Delete `/ecommerce/` directory
   - Drop e-commerce database tables
   - Remove e-commerce references from navigation
   - Clean up dashboard statistics

2. **Remove Consultancy Module**
   - Delete `/consultancy/` directory
   - Drop consultancy database tables
   - Remove consultancy references from navigation
   - Clean up dashboard statistics

3. **Update User Role System**
   - Modify users table role enum
   - Update authentication system
   - Create permission matrix
   - Update all permission checks

4. **Create Lead Farmer Module**
   - Create lead_farmers table
   - Build Lead Farmer CRUD pages
   - Update farmers table (add lead_farmer_id)
   - Build cluster assignment interface

**Deliverables:**
- Clean codebase without e-commerce/consultancy
- Working Lead Farmer management
- Updated user roles
- Farmer-Lead Farmer relationship

### Phase 2: Loan & Input Management (Priority: High)

**Objective:** Implement loan request and input distribution workflow

**Tasks:**
1. **Supplier Management**
   - Create suppliers table
   - Build Supplier CRUD pages
   - Supplier listing and search

2. **Goods Received Notes (GRN)**
   - Create GRN tables
   - Build GRN creation form
   - GRN item management
   - GRN verification workflow

3. **Loan Input Request System**
   - Create loan_input_requests table
   - Build request form (mirrors manual form)
   - Approval workflow (Lead Farmer > Admin > Finance)
   - Request tracking dashboard

4. **Cluster Input Distribution**
   - Create cluster_input_distributions table
   - Distribution planning interface
   - Per-farmer distribution recording
   - Digital signature capture
   - Distribution confirmation

**Deliverables:**
- Supplier management system
- GRN processing workflow
- Loan request submission and approval
- Input distribution tracking

### Phase 3: Inventory & Store Management (Priority: High)

**Objective:** Implement comprehensive inventory tracking

**Tasks:**
1. **Store Card System**
   - Create store_cards and transactions tables
   - Automatic card creation on GRN
   - Transaction recording interface
   - Running balance calculations

2. **Inventory Dashboard**
   - Real-time stock levels
   - Low stock alerts
   - Stock movement history
   - Item-wise ledger view

3. **Integration Points**
   - Auto-deduct on distribution
   - Auto-add on GRN completion
   - Stock adjustment interface
   - Stock take functionality

**Deliverables:**
- Store card system
- Inventory ledger
- Automated stock updates
- Stock reports

### Phase 4: Crop Monitoring (Priority: Medium)

**Objective:** Implement weekly progress tracking and inspection

**Tasks:**
1. **Progress Report Module**
   - Create crop_progress_reports table
   - Weekly report form (Week 1-4, 5-8, etc.)
   - Crop health indicators
   - Disease/defect tracking

2. **Inspector Assignment**
   - Assign inspectors to farmers/clusters
   - Inspector mobile-friendly interface
   - Photo upload capability
   - GPS location capture

3. **Approval Workflow**
   - Farmer submission
   - Lead Farmer verification
   - Inspector review
   - JIMSAN official comments

**Deliverables:**
- Crop progress reporting
- Multi-stage approval workflow
- Photo documentation
- Inspector dashboard

### Phase 5: Harvest & Loan Recovery (Priority: High)

**Objective:** Complete the loan lifecycle with recovery

**Tasks:**
1. **Harvest Recording Enhancement**
   - Link to farmer contracts
   - Yield vs expected comparison
   - Quality grading
   - Photo documentation

2. **Loan Recovery System**
   - Create loan_recovery_records table
   - Recovery form (mirrors manual)
   - Product purchase recording
   - Balance calculation
   - Settlement workflow

3. **Farmer Settlement**
   - Net payment calculation
   - Payment processing
   - Receipt generation
   - Settlement reports

**Deliverables:**
- Enhanced harvest recording
- Loan recovery processing
- Automatic balance calculations
- Settlement reports

### Phase 6: Financial Documents (Priority: Medium)

**Objective:** Generate financial documents

**Tasks:**
1. **Receipt Generation**
   - Create official_receipts table
   - Receipt form and preview
   - PDF generation
   - Receipt numbering

2. **Invoice System**
   - Create sales_invoices table
   - Invoice creation interface
   - PDF generation
   - Payment tracking

3. **Local Purchase Calculation**
   - Create LPC table
   - LPC form with markup calculation
   - PDF generation
   - Integration with payments

**Deliverables:**
- Receipt generation
- Invoice management
- LPC processing
- PDF exports

### Phase 7: Reporting & Analytics (Priority: Medium)

**Objective:** Comprehensive reporting system

**Tasks:**
1. **Dashboard Enhancement**
   - Role-specific dashboards
   - Key metrics widgets
   - Quick action buttons
   - Recent activity feed

2. **Report Modules**
   - Lead Farmer performance
   - Cluster analysis
   - Loan portfolio status
   - Recovery rates
   - Inventory reports
   - Financial summaries

3. **Export Functionality**
   - PDF report generation
   - Excel export
   - Date range filtering
   - Scheduled reports

**Deliverables:**
- Role-based dashboards
- Comprehensive reports
- Export capabilities

---

## 5. Technical Specifications

### 5.1 Technology Stack (Retain)

| Component | Technology |
|-----------|------------|
| Backend | PHP 8.0+ |
| Database | MySQL 8.0+ |
| Frontend | Bootstrap 5.3, JavaScript ES6+ |
| Icons | Font Awesome 6 |
| Charts | Chart.js |
| Tables | DataTables |
| PDF | TCPDF or Dompdf |
| Excel | PhpSpreadsheet |

### 5.2 File Structure Changes

```
JIMSAN/
├── api/
│   ├── lead-farmers.php       [NEW]
│   ├── suppliers.php          [NEW]
│   ├── grn.php                [NEW]
│   ├── loan-requests.php      [NEW]
│   ├── distributions.php      [MODIFY]
│   ├── crop-progress.php      [NEW]
│   ├── loan-recovery.php      [NEW]
│   ├── receipts.php           [NEW]
│   ├── invoices.php           [NEW]
│   └── store-cards.php        [NEW]
│
├── lead-farmers/              [NEW]
│   ├── index.php
│   ├── add.php
│   ├── view.php
│   ├── edit.php
│   └── clusters.php
│
├── suppliers/                 [NEW]
│   ├── index.php
│   ├── add.php
│   └── view.php
│
├── grn/                       [NEW]
│   ├── index.php
│   ├── add.php
│   ├── view.php
│   └── verify.php
│
├── loan-requests/             [NEW]
│   ├── index.php
│   ├── add.php
│   ├── view.php
│   └── approve.php
│
├── crop-progress/             [NEW]
│   ├── index.php
│   ├── add.php
│   ├── view.php
│   └── review.php
│
├── loan-recovery/             [NEW]
│   ├── index.php
│   ├── add.php
│   ├── view.php
│   └── settle.php
│
├── store-cards/               [NEW]
│   ├── index.php
│   ├── view.php
│   └── transactions.php
│
├── receipts/                  [NEW]
│   ├── index.php
│   ├── add.php
│   └── print.php
│
├── invoices/                  [NEW]
│   ├── index.php
│   ├── add.php
│   └── print.php
│
├── ecommerce/                 [DELETE]
├── consultancy/               [DELETE]
│
├── farmers/                   [MODIFY - add lead_farmer filter]
├── contracts/                 [MODIFY - link to loan system]
├── distributions/             [MODIFY - cluster-based]
├── harvests/                  [MODIFY - link to recovery]
├── monitoring/                [MODIFY - progress-based]
└── inventory/                 [MODIFY - store card integration]
```

### 5.3 Permission Matrix

| Permission | Super Admin | Admin | Finance | Inspector | Lead Farmer | Farmer |
|------------|:-----------:|:-----:|:-------:|:---------:|:-----------:|:------:|
| User Management | Yes | No | No | No | No | No |
| System Settings | Yes | No | No | No | No | No |
| Lead Farmer CRUD | Yes | Yes | No | No | No | No |
| Farmer CRUD | Yes | Yes | No | No | View Own | View Own |
| Supplier CRUD | Yes | Yes | No | No | No | No |
| GRN Management | Yes | Yes | No | No | No | No |
| Loan Requests | Yes | Approve | View | No | Submit | View Own |
| Input Distribution | Yes | Yes | View | No | View Own | View Own |
| Crop Progress | Yes | View | No | Edit | Submit | View Own |
| Loan Recovery | Yes | Yes | Process | No | View Own | View Own |
| Receipts | Yes | Yes | Yes | No | No | No |
| Invoices | Yes | Yes | Yes | No | No | No |
| Store Cards | Yes | Yes | View | No | No | No |
| Reports | All | All | Financial | Monitoring | Cluster | Own |

---

## 6. Migration Strategy

### 6.1 Data Migration

1. **Backup Current Database**
   ```bash
   mysqldump -u root -p msnng_jimsan > backup_$(date +%Y%m%d).sql
   ```

2. **Create Migration Script**
   - Identify existing farmers
   - Group farmers by location for cluster creation
   - Create placeholder lead farmers
   - Assign farmers to lead farmers

3. **Migrate Existing Data**
   - Preserve farmer records
   - Convert existing contracts to loan format
   - Migrate inventory to store card format
   - Preserve monitoring reports

### 6.2 Code Migration

1. **Branch Strategy**
   - Create feature branch: `feature/outgrower-upgrade`
   - Implement changes incrementally
   - Test thoroughly before merge

2. **Deployment Steps**
   - Put site in maintenance mode
   - Backup database
   - Run migrations
   - Deploy code changes
   - Clear caches
   - Test critical paths
   - Enable site

---

## 7. UI/UX Improvements

### 7.1 Design Principles

1. **Simplicity** - Reduce complexity for field users
2. **Mobile-First** - Optimize for tablet/phone use in field
3. **Clear Workflow** - Visual status indicators
4. **Quick Actions** - Reduce clicks for common tasks

### 7.2 Key UI Components

1. **Status Badges**
   - Draft (Gray)
   - Submitted (Blue)
   - Under Review (Yellow)
   - Approved (Green)
   - Rejected (Red)

2. **Workflow Indicators**
   ```
   [Draft] → [Submitted] → [Reviewed] → [Approved] → [Disbursed]
   ```

3. **Dashboard Widgets**
   - Pending approvals count
   - Low stock alerts
   - Outstanding loans
   - Recent activities

---

## 8. Testing Strategy

### 8.1 Test Categories

1. **Unit Tests** - Individual functions
2. **Integration Tests** - Module interactions
3. **User Acceptance Tests** - Business workflow validation
4. **Security Tests** - Permission and access control

### 8.2 Test Scenarios

| Scenario | Expected Outcome |
|----------|------------------|
| Lead Farmer creates loan request | Request saved with draft status |
| Admin approves loan request | Status changes, notification sent |
| Distribution recorded | Stock deducted, store card updated |
| Harvest recorded | Linked to contract, recovery enabled |
| Loan recovery processed | Balance calculated correctly |
| Receipt generated | PDF created, number sequential |

---

## 9. Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Data loss during migration | High | Multiple backups, staged migration |
| User resistance to change | Medium | Training, gradual rollout |
| Performance issues | Medium | Database optimization, caching |
| Security vulnerabilities | High | Code review, penetration testing |
| Incomplete requirements | Medium | Regular stakeholder feedback |

---

## 10. Success Criteria

1. All E-commerce and Consultancy code removed
2. Lead Farmer hierarchy fully functional
3. Loan lifecycle (request → distribution → recovery) complete
4. Store card system operational
5. All financial documents generating correctly
6. Role-based access working as specified
7. Mobile-responsive interface
8. Performance: Page load < 3 seconds
9. Zero critical security vulnerabilities

---

## Appendix A: Form Field Mappings

### A.1 Farmers Performance Progress Form → crop_progress_reports

| Manual Field | Database Column |
|--------------|-----------------|
| Farmer's Name | farmer_id (FK) |
| Farm Location | farm_location |
| Contact Number | farmer_id.phone |
| Number of Hectare | hectares |
| Crop Type | crop_type |
| Date Planted | date_planted |
| Fertilizer Application Date | fertilizer_application_date |
| Chemical Application Date | chemical_application_date |
| Week 1-4 Progress | week_1_4 (JSON) |
| Week 5-8 Progress | week_5_8 (JSON) |
| Week 9-12 Progress | week_9_12 (JSON) |
| Week 13-16 Progress | week_13_16 (JSON) |
| Crop Defects | defects (JSON) |
| Inspector Comments | inspector_comments |
| JIMSAN Official Comments | jimsan_official_comments |

### A.2 Lead Farmer Loan Inputs Evaluation → loan_input_requests

| Manual Field | Database Column |
|--------------|-----------------|
| Lead Farmer's Name | lead_farmer_id (FK) |
| Contact Address | lead_farmer_id.address |
| Contact Number | lead_farmer_id.phone |
| Number of Farmers | total_farmers |
| Number of Hectares | total_hectares |
| Seeds (Maize, Rice, etc.) | seed_requests (JSON) |
| Fertilizer (NPK, Urea, etc.) | fertilizer_requests (JSON) |
| Agro Chemicals | chemical_requests |
| Values (Office Use) | total_seed_value, total_fertilizer_value, etc. |

---

## Appendix B: API Endpoints

### Lead Farmers
- `GET /api/lead-farmers.php?action=list`
- `GET /api/lead-farmers.php?action=get&id={id}`
- `POST /api/lead-farmers.php?action=create`
- `POST /api/lead-farmers.php?action=update`
- `GET /api/lead-farmers.php?action=farmers&id={id}` - Get farmers in cluster

### Loan Requests
- `GET /api/loan-requests.php?action=list`
- `GET /api/loan-requests.php?action=get&id={id}`
- `POST /api/loan-requests.php?action=create`
- `POST /api/loan-requests.php?action=submit&id={id}`
- `POST /api/loan-requests.php?action=approve&id={id}`
- `POST /api/loan-requests.php?action=reject&id={id}`

### Store Cards
- `GET /api/store-cards.php?action=list`
- `GET /api/store-cards.php?action=transactions&id={id}`
- `POST /api/store-cards.php?action=adjust`
- `GET /api/store-cards.php?action=balance&item_type={type}&item_id={id}`

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2024-12-14 | System | Initial implementation plan |

---

*This implementation plan should be reviewed and approved by stakeholders before development begins.*
