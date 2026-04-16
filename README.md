ACME GROUP
Web EDI Portal


GitHub Repository Guide
Deployment, Customization & Development Workflow
April 2025
 
Project Overview
This repository contains the ACME GROUP Web EDI Portal — a single-file HTML application that simulates a Web EDI platform for supplier-customer document exchange. It is designed as a demo/prototype tool for sales presentations and product demonstrations.

Technology	React 18 + Babel Standalone (no build step required)
Storage	Browser localStorage (cross-tab sync, no server needed)
File format	Single self-contained HTML file (~150KB)
Hosting	GitHub Pages (static hosting, free)
Repository Structure
edi-portal.html	The deployable standalone HTML file — this is what you host on GitHub Pages
edi-portal-v5.jsx	The editable React source file — make all changes here, then regenerate the HTML
CHANGES.md	Changelog — automatically updated by Claude when modifications are made. Do not edit manually.
README.md	This document
USER_MANUAL.md / .docx	End-user documentation
Initial Setup — GitHub Pages
1.	Create a free account at github.com if you don't have one
2.	Click + New repository → set a name (e.g. edi-portal) → Public → Create repository
3.	On the repository page click uploading an existing file
4.	Drag and drop all files from this folder → Commit changes
5.	Go to Settings → Pages → Source: Deploy from a branch → Branch: main → Folder: / (root) → Save
6.	Wait 1–2 minutes → your URL will be: https://[yourusername].github.io/[reponame]/edi-portal.html

💡 GitHub Pages automatically rebuilds when you push new files. To update the portal, simply upload a new edi-portal.html and the live URL updates within minutes.
Updating the Portal
Standard Workflow
7.	Open a new Claude conversation (or use the Claude Project if configured)
8.	Upload the current edi-portal-v5.jsx file
9.	Describe the changes you want in plain language
10.	Claude modifies the JSX, updates CHANGES.md, and generates a new edi-portal.html
11.	Download both files and upload them to the GitHub repository
12.	The live URL updates automatically

⚠️ Always work from the latest version of edi-portal-v5.jsx. Do not modify the HTML file directly — changes will be overwritten when the HTML is regenerated from the JSX.

File Naming Convention
When Claude produces a new version, the JSX file is versioned sequentially: edi-portal-v5.jsx → edi-portal-v6.jsx. Always keep the previous version as a backup before uploading a new one.
CHANGES.md — Changelog
CHANGES.md is managed exclusively by Claude. Every time a modification is made, Claude appends an entry to this file with:
•	Version number
•	Date
•	List of changes made
•	Files modified

⚠️ Do not edit CHANGES.md manually. It is used as a reference when Claude analyzes the current state of the codebase.
Customization
Brand Colors
Edit the BRAND constant at the top of edi-portal-v5.jsx:
const BRAND = { name: "CLIENT NAME", color: "#0f4c81", accent: "#1a73c8", light: "#e8f0fa", dark: "#0a3560" };

Demo Data
Initial suppliers, DELFORs, ASNs, and inventory records are defined in the INIT constant in edi-portal-v5.jsx. Edit these to pre-populate the demo with client-specific data before a presentation.
Two-Tab Demo Setup
For live demos showing real-time sync between customer and supplier:
13.	Open the portal URL in Tab 1 → login as Customer
14.	Copy the URL → open in Tab 2 → login as Supplier
15.	Actions in one tab are reflected in the other within ~2 seconds

💡 Both tabs must be in the same browser and same browser profile. Incognito mode and different browsers do not share localStorage.
Technical Architecture
Data Flow
Customer uploads DELFOR/Inventory → stored in localStorage → Supplier tab polls every 2s → MERGE_FROM_LS action updates supplier view → Flow Tracking updates in both tabs.

Key Constants
LS_KEY	edi_portal_shared_store — the localStorage key used for cross-tab sync
INIT	Initial demo data object (suppliers, delfors, inventory, asns, documents, reports)
BRAND	Brand configuration (name, colors)

Dependencies (CDN)
React 18	cdnjs.cloudflare.com/ajax/libs/react/18.2.0/
ReactDOM 18	cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/
Babel Standalone 7.23	cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.5/
SheetJS 0.18.5	cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/ (Excel export)
IBM Plex Sans/Mono	fonts.googleapis.com (UI typography)

