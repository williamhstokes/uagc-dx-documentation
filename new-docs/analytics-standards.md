# Analytics Standards & Personalization Framework

This document outlines the analytics implementation standards for UAGC's **Intelligent Personalization Framework**, designed to transform every visitor into a personalized, seamless experience from first click to enrollment.

:::tip Strategic Intelligence Suite
Our analytics framework supports the comprehensive **[UAGC Future Student Experience](https://omac049.github.io/UAGC-Strategic-Intelligence/cookie/UAGC-cookie-personalization.html)** strategy:
- **90%+ Campaign Attribution** preservation across complete user journey
- **20-25% RFI Increase** through personalized content delivery  
- **87%+ Lead Scoring Accuracy** correlation with enrollment outcomes
- **10%+ ROI Improvement** through enhanced tracking and optimization
:::

## Quick Navigation

- [Journey Architecture & Personalization](#journey-architecture--personalization) ⭐
- [UTM Framework & Attribution Strategy](#utm-framework--attribution-strategy)
- [RFI & Application Submission Tracking](#rfi--application-submission-tracking-) ⭐
- [Technical Implementation](#technical-implementation-) ⭐
- [Privacy & Compliance](#privacy--compliance)
- [Success Metrics](#success-metrics-) ⭐

## Journey Architecture & Personalization

### 4-Stage Personalization Framework

Our intelligent personalization engine follows a **journey-based progression** where each visitor advances through distinct stages with tailored experiences:

| Stage | Duration | Key Behaviors | Personalization Strategy |
|-------|----------|---------------|-------------------------|
| **Awareness** | 0-7 days | First discovery, UTM capture | Generic awareness content, program exploration |
| **Interest** | 7-30 days | Content engagement, resource downloads | Progressive engagement, targeted program content |
| **Consideration** | 30-60 days | Form interactions, RFI submission | Lead scoring activation, application-focused messaging |
| **Intent** | 60-90 days | Application start, enrollment actions | Conversion optimization, enrollment support |

### Visitor Identification & Segmentation

#### 90-Day Cookie Persistence Framework

```javascript
// Visitor identification and segmentation
window.dataLayer.push({
  'event': 'visitor_identification',
  'visitor_type': 'returning_visitor',
  'visitor_segment': 'military_affiliated',
  'journey_stage': 'consideration',
  'days_since_first_visit': 14,
  'session_count': 5,
  'personalization_active': true,
  'cookie_consent_status': 'all_accepted'
});
```

#### Visitor Segments & Triggers

| Segment | Identification Criteria | Personalization Triggers |
|---------|------------------------|---------------------------|
| **New Visitor** | First session, no cookie | Show program exploration content |
| **Returning Visitor** | Existing cookie, multiple sessions | Progressive engagement messaging |
| **Military Affiliated** | UTM military parameters, military pages | Military benefits and support focus |
| **Program Specific** | Visited specific program pages 3+ times | Targeted program content and testimonials |
| **High Intent** | RFI submitted, application page visits | Application completion assistance |
| **Re-engagement** | 30+ days inactive, previous engagement | Win-back campaigns and new program highlights |

### Journey Progression Tracking

#### Stage Advancement Events

```javascript
// Track journey stage progression
window.dataLayer.push({
  'event': 'journey_stage_advance',
  'previous_stage': 'interest',
  'current_stage': 'consideration',
  'advancement_trigger': 'rfi_form_start',
  'journey_days': 12,
  'touchpoint_count': 8,
  'visitor_segment': 'military_affiliated',
  'lead_score': 45,
  'predicted_enrollment_probability': 0.68
});
```

#### Personalization Delivery Tracking

```javascript
// Track personalized content delivery
window.dataLayer.push({
  'event': 'personalization_delivered',
  'personalization_type': 'hero_content_variant',
  'variant_id': 'military_benefits_v2',
  'targeting_criteria': ['military_affiliated', 'consideration_stage'],
  'ab_test_name': 'military_hero_test_q4',
  'ab_test_variant': 'variant_b',
  'content_relevance_score': 0.85
});
```

## UTM Framework & Attribution Strategy

### Comprehensive 25-Parameter Tracking Framework

Our attribution strategy preserves **90%+ campaign data** across the complete user journey through standardized UTM governance and advanced tracking parameters.

#### Standard UTM Parameters

| Parameter | Format & Example |
|-----------|------------------|
| `utm_source` | lowercase, no spaces<br/>`google`, `facebook`, `email` |
| `utm_medium` | channel type<br/>`cpc`, `social`, `email`, `display` |
| `utm_campaign` | `[timing]_[initiative]`<br/>`fall2025_click-to-lead` |
| `utm_content` | `[type]_[identifier]`<br/>`video_testimonial`, `text_military` |
| `utm_term` | keywords with + signs<br/>`online+mba+military` |

#### Advanced Tracking Parameters

| Parameter | Purpose | Example |
|-----------|---------|---------|
| `sourceid` | Internal campaign tracking | `18SGB`, `src123456` |
| `affiliateid` | Partner identification | `partner_eduportal` |
| `clickid` | Unique click tracking | `clk_abc123xyz` |
| `utm_vendor` | Lead generation vendor | `leadgenpartner` |
| `adgroup` | Ad group targeting | `mba_military_programs` |
| `ad` | Specific ad creative | `headline_test_a` |
| `match` | Keyword match type | `exact`, `phrase`, `broad` |

#### Campaign Structure Examples

**Click-to-Lead Campaign (RFI Focus):**
```
https://www.uagc.edu/programs/mba?utm_source=google&utm_medium=cpc&utm_campaign=fall2025_click-to-lead&utm_content=text_military&utm_term=online+mba+military&adgroup=mba_military_programs&ad=benefits_headline_v2&sourceid=18SGB
```

**Lead-to-App Campaign (Conversion Focus):**
```
https://www.uagc.edu/apply-now?utm_source=email&utm_medium=email&utm_campaign=spring2025_lead-to-app&utm_content=cta_apply&utm_vendor=salesforce&clickid=clk_app_push_123
```

### Attribution Preservation Events

```javascript
// Multi-touch attribution tracking
window.dataLayer.push({
  'event': 'attribution_touchpoint',
  'touchpoint_type': 'paid_search',
  'campaign_source': 'google',
  'campaign_medium': 'cpc',
  'campaign_name': 'fall2025_click-to-lead',
  'touchpoint_sequence': 3,
  'attribution_value': 0.35,
  'time_since_first_touch_minutes': 2880,
  'utm_preservation_status': 'maintained'
});
```

## RFI & Application Submission Tracking ⭐

### RFI Form Progression Analytics

#### Form Interaction Events

```javascript
// RFI form start tracking
window.dataLayer.push({
  'event': 'rfi_form_start',
  'form_id': 'rfi_homepage_v3',
  'form_location': 'homepage_hero',
  'visitor_segment': 'military_affiliated',
  'journey_stage': 'interest',
  'prefill_data_available': true,
  'lead_score_at_start': 28,
  'session_count': 3
});

// RFI form completion tracking
window.dataLayer.push({
  'event': 'rfi_form_submit',
  'form_id': 'rfi_homepage_v3',
  'form_completion_time_seconds': 145,
  'fields_completed': 8,
  'fields_total': 10,
  'prefill_usage': 'partial',
  'lead_score_update': 65,
  'predicted_enrollment_probability': 0.72,
  'attribution_source': 'google_cpc_fall2025'
});
```

#### Form Optimization Tracking

```javascript
// Form abandonment tracking
window.dataLayer.push({
  'event': 'rfi_form_abandon',
  'form_id': 'rfi_homepage_v3',
  'last_completed_field': 'email_address',
  'completion_percentage': 0.60,
  'time_on_form_seconds': 89,
  'abandon_reason': 'field_validation_error',
  'recovery_campaign_triggered': true
});

// Form error tracking
window.dataLayer.push({
  'event': 'rfi_form_error',
  'form_id': 'rfi_homepage_v3',
  'error_field': 'phone_number',
  'error_type': 'validation_failed',
  'error_message': 'Please enter a valid phone number',
  'user_correction_attempted': true
});
```

### Application Progression Tracking

#### Application Funnel Events

```javascript
// Application start tracking
window.dataLayer.push({
  'event': 'application_start',
  'application_type': 'undergraduate',
  'program_interest': 'business_administration',
  'referral_source': 'rfi_nurture_email',
  'lead_score': 78,
  'days_since_rfi': 14,
  'previous_application_attempts': 0
});

// Application milestone tracking
window.dataLayer.push({
  'event': 'application_milestone',
  'milestone_name': 'personal_information_complete',
  'application_progress_percentage': 0.25,
  'time_since_start_minutes': 12,
  'save_and_continue_used': true,
  'assistance_requested': false
});
```

### Lead Scoring Integration

```javascript
// Real-time lead scoring updates
window.dataLayer.push({
  'event': 'lead_score_calculation',
  'previous_score': 45,
  'current_score': 68,
  'score_change_reason': 'application_section_complete',
  'score_factors': [
    'program_page_views_3+',
    'rfi_submitted',
    'application_started',
    'military_affiliation'
  ],
  'enrollment_probability': 0.74,
  'recommended_next_action': 'admissions_counselor_outreach'
});
```

## Technical Implementation ⭐

### DataLayer Architecture

#### Core DataLayer Structure

```javascript
// Enhanced dataLayer for personalization
window.dataLayer = window.dataLayer || [];

// Page view with personalization context
window.dataLayer.push({
  'event': 'page_view_enhanced',
  'page_location': window.location.href,
  'page_title': document.title,
  'visitor_id': 'vis_abc123xyz',
  'session_id': 'ses_def456uvw',
  'journey_stage': 'consideration',
  'visitor_segment': 'military_affiliated',
  'personalization_active': true,
  'utm_preserved': true,
  'cookie_consent': 'all_accepted',
  'lead_score': 58
});
```

#### Cross-Domain Tracking Implementation

```javascript
// Cross-domain visitor persistence
window.dataLayer.push({
  'event': 'cross_domain_navigation',
  'source_domain': 'uagc.edu',
  'destination_domain': 'apply.uagc.edu',
  'visitor_id': 'vis_abc123xyz',
  'journey_stage': 'consideration',
  'utm_parameters_preserved': true,
  'session_continuity': true,
  'personalization_context_maintained': true
});
```

### Google Tag Manager Configuration

#### Required GTM Events for Personalization

| Event Category | Required Events | Trigger Conditions |
|---------------|-----------------|-------------------|
| **Journey Progression** | `journey_stage_advance`, `visitor_segment_update` | Stage transition logic |
| **Personalization** | `personalization_delivered`, `ab_test_served` | Content variant display |
| **Lead Generation** | `rfi_form_start`, `rfi_form_submit`, `lead_score_update` | Form interactions |
| **Attribution** | `utm_capture`, `attribution_touchpoint` | UTM parameter persistence |
| **Compliance** | `cookie_consent_update`, `privacy_action` | Consent management |

#### Custom Dimensions Configuration

```javascript
// GA4 Custom Dimensions for Personalization
const customDimensions = {
  'visitor_segment': 'custom_dimension_1',
  'journey_stage': 'custom_dimension_2', 
  'personalization_variant': 'custom_dimension_3',
  'lead_score_range': 'custom_dimension_4',
  'utm_campaign_preserved': 'custom_dimension_5',
  'military_affiliation': 'custom_dimension_6',
  'program_interest': 'custom_dimension_7',
  'ab_test_name': 'custom_dimension_8'
};
```

## Privacy & Compliance

### GDPR, CCPA & FERPA by Design

Our personalization framework ensures **100% compliance** with privacy regulations while maintaining data integrity for educational institutions.

#### OneTrust Cookie Consent Management

```javascript
// Enhanced cookie consent tracking
window.dataLayer.push({
  'event': 'cookie_consent_update',
  'consent_analytics': true,
  'consent_marketing': true,
  'consent_personalization': true,
  'consent_functional': true,
  'consent_timestamp': '2025-03-15T10:30:00Z',
  'consent_version': 'v2.1',
  'consent_method': 'explicit_banner_click',
  'personalization_impact': 'full_experience_enabled'
});
```

#### Privacy-First Data Collection

```javascript
// Compliant visitor tracking
window.dataLayer.push({
  'event': 'privacy_compliant_tracking',
  'data_collection_purpose': 'personalization_and_analytics',
  'data_retention_period': '90_days',
  'visitor_rights_disclosed': true,
  'opt_out_mechanism_available': true,
  'ferpa_compliance_verified': true,
  'data_minimization_applied': true
});
```

#### Student Privacy Protection (FERPA)

```javascript
// FERPA-compliant student data handling
window.dataLayer.push({
  'event': 'ferpa_protected_interaction',
  'interaction_type': 'application_submission',
  'pii_handling': 'encrypted_transmission',
  'directory_information_disclosed': false,
  'student_consent_verified': true,
  'legitimate_educational_interest': true
});
```

### Data Governance Framework

| Data Type | Collection Method | Retention Period | Privacy Controls |
|-----------|------------------|------------------|------------------|
| **Visitor Behavior** | Cookie-based tracking | 90 days | Consent-gated, anonymized |
| **UTM Parameters** | URL capture | 12 months | Campaign attribution only |
| **Form Submissions** | Explicit user input | 7 years (FERPA) | Encrypted, access-controlled |
| **Lead Scoring** | Behavioral analytics | 90 days | Pseudonymized identifiers |
| **Cross-Domain** | First-party cookies | 90 days | Same-origin policy enforced |

## Success Metrics ⭐

### Strategic Personalization KPIs

Our analytics framework targets these measurable outcomes aligned with the **UAGC Future Student Experience** strategy:

| Metric | Target | Measurement Method | Success Criteria |
|--------|--------|-------------------|------------------|
| **Campaign Attribution Preservation** | **90%+** | UTM parameter persistence tracking | ≥90% of conversions maintain source attribution |
| **RFI Submission Increase** | **20-25%** | A/B testing vs. control groups | +22.5% average lift across personalized journeys |
| **Lead Scoring Accuracy** | **87%+** | Enrollment outcome correlation | 87% correlation between predicted and actual enrollment |
| **ROI & Revenue Impact** | **10%+** | Revenue per visitor analysis | 10% increase in qualified lead value |
| **Conversion Rate Improvement** | **5%+** | RFI-to-application funnel optimization | 5% minimum lift in conversion rates |
| **UTM Attribution Accuracy** | **90%+** | Campaign source validation | 90% consistent UTM tagging accuracy |
| **Compliance Adherence** | **100%** | Privacy regulation monitoring | Zero compliance violations |
| **Data Quality Integration** | **95%+** | CRM data accuracy validation | 95% accurate cross-system data integration |

### Real-Time Performance Monitoring

#### Attribution Validation Events

```javascript
// Comprehensive attribution accuracy tracking
window.dataLayer.push({
  'event': 'attribution_validation_complete',
  'original_utm_source': 'google',
  'original_utm_campaign': 'fall2025_click-to-lead',
  'final_conversion_source': 'google',
  'final_conversion_campaign': 'fall2025_click-to-lead',
  'attribution_preservation_success': true,
  'journey_duration_days': 14,
  'touchpoint_count': 5,
  'attribution_confidence_score': 0.94
});
```

#### Personalization Performance Impact

```javascript
// Technical performance monitoring
window.dataLayer.push({
  'event': 'personalization_performance_metrics',
  'page_load_impact_ms': 45,
  'script_execution_time_ms': 12,
  'cookie_processing_time_ms': 3,
  'personalization_api_response_ms': 28,
  'total_performance_impact_ms': 88,
  'performance_grade': 'excellent',
  'core_web_vitals_impact': 'minimal'
});
```

#### Lead Scoring Accuracy Validation

```javascript
// Lead scoring effectiveness tracking
window.dataLayer.push({
  'event': 'lead_scoring_accuracy_check',
  'predicted_enrollment_probability': 0.74,
  'actual_enrollment_outcome': true,
  'prediction_accuracy': 'correct',
  'score_calibration_factor': 1.02,
  'model_confidence_level': 0.87,
  'scoring_algorithm_version': 'v2.3'
});
```

### Quarterly Success Reviews

#### Q4 2025 Launch Metrics
- **Foundation Establishment**: UTM standardization and basic journey tracking
- **Baseline Measurement**: Current conversion rates and attribution accuracy
- **Initial A/B Tests**: First personalization campaigns with control groups

#### 2026 Scaling Metrics  
- **Full Personalization**: All visitor segments receiving tailored experiences
- **Advanced Attribution**: Complete cross-domain and multi-touch tracking
- **ROI Optimization**: Continuous improvement and campaign refinement

## Implementation Timeline

### Phase 1: Foundation & Strategy (Q3 2025)
**BUILD** Foundation Infrastructure
- Finalize 25-parameter UTM tracking framework implementation
- Deploy OneTrust cookie consent management with GDPR/CCPA/FERPA compliance
- Implement 90-day cookie persistence and visitor identification system
- Set up enhanced dataLayer structure for personalization triggers
- Configure GA4 custom dimensions for journey tracking

### Phase 2: Launch & Activation (Q4 2025)  
**LAUNCH** Personalization Campaigns
- Deploy first 4-stage journey personalization experiences
- Activate RFI form optimization and lead scoring algorithms
- Implement real-time attribution preservation tracking
- Launch A/B testing framework for personalization variants
- Begin baseline performance measurement and monitoring

### Phase 3: Scale & Optimize (2026)
**SCALE** Full Experience Personalization
- Expand personalization to all visitor segments and journey stages
- Deploy advanced cross-domain tracking and session persistence
- Implement predictive enrollment probability scoring
- Launch continuous optimization and machine learning enhancements
- Achieve full 90%+ attribution preservation and 20-25% RFI increase targets

### Key Milestones & Dependencies

| Quarter | Critical Dependencies | Success Criteria |
|---------|----------------------|------------------|
| **Q3 2025** | OneTrust licensing, GTM configuration | Cookie consent >80%, UTM standardization 100% |
| **Q4 2025** | Personalization platform, team training | First campaigns live, baseline metrics established |
| **Q1 2026** | CRM integration, advanced analytics | Journey tracking 95%+, lead scoring accuracy 87%+ |
| **Q2 2026** | Optimization tools, performance monitoring | ROI targets achieved, full scalability confirmed |

## Governance & Accountability

### Analytics Excellence Framework

#### **Strategic Leadership**
- **Omar Corral** - Analytics Standards Authority & Implementation Oversight  
- **Personalization Committee** - Journey strategy approval and optimization priorities
- **Privacy Council** - GDPR/CCPA/FERPA compliance validation and data governance

#### **Operational Governance**

| Governance Area | Authority | Review Frequency | Approval Requirements |
|----------------|-----------|------------------|----------------------|
| **UTM Standards** | Omar Corral | Monthly | Any new parameter additions |
| **Journey Tracking** | Personalization Committee | Bi-weekly | New segmentation or stage logic |
| **Privacy Compliance** | Privacy Council | Quarterly | All new data collection points |
| **Performance Optimization** | Analytics Team | Weekly | Campaign performance and A/B test results |

#### **Documentation & Change Management**
- **Living Documentation**: All tracking implementations must be documented in real-time
- **Change Control**: No tracking modifications without documented business justification
- **Training Requirements**: Quarterly training on new personalization features and compliance updates
- **Audit Trail**: Complete change history and decision rationale for all analytics implementations

#### **Success Review Cycle**
- **Weekly**: Campaign performance and optimization opportunities
- **Monthly**: Attribution accuracy and data quality validation  
- **Quarterly**: Strategic KPI review and personalization effectiveness assessment
- **Annually**: Comprehensive ROI analysis and future roadmap planning

### Quality Assurance Standards

#### **Pre-Launch Verification**
✅ All personalization events fire correctly across journey stages  
✅ UTM parameters persist through complete conversion funnel  
✅ Lead scoring algorithms correlate with enrollment outcomes  
✅ Cross-domain tracking maintains visitor identity  
✅ Privacy controls function properly with consent management  
✅ Performance impact remains within acceptable thresholds  

#### **Ongoing Monitoring**
📊 Real-time dashboard alerts for tracking anomalies  
🎯 Automated validation of attribution preservation rates  
🔒 Continuous compliance monitoring and privacy audit trails  
⚡ Performance impact assessment and optimization recommendations 