# System Architecture Document

**Product:** Enhanced Gmail Purchases Tab  
**Document Purpose:** Provide a clear technical overview of how this improved feature can be structured, built, and supported within Gmail’s ecosystem.

---

## 1. Overview

The Enhanced Purchases Tab is an improved version of the existing “Purchases” page within Gmail. Rather than building a separate app or browser extension, this enhancement focuses on restructuring how purchase-related data already extracted from email receipts is displayed, analyzed, and interacted with by users.

This document outlines the proposed architecture, technology considerations, component structure, and communication flow for implementing this feature improvement.

---

## 2. Proposed Architecture Summary

The solution uses Gmail’s existing data extraction engine but improves the presentation layer, logic layer, and user interaction model.

| Layer      | Role                                                                 |
|------------|----------------------------------------------------------------------|
| Frontend   | Renders the UI for dashboard, purchase list, filters, and detail views |
| Backend    | Processes receipt metadata, categorization logic, analytics, and quick-action updates |
| Data Layer | Uses Gmail’s existing storage; adds lightweight metadata for analytics and filtering |

---

## 3. Frontend Architecture

The frontend builds on Gmail’s existing UI framework and component system.

**Recommended Tech Stack (if built as an internal Google feature):**  
- Framework: Angular (Google’s primary frontend framework)  
- UI Library: Material Design Components  
- Charts & Visuals: Google Charts or Material Chart Components  

**Frontend Responsibilities:**  
- Display dashboard analytics (spending trends, categories, merchants)  
- Render purchase list with filters and sorting  
- Manage a slide-in panel for detailed purchase view  
- Handle user interactions like marking delivered, requesting refund, or flagging a purchase  

**Key UI Components:**  
- Dashboard Summary Component  
- Purchases List Component  
- Filters & Sort Controls  
- Purchase Detail Panel  

---

## 4. Backend Architecture

The backend enhances the logic that already parses purchase-related emails within Gmail.

**Recommended Backend Tech Approach:**  
- Core Service: Google server-side service (Java-based microservice)  

**Logic Modules:**  
- Purchase metadata processor  
- Categorization engine (merchant + category assignment)  
- Analytics service (spending summaries, trends, merchant frequency)  

**Backend Responsibilities:**  
- Receive and process extracted receipt metadata  
- Assign category tags and merchant labels  
- Compute aggregate analytics data for dashboard  
- Serve processed data to frontend via internal API  

---

## 5. Data & Storage

This feature continues using Gmail’s existing receipt extraction and storage model.

**Data Sources:**  
- Email receipts already parsed by Gmail  
- Attached metadata (amount, merchant, date, item list)  

**Additional Data Storage Needs (Lightweight):**  
- User-level metadata for filters and analytics  
- Category tags, delivery status, refund tracking flags  

**Database Consideration:**  
- Primary Database: Google’s internal scalable data store (BigTable / Spanner)  
- No external database is needed  

This ensures compliance with Gmail’s secure, privacy-preserving architecture.

---

## 6. Component Communication Flow

Below is a simplified flow of how components interact:

1. **Email Receipt Arrives in Gmail**  
2. **Existing Parser Extracts Receipt Data**  
   - Merchant, date, amount, items, delivery/refund info (if applicable)  
3. **Enhanced Backend Service Processes Data**  
   - Categorizes purchase  
   - Generates analytics metadata  
4. **Frontend Requests Data from Backend API**  
   - Summary dashboard metrics  
   - Purchase lists and categories  
5. **User Interacts with UI**  
   - Filter, sort, open detail, mark delivered, flag issue  

---

## 7. Why This Approach is Technically Feasible

This enhancement is feasible because:  

- It leverages an existing Gmail feature instead of creating a new standalone system.  
- Gmail already extracts purchase information from receipts; this proposal improves usability, not data collection.  
- Google has existing infrastructure (UI, backend services, storage) that aligns with the required architecture.  
- Enhancements are mostly presentation and logic improvements, not structural changes.  
- Metadata storage and analytics operate on lightweight, derived data — no duplication of core email data.  

In other words, the architecture respects Google’s security, data policies, and engineering standards while delivering meaningful user-facing improvements.

---

## 8. Out of Scope (for clarity)

- New data scraping sources  
- Budgeting, payments, or expense tracking tools  
- Integrations with banks, credit cards, or merchants  
- Exporting personal purchase data to external apps
