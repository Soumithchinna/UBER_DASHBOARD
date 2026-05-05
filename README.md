<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Uber_logo_2018.png" alt="Uber Logo" width="120"/>

# 🚗 Uber Ride Analytics Dashboard
### Power BI Report | End-to-End Ride Performance Intelligence





[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Status](https://img.shields.io/badge/Status-Active-00D26A?style=for-the-badge)](.)
[![Pages](https://img.shields.io/badge/Report%20Pages-7-1A56DB?style=for-the-badge)](.)
[![Theme](https://img.shields.io/badge/Theme-Fluent2-FF6B35?style=for-the-badge)](.)

> **A multi-page Power BI dashboard delivering deep insights into Uber's ride operations — from bookings and revenue to driver performance, vehicle utilization, rider behavior, and location-level analytics.**

---

</div>

## 📌 Table of Contents

- [Overview](#-overview)
- [KPI Summary](#-kpi-summary)
- [Report Pages](#-report-pages)
- [Data Model](#-data-model)
- [Measures & Calculations](#-measures--calculations)
- [Visual Design](#-visual-design)
- [Getting Started](#-getting-started)
- [File Structure](#-file-structure)
- [Tech Stack](#-tech-stack)

---

## 🌟 Overview

The **Uber Ride Analytics Dashboard** is a comprehensive Power BI (`.pbix`) report built to monitor and analyze the full lifecycle of Uber ride operations. Spanning **7 report pages**, the dashboard enables business stakeholders to track booking trends, revenue performance, driver ratings, vehicle deployment, and rider retention — all within a sleek, dark-themed UI powered by the **Fluent2 design system**.

This dashboard is ideal for:
- 📊 **Operations Teams** monitoring ride completions and cancellations
- 💰 **Finance Teams** tracking revenue and payment method splits
- 🧑‍💼 **Fleet Managers** analyzing vehicle type performance
- 🗺️ **City Planners** reviewing pickup/drop-off hotspots
- 🤝 **Customer Success** understanding rider segments and ratings

---

## 📊 KPI Summary

The following Key Performance Indicators (KPIs) are tracked across the dashboard:

| # | KPI | Description | Visual Type | Page |
|---|-----|-------------|-------------|------|
| 1 | **Total Bookings** | Count of all ride requests placed | Card | Overview, Revenue |
| 2 | **Completed Bookings** | Rides successfully completed by drivers | Card | Overview |
| 3 | **Booking Value (Revenue)** | Total fare revenue generated across all rides | Card | Overview, Revenue |
| 4 | **Avg Distance per Ride** | Mean trip distance across completed rides | Card | Overview |
| 5 | **Total Distance Covered** | Cumulative kilometers/miles driven across all rides | Card | Overview |
| 6 | **Lost Bookings** | Cancelled or unfulfilled ride requests | Card | Overview |
| 7 | **Cancellation Rate** | % of total bookings that were cancelled | Card | Overview |
| 8 | **Customer Count** | Unique customers who placed bookings | Card | Rider |
| 9 | **First-Time Riders** | Riders placing their first-ever booking | Card | Rider |
| 10 | **Regular Riders** | Riders with repeated bookings in the period | Card | Rider |
| 11 | **Return Riders** | Previously inactive riders who came back | Card | Rider |
| 12 | **Avg Driver Rating** | Mean star rating given to drivers | Card | Vehicle |
| 13 | **Avg Customer Rating** | Mean rating of customers by drivers | Card | Rider |
| 14 | **Bookings (Status-Agnostic)** | Total bookings ignoring status filters | Card | Revenue |
| 15 | **Cont%** | Contribution % of a segment to total bookings/revenue | Card | Revenue |

> 💡 **KPI Cards** use sparklines and time-based axis (Month, Weekday) to show trend direction alongside the headline number.

---

## 📑 Report Pages

### 🏠 1. Home
> **Navigation Hub** — A branded landing page with interactive navigation buttons to each report section. Features the Uber logo, custom background imagery, and icon-based menu navigation.
<img width="932" height="480" alt="Screenshot 2026-05-05 105522" src="https://github.com/user-attachments/assets/418469e9-f42f-4de2-9ec6-444111f39930" />

---

### 📋 2. Overview
> **Executive Summary** — The default landing page. Provides a bird's-eye view of all core operational metrics.

**Visuals include:**
- KPI cards: Total Bookings, Booking Value, Completed Bookings, Avg Distance, Lost Bookings
- Area Chart: Booking trend over time (by Month)
- Donut Charts: Ride status breakdown, Payment method split, Vehicle type distribution
- Clustered Column Chart: Bookings by time slot
- Multi-row Card: Cancellation breakdown by reason
- Slicers: Date range, Time slot, City/Location

---

### 💰 3. Revenue
> **Financial Performance** — Dives into fare revenue, payment preferences, and contribution analysis.

**Visuals include:**
- Booking Value KPI with trend
- Clustered Bar/Column Charts: Revenue by vehicle type, revenue by time slot
- Donut Chart: Payment method distribution (Cash, UPI, Credit Card, etc.)
- Cont% analysis: Revenue contribution by segment
- Bookings vs Revenue comparison over month

---

### 🚗 4. Vehicle
> **Fleet Analysis** — Performance breakdown by vehicle category (Sedan, SUV, Intercity, Comfort, etc.)

**Visuals include:**
- Vehicle-type image cards with per-category KPIs
- Driver Ratings: Avg star rating by vehicle type
- Bookings by Vehicle Type
- Multi-row Card: Vehicle-level performance table
- Slicers: Vehicle type filter

---

### 👤 5. Rider
> **Customer Intelligence** — Deep-dive into rider segments, behavior, and satisfaction.

**Visuals include:**
- Customer Count, First-Time, Regular, Return Rider KPI cards
- Avg Customer Rating card
- Rider segmentation donut or bar chart
- Booking behavior by Weekday
- Multi-row Card: Rider-level breakdown

---

### 📍 6. Location
> **Geospatial Insights** — Pickup and drop-off hotspot analysis across the city.

**Visuals include:**
- Location-based cards (Pickup Location, Drop Location)
- Bar/Column Charts: Top pickup and drop-off zones
- Slicers: Location filter
- Icons for visual location context

---


## 🗄️ Data Model

The report is built on the **UBER** fact table with supporting dimension tables:

```
UBER (Fact Table)
├── Customer ID
├── Vehicle Type
├── Ve_Type (Category)
├── Pickup Location
├── Drop Location
├── Payment Method
├── Time Slot
├── Driver Ratings
├── Customer Rating
├── Driver Cancellation Reason
├── Reason for Cancelling by Customer
└── Incomplete Rides Reason

Calender (Date Dimension)
├── Month
└── Weekday

IMG (Lookup Table)
├── Vehicle Type
└── Img (Image URL for vehicle icons)

Date Axis (Custom Date Table)
└── Date Axis

Cancel Rides (Cancellation Lookup)
└── Cancel Rides

_Measures (Calculated Measure Table)
└── [All DAX measures]
```

---

## 🧮 Measures & Calculations

All DAX measures are housed in a dedicated **`_Measures`** table for clean model organization:

| Measure | DAX Logic | Description |
|---------|-----------|-------------|
| `Completed_Bookings` | `CALCULATE(COUNT(...), Status = "Completed")` | Rides with completed status |
| `Booking_count` | `COUNT(UBER[Customer ID])` | Total ride requests |
| `Booking_Value` | `SUM(UBER[Fare])` | Total revenue |
| `Total_Distance` | `SUM(UBER[Distance])` | Cumulative trip distance |
| `Avg_Distance` | `AVERAGE(UBER[Distance])` | Mean trip distance |
| `Lost_Bookings` | Cancelled + Incomplete rides | Unfulfilled demand |
| `Cont%` | `DIVIDE([Booking_count], [Bookings_Remove_Status_Filter])` | Segment contribution % |
| `Customer_Count` | `DISTINCTCOUNT(UBER[Customer ID])` | Unique customers |
| `First_time` | Riders with 1 booking | New customer metric |
| `Regular_rider` | Riders with 2+ bookings | Loyal customer metric |
| `Return_rider` | Previously churned, now active | Re-engagement metric |
| `Bookings_Remove_Status_Filter` | `ALL()` on status | Context-independent total |

> Sparkline data for `Completed_Bookings` is computed over `Calender.Month` axis for trend cards.

---

## 🎨 Visual Design

| Property | Value |
|----------|-------|
| **Theme** | Fluent2 (Microsoft) + Custom JSON theme |
| **Background Color** | `#F1EFEF` (light warm gray) |
| **Canvas Size** | 2000 × 1080 px (widescreen) |
| **Navigation** | Action buttons with page-navigation interactions |
| **Icons** | Custom PNG icons (rupee, location, car, distance, star rating, user avatar) |
| **Layout** | Multi-section cards + charts + slicers per page |
| **Slicers** | Advanced Slicer visuals with dropdown/list variants |

---

## 🚀 Getting Started

### Prerequisites
- **Power BI Desktop** (November 2024 or later recommended)
- Windows OS (Power BI Desktop is Windows-only)

### Opening the Report

```bash
# Clone or download the repository
git clone https://github.com/your-username/uber-powerbi-dashboard.git

# Open in Power BI Desktop
# File → Open → uber.pbix
```

### Connecting to Your Data

1. Open `uber.pbix` in Power BI Desktop
2. Go to **Home → Transform Data → Data Source Settings**
3. Update the data source path to your Uber dataset (CSV/Excel/SQL)
4. Ensure columns match the expected schema (see [Data Model](#-data-model))
5. Click **Refresh** to load live data

> ⚠️ The `.pbix` file may contain embedded sample data. For production use, connect to your actual data source.

---

## 📁 File Structure

```
uber-powerbi-dashboard/
│
├── uber.pbix                          # Main Power BI report file
│
├── README.md                          # Project documentation (this file)
│
└── ASSETS/                          # Reference assets (optional)
    ├── DASHBOARD PDF/
    |
    └── data-sample/
        └── uber_sample.csv            # Sample data schema reference
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Report authoring, DAX, data modeling |
| **DAX** | KPI calculations, time intelligence, segmentation |
| **Fluent2 Theme** | Microsoft's design system for visual consistency |
| **Custom JSON Theme** | Brand color overrides and typography |
| **Power Query (M)** | Data transformation and cleaning |
| **PNG Icons** | Custom visual branding (rupee, location, cars, avatars) |

---

## 📈 Roadmap

- [ ] Add **Map Visual** for geospatial pickup/drop heatmap
- [ ] Integrate **Surge Pricing** analysis layer
- [ ] Add **Driver Performance** dedicated page
- [ ] Enable **Row-Level Security (RLS)** by city/region
- [ ] Publish to **Power BI Service** with scheduled refresh
- [ ] Add **AI Insights** visuals using Power BI's smart narrative

---







