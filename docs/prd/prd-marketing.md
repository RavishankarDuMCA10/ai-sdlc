# PRD - Car Rental Marketing

## Document Information

| Field | Details |
|---|---|
| **Product / Feature Name** | Car Rental Marketing |
| **Author** | @Copilot |
| **Date** | |
| **Version** | |

---

## Table of Contents

1. [Overview](#overview)
   - [Background](#background)
   - [Objective](#objective)
   - [Goals](#goals)
2. [Problem Statement](#problem-statement)
3. [Functional Requirements](#functional-requirements)
   - [FR-1: Multi-Channel Marketing Promotion](#fr-1-multi-channel-marketing-promotion)
   - [FR-2: Promotional Campaigns Management](#fr-2-promotional-campaigns-management)
   - [FR-3: Customer Segmentation](#fr-3-customer-segmentation)
   - [FR-4: Campaign Performance Metrics & Analytics](#fr-4-campaign-performance-metrics--analytics)
   - [FR-5: Upsell and Cross-Sell Opportunities](#fr-5-upsell-and-cross-sell-opportunities)
   - [FR-6: External Marketing Tool Integration](#fr-6-external-marketing-tool-integration)
   - [FR-7: Pricing & Promotions Management with Dynamic Pricing](#fr-7-pricing--promotions-management-with-dynamic-pricing)
   - [FR-8: Referral and Affiliate Program](#fr-8-referral-and-affiliate-program)
   - [FR-9: Marketing Reporting & Dashboard](#fr-9-marketing-reporting--dashboard)
   - [FR-10: Customer Feedback and Reviews](#fr-10-customer-feedback-and-reviews)

---

## Overview

### Background

The company has an established presence in the car sales business with existing marketing channels, customer relationships, and promotional infrastructure. As it expands into car rental — a new business line — the marketing team needs the system to support targeted promotion, campaign management, and customer engagement capabilities that leverage existing assets while addressing the unique demands of the rental market.

### Objective

To equip the marketing team with system features that enable them to effectively promote car rental services, manage campaigns and pricing, measure effectiveness, and grow a loyal rental customer base — all while capitalising on the synergy with the existing car sales business.

### Goals

- Enable the marketing team to run and manage car rental promotional campaigns from within the system.
- Allow customer segmentation to support targeted, personalised marketing for rentals.
- Provide data-driven insights and dashboards so marketing can measure campaign ROI and optimise strategies.
- Leverage cross-sell and upsell opportunities between car sales and rental customers.
- Integrate with existing and new marketing platforms (email, social media, ad platforms).
- Support flexible and dynamic pricing as a marketing lever.
- Build loyalty and growth through referral, affiliate, and review programs.

---

## Problem Statement

The marketing team has no dedicated system to manage, track, or optimise car rental marketing activities. Without this, the team cannot:

- Reach the right customers with the right rental offers at the right time.
- Reuse and extend the existing car sales marketing channels and customer base effectively for rentals.
- Measure whether their campaigns are actually driving rental bookings or revenue.
- Respond quickly to market demand with dynamic pricing and time-sensitive promotions.

The primary users affected are **marketing managers**, **campaign operators**, and **marketing analysts** within the company. This is important now because the car rental business is launching and without marketing system support from day one, the new business line risks slow adoption, poor customer targeting, and missed revenue opportunities during the critical early growth phase.

---

## Functional Requirements

### FR-1: Multi-Channel Marketing Promotion

**Title:** Extend existing marketing channels to promote car rentals

**Statement:**
**As a** marketing manager, **I want** to configure and activate existing marketing channels (website, email, social media, showroom displays) for car rental promotions, **so that** I can reach potential rental customers using the same channels already used for car sales without rebuilding from scratch.

**Acceptance Criteria:**
- The system allows marketing to associate promotional content with the car rental business line on each active channel.
- Channels currently used for car sales (e.g., email newsletters, social media pages, website banners) can be extended to include car rental campaigns.
- Marketing can select which channels a given rental campaign is published to.

---

### FR-2: Promotional Campaigns Management

**Title:** Create and manage car rental promotional campaigns

**Statement:**
**As a** campaign operator, **I want** to create, schedule, and manage diverse promotional campaigns for car rentals — including seasonal offers, loyalty reward campaigns, and partnership promotions — **so that** I can attract new customers and retain existing ones throughout the year.

**Acceptance Criteria:**
- The system supports creating campaigns with types: seasonal offer, loyalty reward, partnership promotion, and general discount.
- Each campaign has configurable attributes: name, type, start date, end date, discount value or type (percentage, flat, free upgrade), target audience, and applicable vehicle categories.
- Campaigns can be scheduled in advance and activated/deactivated manually or automatically based on dates.
- Loyalty program campaigns can be associated with customer loyalty tiers.
- Partnership promotions can reference the partner name/organisation.

---

### FR-3: Customer Segmentation

**Title:** Segment customers for targeted rental marketing

**Statement:**
**As a** marketing analyst, **I want** to segment customers based on relevant attributes such as rental history, demographics, car sales history, geographic location, and loyalty status, **so that** I can create targeted marketing messages that are relevant to each customer group and improve campaign conversion rates.

**Acceptance Criteria:**
- The system allows defining customer segments using one or more attributes including: age group, location/region, rental frequency, vehicle preference, loyalty tier, car purchase history, and preferred rental duration.
- Campaigns can be assigned to one or more customer segments.
- Customers who belong to a segment automatically receive relevant campaign communications when triggered.
- Segment definitions can be saved, edited, and reused across campaigns.

---

### FR-4: Campaign Performance Metrics & Analytics

**Title:** Track and evaluate rental campaign effectiveness

**Statement:**
**As a** marketing manager, **I want** to access metrics from the car rental system that show how well my campaigns are performing — such as bookings generated, revenue attributed, redemption rates, and customer acquisition — **so that** I can evaluate ROI and make data-informed decisions about future campaigns.

**Acceptance Criteria:**
- The system captures and attributes the following metrics per campaign: number of bookings, revenue generated, coupon/offer redemption count and rate, new customers acquired, and cost per acquisition (where cost data is available).
- Metrics are visible in real time or near real time on a campaign detail view.
- Marketing can compare metrics across campaigns and time periods.
- Data can be exported in CSV or PDF format for reporting purposes.

---

### FR-5: Upsell and Cross-Sell Opportunities

**Title:** Present upsell and cross-sell offers between car sales and rentals

**Statement:**
**As a** marketing manager, **I want** the system to identify and surface upsell and cross-sell opportunities — such as offering a rental to a customer who recently purchased a car (e.g., while their new car is being serviced) or offering a car purchase deal to a loyal rental customer — **so that** the company can increase revenue per customer and create a seamless experience across both business lines.

**Acceptance Criteria:**
- The system can flag car sales customers as potential rental leads based on configurable triggers (e.g., car service booking, recent purchase).
- The system can flag frequent rental customers as potential car sales leads based on configurable rental frequency thresholds.
- Cross-sell and upsell recommendations are surfaced to the marketing team in a dedicated view or report.
- Targeted offers for cross-sell/upsell can be created and associated with appropriate customer segments (FR-3).
- Customers can be opted into cross-sell communications based on their communication preferences.

---

### FR-6: External Marketing Tool Integration

**Title:** Integrate the car rental system with external marketing platforms

**Statement:**
**As a** marketing manager, **I want** the car rental system to integrate with external tools such as email marketing platforms, social media ad platforms, and CRM systems, **so that** I can run coordinated campaigns across all channels without manually exporting and re-entering data.

**Acceptance Criteria:**
- The system supports outbound integration with at least one email marketing platform (e.g., Mailchimp, SendGrid) for sending campaign emails triggered by rental system events.
- The system supports exporting customer segment lists to social media ad platforms (e.g., Meta, Google Ads) for audience targeting.
- Customer data synchronised to external tools respects privacy/consent settings recorded in the rental system.
- Integration configuration (API keys, platform selection) is managed by an administrator within the system settings.
- Integration failures are logged and alerted to administrators.

---

### FR-7: Pricing & Promotions Management with Dynamic Pricing

**Title:** Manage car rental pricing and promotions with dynamic pricing support

**Statement:**
**As a** marketing manager, **I want** to define base rental prices, create promotional pricing rules, and enable dynamic pricing based on demand, seasonality, or fleet availability, **so that** the company can remain competitive, maximise revenue, and attract price-sensitive customers with timely offers.

**Acceptance Criteria:**
- The system provides a pricing management interface where marketing/pricing teams can set base rates per vehicle category and rental duration.
- Promotional pricing (discounts, free days, upgrades) can be layered on top of base pricing and tied to specific campaigns (FR-2).
- Dynamic pricing rules can be configured based on parameters such as: fleet availability threshold, booking lead time, season/date range, and demand index.
- When dynamic pricing is enabled, the system recalculates displayed rental prices automatically according to the active rules.
- Marketing can preview the effective customer-facing price before activating a pricing rule.
- All pricing changes are logged with a timestamp and the user who made the change.

---

### FR-8: Referral and Affiliate Program

**Title:** Support a referral and affiliate program for car rentals

**Statement:**
**As a** marketing manager, **I want** the system to support a referral program where existing customers can refer new customers, and an affiliate program where external partners can drive bookings in exchange for a commission, **so that** the company can grow its rental customer base at a lower acquisition cost through word-of-mouth and partner channels.

**Acceptance Criteria:**
- The system generates unique referral codes for registered rental customers who opt into the referral program.
- When a new customer books using a referral code, both the referrer and the new customer receive a configurable reward (e.g., discount, credit, free rental day).
- The system supports registering affiliate partners with a unique affiliate tracking link or code.
- Bookings attributed to an affiliate are tracked and a commission amount is calculated per configurable rules.
- A referral and affiliate report is available showing: total referrals, conversions, rewards issued, affiliate bookings, and commissions owed.
- Referral and affiliate program settings (reward values, commission rates) are configurable by an administrator.

---

### FR-9: Marketing Reporting & Dashboard

**Title:** Provide a marketing reporting dashboard for car rentals

**Statement:**
**As a** marketing analyst, **I want** access to a dedicated marketing dashboard in the car rental system that consolidates KPIs, campaign performance, customer insights, and channel metrics, **so that** I can monitor the health of our marketing activities and quickly identify areas for improvement without needing to query raw data manually.

**Acceptance Criteria:**
- The marketing dashboard displays the following KPIs: total bookings (with period-over-period comparison), revenue from rentals, active campaign count and total redemptions, new customer count, and customer retention rate.
- The dashboard includes a campaign performance section listing all active campaigns with their key metrics (FR-4).
- Charts and visualisations (bar, line, pie) are provided for: bookings over time, revenue by vehicle category, top-performing campaigns, and customer segment breakdown.
- The dashboard supports filtering by time period (daily, weekly, monthly, custom range) and by campaign, segment, or channel.
- Reports can be scheduled for automated email delivery to selected recipients at a configurable frequency.
- Dashboard data refreshes at least every 24 hours, with the last-updated timestamp shown.

---

### FR-10: Customer Feedback and Reviews

**Title:** Collect and utilise customer feedback and reviews for marketing

**Statement:**
**As a** marketing manager, **I want** the system to automatically collect post-rental reviews and feedback from customers, and allow marketing to highlight positive reviews in promotional materials, **so that** the company can build social proof, improve service quality, and use authentic customer voices in marketing content.

**Acceptance Criteria:**
- The system sends an automated post-rental feedback request to the customer via email or SMS within a configurable number of hours after rental completion.
- Customers can submit a star rating (1–5) and an optional written review via a provided link.
- Submitted reviews are visible to the marketing team in a review management interface, showing rating, review text, customer (anonymised option available), rental date, and vehicle category.
- Marketing can flag selected reviews as "approved for marketing use" with customer consent recorded.
- Approved reviews can be exported or displayed in configurable website banners or campaign materials.
- Aggregate rating data (average score, rating distribution) is available on the marketing dashboard (FR-9).
- The system flags and holds for moderation any reviews containing flagged language before they are published or exported.
