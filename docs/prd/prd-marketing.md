# PRD - Marketing

## Document Information

| Field | Details |
|---|---|
| **Product / Feature Name** | Marketing – Car Rental System |
| **Author** | Copilot |
| **Date** | |
| **Version** | |

---

## Table of Contents

1. [Overview](#overview)
   - 1.1 [Background](#background)
   - 1.2 [Objective](#objective)
   - 1.3 [Goals](#goals)
2. [Problem Statement](#problem-statement)
3. [Functional Requirements](#functional-requirements)
   - 3.1 [Multi-Channel Campaign Management](#31-multi-channel-campaign-management)
   - 3.2 [Promotional Campaign Management](#32-promotional-campaign-management)
   - 3.3 [Customer Segmentation](#33-customer-segmentation)
   - 3.4 [Campaign Analytics and Metrics](#34-campaign-analytics-and-metrics)
   - 3.5 [Upsell and Cross-Sell Opportunities](#35-upsell-and-cross-sell-opportunities)
   - 3.6 [External Marketing Tool Integration](#36-external-marketing-tool-integration)
   - 3.7 [Pricing and Promotions Management](#37-pricing-and-promotions-management)
   - 3.8 [Referral and Affiliate Programs](#38-referral-and-affiliate-programs)
   - 3.9 [Marketing Reporting and Dashboard](#39-marketing-reporting-and-dashboard)
   - 3.10 [Customer Feedback and Review Management](#310-customer-feedback-and-review-management)

---

## Overview

### Background

The company is an established player in the car sales industry with existing marketing channels, customer relationships, and brand equity. As the business expands into car rental, the marketing team must extend its strategies and systems to support a new line of business. Unlike car sales—where transactions are infrequent but high-value—car rentals involve recurring, shorter-duration transactions with a higher volume of customer interactions. This shift requires dedicated marketing capabilities to attract, retain, and grow the rental customer base.

### Objective

Define the functional requirements for a marketing module within the car rental system that enables the marketing team to run campaigns, manage promotions, segment customers, integrate with external platforms, track performance, and leverage customer feedback to drive rental business growth.

### Goals

- Enable the marketing team to repurpose and extend existing car sales marketing channels to promote car rentals.
- Support the creation and management of promotional campaigns (seasonal, loyalty, partnership-based) tailored to the rental business.
- Provide customer segmentation capabilities to enable targeted marketing for car rentals.
- Deliver campaign effectiveness metrics and marketing dashboards to support data-driven decision making.
- Support upsell and cross-sell opportunities between car rentals and car sales.
- Facilitate integration with external marketing platforms (email, social media, ad platforms).
- Enable flexible pricing and promotion management, including dynamic pricing.
- Support referral and affiliate programs to grow the rental customer base organically.
- Collect and surface customer feedback and reviews to support marketing activities.

---

## Problem Statement

The company's marketing team has extensive experience promoting car sales, but currently lacks any system or process to support marketing for car rentals. As the company enters the car rental market, the team faces the challenge of:

- Launching a new product line with no dedicated marketing infrastructure or data history for rentals.
- Adapting existing marketing channels, customer lists, and brand campaigns to also serve rental customers.
- Being unable to run targeted, personalised promotions for rental customers without segmentation capabilities.
- Having no visibility into campaign effectiveness or rental-specific marketing KPIs.
- Lacking tooling to manage rental-specific promotions, dynamic pricing, referrals, or affiliate partnerships.
- Missing mechanisms to systematically collect, analyse, and act on customer feedback about rental experiences.

**Key users affected:**
- **Marketing Manager / Marketing Team:** Responsible for planning and executing campaigns, managing promotions, and analysing performance.
- **Pricing Analyst:** Responsible for managing rental pricing rules and promotional discounts.
- **Partnership / Affiliate Manager:** Responsible for managing referral and affiliate programs.
- **Customer:** Rents vehicles and is the target of all marketing activities.

**Why this is important now:**  
The company is launching car rental as a new business line immediately. Without a marketing module from the outset, the team cannot effectively acquire customers, differentiate offers, or measure the success of the new line of business. Delayed marketing infrastructure directly risks slow customer acquisition and poor return on investment for the car rental launch.

---

## Functional Requirements

### 3.1 Multi-Channel Campaign Management

#### US-MKT-001: View and select marketing channels for car rental campaigns

**Statement:** **As a** Marketing Manager,  
**I want to** view all available marketing channels (e.g. email, SMS, social media, paid ads, in-app notifications) and select which ones to use for a car rental campaign,  
**So that** I can leverage the company's existing marketing infrastructure for the new rental business.

**Acceptance Criteria:**
- The system displays a list of all available marketing channels.
- The Marketing Manager can associate one or more channels with a campaign.
- The system indicates which channels were previously used for car sales and are available for rental campaigns.

---

#### US-MKT-002: Create and publish a multi-channel car rental campaign

**Statement:** **As a** Marketing Manager,  
**I want to** create a car rental marketing campaign with content, target audience, schedule, and channels defined,  
**So that** I can promote car rental offers across multiple platforms from a single interface.

**Acceptance Criteria:**
- The system allows creating a campaign with a name, description, start/end date, target segment, selected channels, and associated promotions.
- The campaign can be scheduled for future publishing or published immediately.
- The system confirms successful publishing and shows campaign status (draft, active, ended).

---

### 3.2 Promotional Campaign Management

#### US-MKT-003: Create a seasonal promotional campaign for car rentals

**Statement:** **As a** Marketing Manager,  
**I want to** create time-limited seasonal promotions (e.g. summer discount, holiday weekend offer) for car rentals,  
**So that** I can drive demand during peak or targeted periods.

**Acceptance Criteria:**
- The system allows defining a promotion with a name, discount type (percentage or fixed amount), validity period, and applicable vehicle categories.
- The promotion can be linked to a campaign.
- The system prevents overlapping promotions on the same vehicle category unless explicitly allowed.

---

#### US-MKT-004: Create a customer loyalty program for car rentals

**Statement:** **As a** Marketing Manager,  
**I want to** define a loyalty program where customers earn points or rewards for car rental transactions,  
**So that** I can incentivise repeat rentals and increase customer lifetime value.

**Acceptance Criteria:**
- The system allows configuring earning rules (e.g. points per rental day or spend amount) and redemption rules (e.g. free rental day after N points).
- Loyalty program status and points balance are visible to the customer in their profile.
- The system can send automated notifications when a customer reaches a reward threshold.

---

#### US-MKT-005: Create a partnership-based promotion for car rentals

**Statement:** **As a** Marketing Manager,  
**I want to** create promotional offers tied to partner organisations (e.g. hotels, airlines, corporates),  
**So that** I can attract new customer segments through third-party referral channels.

**Acceptance Criteria:**
- The system allows associating a promotion with a specific partner organisation.
- Unique partner promo codes or discount links can be generated per partner.
- Partner-attributed bookings are tracked and reportable.

---

### 3.3 Customer Segmentation

#### US-MKT-006: Define customer segments for targeted rental marketing

**Statement:** **As a** Marketing Manager,  
**I want to** create customer segments based on attributes such as rental history, geography, vehicle preference, age group, and spending tier,  
**So that** I can deliver targeted and relevant marketing messages to the right customers.

**Acceptance Criteria:**
- The system supports defining segments using at least the following attributes: rental frequency, total spend, vehicle type preference, location/region, customer age group, and loyalty tier.
- Segments can be saved, named, and reused across multiple campaigns.
- The system displays the estimated audience size for a segment before a campaign is launched.

---

#### US-MKT-007: View customer segment membership

**Statement:** **As a** Marketing Manager,  
**I want to** see which customers belong to a given segment,  
**So that** I can validate segment definitions and review target audiences before launching a campaign.

**Acceptance Criteria:**
- The system displays a list of customers in a selected segment with key attributes visible.
- Segment membership is dynamically recalculated when filter criteria change.
- The Marketing Manager can export segment lists for external use.

---

### 3.4 Campaign Analytics and Metrics

#### US-MKT-008: Track campaign performance metrics

**Statement:** **As a** Marketing Manager,  
**I want to** view key performance metrics for each car rental campaign (e.g. impressions, click-through rate, bookings attributed, revenue generated),  
**So that** I can evaluate the effectiveness of each campaign and optimise future efforts.

**Acceptance Criteria:**
- The system tracks and displays at least: campaign reach, click-through rate, conversion rate (rental bookings), revenue attributed, and cost per acquisition.
- Metrics are updated in near real-time or on a defined refresh schedule.
- Campaign metrics can be filtered by date range, channel, and segment.

---

#### US-MKT-009: Compare performance across campaigns

**Statement:** **As a** Marketing Manager,  
**I want to** compare performance metrics across multiple campaigns side by side,  
**So that** I can identify which campaigns and channels deliver the best return on investment.

**Acceptance Criteria:**
- The system provides a comparison view for selected campaigns with the same KPIs displayed.
- The comparison can be filtered by channel, promotion type, and customer segment.
- Results can be exported as a report.

---

### 3.5 Upsell and Cross-Sell Opportunities

#### US-MKT-010: Offer car rental upsell to car sales customers

**Statement:** **As a** Marketing Manager,  
**I want to** identify car sales customers who have not yet rented a vehicle and target them with rental introductory offers,  
**So that** I can convert existing sales customers into rental customers.

**Acceptance Criteria:**
- The system can generate a segment of customers who have a car sales history but no rental history.
- A targeted campaign or promotional offer can be sent to this segment.
- Conversion from sales-only to rental customer is tracked and reported.

---

#### US-MKT-011: Offer car sales upsell to active car rental customers

**Statement:** **As a** Marketing Manager,  
**I want to** identify frequent rental customers who may be ready to purchase a vehicle and target them with car sales offers,  
**So that** I can grow overall company revenue by cross-selling car sales to rental customers.

**Acceptance Criteria:**
- The system can generate a segment of high-frequency or high-spend rental customers.
- A targeted car sales promotional message can be associated with this segment.
- Cross-sell conversions are tracked and attributed to the campaign.

---

### 3.6 External Marketing Tool Integration

#### US-MKT-012: Integrate with email marketing platforms

**Statement:** **As a** Marketing Manager,  
**I want to** connect the car rental system with an email marketing platform (e.g. Mailchimp, SendGrid),  
**So that** I can send personalised rental campaign emails using our existing email marketing tooling.

**Acceptance Criteria:**
- The system supports configuration of at least one email marketing platform integration.
- Customer segments can be synchronised or exported to the connected email platform.
- Campaign performance data (e.g. open rates, click-through rates) can be imported back into the system.

---

#### US-MKT-013: Integrate with social media and advertising platforms

**Statement:** **As a** Marketing Manager,  
**I want to** connect the car rental system with social media and ad platforms (e.g. Facebook Ads, Google Ads),  
**So that** I can run targeted digital advertising campaigns using rental customer segments.

**Acceptance Criteria:**
- The system supports exporting audience segments to at least one social media or ad platform.
- Campaign spend and performance data from external platforms can be imported and associated with rental campaigns.
- Integration credentials are securely managed by an administrator.

---

### 3.7 Pricing and Promotions Management

#### US-MKT-014: Create and manage rental pricing rules

**Statement:** **As a** Pricing Analyst,  
**I want to** define base pricing rules for different vehicle categories and rental durations,  
**So that** I can ensure rental rates are competitive and aligned with business targets.

**Acceptance Criteria:**
- The system supports defining base prices per vehicle category, per day, per week, and per month.
- Pricing rules can have defined validity periods.
- Only authorised users (Pricing Analyst or Marketing Manager) can create or modify pricing rules.

---

#### US-MKT-015: Apply promotional discounts to rental pricing

**Statement:** **As a** Pricing Analyst,  
**I want to** apply promotional discounts to existing pricing rules for specific time periods or customer segments,  
**So that** I can implement campaign offers without changing the base pricing.

**Acceptance Criteria:**
- Promotional discounts can be defined as a percentage or fixed amount applied on top of base pricing.
- Discounts can be scoped to specific vehicle categories, rental periods, customer segments, or promo codes.
- The system shows the effective price after discount during the booking process.

---

#### US-MKT-016: Enable dynamic pricing based on demand and availability

**Statement:** **As a** Pricing Analyst,  
**I want to** configure dynamic pricing rules that adjust rental rates based on real-time demand, availability, and seasonal factors,  
**So that** I can maximise revenue during peak periods and fill fleet capacity during slow periods.

**Acceptance Criteria:**
- The system supports configuring dynamic pricing rules with parameters such as minimum/maximum price bounds, demand thresholds, and availability percentage.
- Dynamic pricing adjustments are logged and auditable.
- The current effective price (including dynamic adjustments) is visible to customers during booking.

---

### 3.8 Referral and Affiliate Programs

#### US-MKT-017: Create a referral program for car rental customers

**Statement:** **As a** Marketing Manager,  
**I want to** set up a referral program where existing rental customers can refer new customers in exchange for rewards,  
**So that** I can grow the rental customer base through word-of-mouth at a lower acquisition cost.

**Acceptance Criteria:**
- The system generates a unique referral code or link per customer.
- When a new customer completes a rental booking using a referral code, both the referrer and the new customer receive a defined reward (discount, credit, or loyalty points).
- Referral activity (referrals sent, conversions, rewards issued) is trackable per customer and in aggregate.

---

#### US-MKT-018: Manage affiliate partners for car rentals

**Statement:** **As a** Partnership / Affiliate Manager,  
**I want to** register and manage affiliate partners who promote car rentals in exchange for a commission,  
**So that** I can scale customer acquisition through an affiliate network.

**Acceptance Criteria:**
- The system supports registering affiliate partners with unique tracking codes or links.
- Bookings attributed to an affiliate are recorded and associated with the correct partner.
- Commission calculations are tracked and available for reporting and payout processing.

---

### 3.9 Marketing Reporting and Dashboard

#### US-MKT-019: Access a marketing performance dashboard

**Statement:** **As a** Marketing Manager,  
**I want to** access a consolidated marketing dashboard showing key rental marketing KPIs,  
**So that** I can monitor overall marketing performance and make informed decisions at a glance.

**Acceptance Criteria:**
- The dashboard displays at least: total rental bookings from campaigns, revenue attributed to marketing, active campaigns count, top-performing promotions, customer acquisition cost, and loyalty program participation rate.
- The dashboard supports filtering by date range.
- Data on the dashboard refreshes on a defined schedule or on demand.

---

#### US-MKT-020: Generate and export marketing reports

**Statement:** **As a** Marketing Manager,  
**I want to** generate detailed marketing reports for specific campaigns, time periods, or customer segments and export them,  
**So that** I can share performance results with stakeholders and support budget planning.

**Acceptance Criteria:**
- The system supports generating reports for: campaign performance, promotion redemption, referral/affiliate performance, segment conversion rates, and revenue attribution.
- Reports can be exported in at least CSV and PDF formats.
- Scheduled report delivery (e.g. weekly email) can be configured.

---

### 3.10 Customer Feedback and Review Management

#### US-MKT-021: Collect customer feedback after a car rental

**Statement:** **As a** Marketing Manager,  
**I want to** automatically prompt customers to submit feedback or a review after completing a rental,  
**So that** I can collect authentic customer experiences to support marketing materials and service improvement.

**Acceptance Criteria:**
- The system triggers an automated feedback request (via email or in-app notification) within a configurable time window after rental completion.
- Customers can submit a rating (e.g. 1–5 stars) and an optional written review.
- Feedback submissions are stored and associated with the customer, rental record, and vehicle.

---

#### US-MKT-022: Display and utilise customer reviews in marketing

**Statement:** **As a** Marketing Manager,  
**I want to** view, moderate, and approve customer reviews for use in marketing campaigns and the booking experience,  
**So that** I can build social proof and customer trust for the car rental service.

**Acceptance Criteria:**
- Marketing Managers can view all submitted reviews and their status (pending, approved, rejected).
- Approved reviews can be displayed on the company's rental booking pages or marketing materials.
- The system surfaces aggregated rating scores (average rating, total reviews) per vehicle category for use in campaign content.

---

#### US-MKT-023: Analyse customer sentiment from reviews

**Statement:** **As a** Marketing Manager,  
**I want to** view a summary of customer sentiment trends from rental feedback over time,  
**So that** I can identify patterns that affect the rental brand and adjust marketing messaging accordingly.

**Acceptance Criteria:**
- The system provides an aggregated view of ratings over time (e.g. monthly average rating trend).
- Common themes or keywords from written reviews are surfaced (e.g. via a word cloud or frequency summary).
- Negative feedback can be flagged for follow-up by the customer service or operations team.
