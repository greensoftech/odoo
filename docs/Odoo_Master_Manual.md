# The Ultimate Odoo Master Manual
## A 50-Page Complete Guide for Company Owners & Administrators

---

# Table of Contents
* **Part 1 (Current):** Introduction, Core Architecture, Settings, and CRM.
* **Part 2 (Next):** Sales, Quotations, Pricing Strategies, and Point of Sale (POS).
* **Part 3 (Upcoming):** Purchasing, Inventory Management, Routing, and Warehouses.
* **Part 4 (Upcoming):** Financial Accounting, Invoicing, and Bank Reconciliation.
* **Part 5 (Upcoming):** Human Resources, Website Builder, E-commerce, and Manufacturing.

---

# Chapter 1: Introduction to the Odoo ERP Paradigm

## 1.1 What is Odoo?
Odoo is not just a software application; it is a complete **Enterprise Resource Planning (ERP)** ecosystem. In traditional businesses, the marketing team uses Mailchimp, the sales team uses Salesforce, the warehouse uses Fishbowl, and the accountants use QuickBooks. This creates "Data Silos" where information gets trapped, requiring manual data entry to move information from one system to another.

Odoo breaks down these silos. Every "App" in Odoo (CRM, Sales, Inventory, Accounting) is actually just a different window looking into the exact same database. 

## 1.2 The Concept of "The Chain Reaction"
Because all apps share the same database, Odoo operates on the principle of the "Chain Reaction." You rarely have to create data twice. 
1. A Lead is created in the **CRM**.
2. The Lead is converted into a Customer in the **Sales** app.
3. A Quotation is confirmed, which automatically generates a Delivery Order in the **Inventory** app.
4. When the Delivery is validated, Odoo automatically generates a Draft Invoice in the **Accounting** app.

As the company owner, your goal is to train your employees to never break this chain. If a warehouse worker decides to ship a product without validating the Delivery Order in Odoo, the Accounting department will never be notified to send the invoice, and the company loses money.

---

# Chapter 2: Core Architecture & Settings

## 2.1 Multi-Company Environments
Odoo allows you to run multiple businesses inside a single database. 
* **Shared Data:** By default, if you leave the "Company" field blank on a Product or Customer, that record is shared across all companies in your database.
* **Restricted Data:** If you assign a Product or Customer to "Company A", then "Company B" will never see it.
* **Strict Financials:** Financial data (Sales Orders, Purchase Orders, Invoices, Journal Entries) is **never** shared. A Sales Order must belong to one and only one company.

## 2.2 User Management and Permissions
To add an employee, go to **Settings -> Manage Users -> New**. 
Permissions in Odoo are highly granular. For every app, you can assign an employee one of the following levels:
* **Blank:** The employee cannot see the app.
* **User (Own Documents Only):** The employee can use the app, but cannot see their coworkers' data. Excellent for competitive sales environments.
* **User (All Documents):** The employee can see everything in the app, but cannot change the app's core settings.
* **Administrator:** Full control over the app's configuration.

## 2.3 The Developer Mode
Odoo hides complex technical settings from regular users to prevent them from breaking the system. To access advanced features (like automated actions or user defaults):
1. Go to Settings and scroll to the bottom.
2. Click **Activate the developer mode**.
3. A bug icon 🐛 will appear in the top right, and a new **Technical** menu will appear at the top of the Settings screen.

---

# Chapter 3: CRM & Lead Management

## 3.1 The Sales Pipeline
The CRM (Customer Relationship Management) app is where your marketing and pre-sales processes happen. The core of the CRM is the **Kanban Pipeline**.
The pipeline is divided into columns (e.g., New -> Qualified -> Proposition -> Won). Salespeople drag and drop "Opportunity Cards" from left to right as the deal progresses.

## 3.2 Lead Generation
Opportunities can be created manually, but Odoo is designed to automate this:
* **Email Aliases:** You can configure an email address like `sales@yourcompany.com`. Whenever a customer emails that address, Odoo automatically creates an Opportunity card in the "New" column of your CRM pipeline.
* **Web Forms:** If you use Odoo's Website builder, anyone filling out the "Contact Us" form is automatically turned into an Opportunity.

## 3.3 Activity Management
Instead of using sticky notes or external calendar reminders, salespeople should use **Activities**. 
On any Opportunity card, click **Schedule Activity** (Call, Email, Meeting, To-Do). Odoo will track this. If a salesperson logs in and sees a red clock icon, it means they have an overdue activity they must complete immediately to save the deal.

## 3.4 Lead Scoring & Probability
As an Opportunity moves from left to right across the pipeline, its "Probability of Winning" percentage increases. Odoo uses Artificial Intelligence (if enabled) to analyze your past won/lost deals and automatically assigns a probability score to new leads based on their country, email domain, and industry, telling your sales team which leads to prioritize!

---
# Chapter 4: Sales & Quotation Management

## 4.1 The Sales Flow
When an Opportunity in the CRM is won (or is nearing a win), the next step is to send a formal proposal. This is done in the **Sales App**. 
1. The salesperson creates a **Quotation**. 
2. They add the Customer and the Products.
3. They send it to the customer via email directly from Odoo.
4. The customer reviews the PDF and can electronically sign and pay for it via the online portal.
5. Once signed or paid, the Quotation officially converts into a **Sales Order (SO)**.

## 4.2 Products and Variants
Before you can sell anything, your products must be configured correctly.
* **Product Templates vs. Variants:** If you sell T-Shirts, the "T-Shirt" is the Product Template. The specific combinations (Red-Small, Blue-Large) are the Product Variants. Odoo allows you to manage inventory at the Variant level but keep marketing copy at the Template level.
* **Service Products:** If you sell consulting, ensure the product type is set to "Service". You can configure Odoo to automatically create a "Project" and "Task" for your delivery team the moment a Service product is sold.

## 4.3 Advanced Pricing Strategies (Pricelists)
Never let salespeople manually override prices by typing numbers into a quotation. This leads to massive margin loss. Instead, use **Pricelists**.
Pricelists are programmable rules that dictate how much a customer pays.
* **Volume Discounts:** "If they buy 10+, give them 15% off."
* **Customer Segments:** "If the customer belongs to the 'VIP Retailers' group, give them wholesale pricing."
* **Time-based Sales:** "Give 20% off all Furniture products from Black Friday to Cyber Monday."
Odoo applies these mathematical rules instantly when the salesperson selects the customer.

---

# Chapter 5: Point of Sale (Retail & Restaurants)

## 5.1 What is the Odoo POS?
The Point of Sale (POS) app is designed for physical retail stores or restaurants. It is an offline-capable web application. This means if your store loses internet connection, the cashier can continue scanning items, taking cash, and printing receipts. When the internet returns, the POS syncs all the offline orders to the main Odoo database automatically.

## 5.2 POS Architecture
You can have multiple "Shops" (POS Configurations) in a single database.
* **Retail Shops:** Optimized for barcode scanners, receipt printers, and fast checkouts.
* **Restaurant/Bar:** A completely different interface that shows a visual map of your tables. Waiters can take orders on tablets, send tickets directly to the kitchen printer, and split the bill between customers.

## 5.3 Daily Sessions & Cash Control
A POS operates in "Sessions". 
1. **Opening:** When the cashier arrives in the morning, they open a session and count the physical cash in the drawer (the "Opening Float").
2. **Selling:** They process transactions all day.
3. **Closing:** At night, they count the drawer again. If Odoo says there should be $500, but there is only $490, the cashier must record a $10 loss. The session is closed, and Odoo posts a single, consolidated Journal Entry to your Accounting app for the entire day's sales, keeping your books incredibly clean.

---
# Chapter 6: Purchasing and Replenishment

## 6.1 The Procure-to-Pay Flow
Just as Sales brings money into the company, Purchasing dictates how money leaves. The flow in Odoo ensures you never overpay for inventory:
1. **Request for Quotation (RFQ):** Your purchasing team creates an RFQ to ask suppliers for their best prices.
2. **Purchase Order (PO):** When the price is agreed upon, the RFQ is confirmed, becoming a legally binding PO.
3. **Receiving Products:** Confirming the PO automatically alerts the Warehouse that a delivery is expected.
4. **Vendor Bill Matching:** When the supplier mails you the invoice, Odoo's 3-way matching ensures that the Vendor Bill matches the original Purchase Order AND the exact quantity the warehouse actually received.

## 6.2 Automated Replenishment (Reordering Rules)
Odoo can completely automate your purchasing department using **Reordering Rules**. 
For any product, you can set a Minimum and Maximum stock rule (e.g., Min: 10, Max: 50). 
If a salesperson sells 5 items and your stock drops to 9, Odoo's scheduler runs overnight and automatically generates an RFQ for 41 items to get you back to the Max level. Your purchasing manager simply logs in, sees the automatically generated RFQ, and clicks "Send to Supplier".

---

# Chapter 7: Inventory & Warehouse Management

## 7.1 Multi-Warehouse Architecture
Odoo can handle complex logistics networks seamlessly.
* **Warehouses:** Represent physical buildings (e.g., "Chicago Warehouse", "Miami Warehouse"). 
* **Locations:** Represent specific areas inside those buildings (e.g., "Shelf 4", "Quality Control", "Loading Dock").
Odoo uses "Double-Entry Inventory." This means products never just disappear. If stock decreases in "Shelf 4", it must increase in the "Customer Location" or the "Scrap Location".

## 7.2 Push and Pull Routes
Routes are the mathematical rules that dictate how products move through your company.
* **Make to Stock (Pull):** The default route. You keep items on shelves. When an order comes in, warehouse workers pick it from the shelf.
* **Make to Order (MTO):** You do not keep stock. When a customer buys the item, Odoo automatically triggers a Purchase Order or a Manufacturing Order just for that specific customer.
* **Dropshipping:** When a customer buys an item, Odoo tells your supplier to ship the item *directly* to the customer, completely bypassing your warehouse.

## 7.3 Barcode Scanning
For medium to large operations, manual data entry causes devastating inventory errors. Odoo's Barcode App allows workers to use handheld scanners (like Zebra devices) or smartphone cameras to process orders.
When a delivery truck arrives, the worker simply scans the barcode on the box, and Odoo automatically increments the inventory count. If they scan the wrong item, the scanner flashes red, preventing the error before it happens.

---
# Chapter 8: Financial Accounting & Invoicing

## 8.1 The Double-Entry Engine
Odoo Accounting is not a lightweight bookkeeping tool; it is a strict, double-entry accounting engine designed for large corporations. Every single financial transaction in Odoo must balance. If you sell a product for $100, Odoo automatically creates a Journal Entry that credits your "Product Sales" account for $100 and debits your "Accounts Receivable" account for $100.
Because it is fully integrated, the accounting department rarely has to manually create journal entries. The sales and purchasing teams do it automatically by confirming their orders!

## 8.2 Customer Invoices and Vendor Bills
* **Invoices:** These represent money owed to you by customers. When an invoice is created, it starts in a "Draft" state. Once you click "Post", it officially hits your General Ledger. If a customer is late, you can use the "Follow-up Reports" feature to automatically email them aggressive reminders.
* **Vendor Bills:** These represent money you owe to suppliers. You can manually type them in, or use Odoo's AI Optical Character Recognition (OCR) to scan a PDF of a bill and automatically extract the total, the vendor name, and the due date.

## 8.3 Chart of Accounts & Taxes
* **Chart of Accounts (CoA):** This is the master list of all financial buckets in your company (e.g., Bank Account, Office Supplies Expense, Retained Earnings). Odoo automatically installs the legally compliant CoA for your specific country when you configure your company.
* **Taxes:** Odoo supports complex tax configurations including VAT, Sales Tax, Eco-Taxes, and Withholding taxes. You configure the tax rate once, and Odoo calculates the legal tax implications on every invoice automatically.

---

# Chapter 9: Bank Synchronization & Reconciliation

## 9.1 Bank Feeds
Typing bank statements into an accounting system by hand is obsolete. Odoo connects securely to thousands of banks worldwide (via Plaid, Salt Edge, or direct API). Every morning, Odoo automatically downloads your latest bank statement lines from your checking and credit card accounts.

## 9.2 The Reconciliation Process
Reconciliation is the act of proving your books are accurate. It answers the question: "We received $500 in our bank account today. Why?"
1. Odoo puts your raw bank statement lines on the left side of the screen.
2. It puts your open Invoices and Vendor Bills on the right side of the screen.
3. Odoo's AI looks at the bank line (e.g., "Wire Transfer from Microsoft - $500") and automatically matches it to the open invoice for Microsoft for $500.
4. Your accountant simply reviews the match and clicks **Validate**.
5. Odoo instantly marks the Invoice as "Paid" and updates your Balance Sheet.

## 9.3 Reconciliation Models
If you have recurring bank fees (like a $15 monthly wire fee), you can create a "Reconciliation Model". When Odoo sees "Wire Fee" on the bank statement, it won't look for an invoice. Instead, it will instantly auto-reconcile it directly against your "Bank Fees Expense" account, saving your accountant hours of tedious work every month!

---
# Chapter 10: Human Resources & Payroll

## 10.1 The Employee Lifecycle
Odoo HR replaces disjointed HR systems. When you hire an employee, you create their profile in the **Employees** app. From there, everything is linked:
* **Contracts:** Store their salary, working schedule, and legal contract.
* **Time Off:** Employees request vacations from their phone. Their manager approves it, and it instantly blocks out their Odoo Calendar so salespeople cannot book meetings for them.
* **Appraisals:** Schedule 360-degree performance reviews automatically every year.

## 10.2 Payroll and Timesheets
If you use Odoo for Payroll, the system calculates their paycheck based on their contract. If the employee submits overtime via the **Timesheets** app, the manager approves it, and the extra pay is automatically injected into their next payslip. When you generate the payslip, Odoo automatically creates the Journal Entry to deduct the money from your corporate bank account.

---

# Chapter 11: Website Builder & E-Commerce

## 11.1 The Drag-and-Drop Builder
You do not need WordPress. Odoo has a native Website Builder. You navigate to the frontend of your site, click "Edit", and simply drag blocks (like Images, Text, Carousels) onto the screen. Because it's native, any form submitted on the website goes directly into your backend database.

## 11.2 Native E-Commerce
If you sell products online, simply go to your Product database and click "Publish to Website". The product instantly appears on your online store. 
When a customer buys it, the flow is completely seamless:
1. They pay via Stripe or PayPal on your website.
2. The Sales Order is automatically confirmed.
3. The Invoice is generated and marked as Paid.
4. A Delivery Order is instantly sent to the warehouse tablet for a worker to pack the box. 
Zero manual data entry is required.

---

# Chapter 12: Manufacturing & MRP

## 12.1 Bill of Materials (BOM)
If you assemble products (e.g., building a Custom PC), you define a Bill of Materials.
A "Custom PC" BOM might consist of: 1 Motherboard, 1 CPU, 2 RAM Sticks, and 1 Case.

## 12.2 Manufacturing Orders (MO)
When a salesperson sells a Custom PC, Odoo doesn't tell the warehouse to ship a PC (because it doesn't exist yet). It automatically creates a **Manufacturing Order**. 
1. Odoo checks the warehouse to see if you have the CPU and RAM. 
2. If you don't, it automatically generates a Purchase Order to buy them.
3. Once the parts arrive, the factory floor gets a green light on their tablet. They assemble the PC and click "Mark as Done".
4. Odoo deducts the raw materials from your inventory and adds 1 finished Custom PC to your stock, ready to be shipped.

---
*End of The Ultimate Odoo Master Manual.*
