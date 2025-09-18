# A/B Testing with Optimizely

Comprehensive guide for planning, implementing, and analyzing A/B tests to optimize the UAGC digital experience and improve conversion rates.

:::tip Quick Start
New to A/B testing? Start with our [A/B Test Template](content-templates.md#ab-test-documentation-template) and the **Basic Test Setup** section below.
:::

## Overview

A/B testing allows us to make data-driven decisions about website changes by comparing different versions of pages or elements to see which performs better.

### Why A/B Test at UAGC?
- **Optimize Conversion Rates**: Improve RFI submissions, application starts, enrollment completions
- **Reduce Risk**: Test changes before full rollout to avoid negative impact
- **Data-Driven Decisions**: Move beyond opinions to evidence-based improvements
- **Continuous Optimization**: Systematically improve user experience over time

## Testing Strategy Framework

### Test Prioritization Matrix

| Impact | Effort | Priority | Examples |
|--------|--------|----------|----------|
| **High Impact, Low Effort** | 🟢 **Priority 1** | Hero headline copy, CTA button text |
| **High Impact, High Effort** | 🟡 **Priority 2** | Page layout changes, new forms |
| **Low Impact, Low Effort** | 🟡 **Priority 3** | Color changes, micro-copy |
| **Low Impact, High Effort** | 🔴 **Avoid** | Complex features with minimal benefit |

### UAGC Test Categories

#### **Enrollment Funnel Tests**
- **RFI Form Optimization**: Field reduction, layout changes, value propositions
- **Program Page Conversion**: Headlines, testimonials, pricing display
- **Application Process**: Step reduction, progress indicators, help text

#### **User Experience Tests**  
- **Navigation Improvements**: Menu structure, search functionality
- **Content Engagement**: Video placement, content length, formatting
- **Mobile Optimization**: Touch targets, loading speed, layout

#### **Trust & Credibility Tests**
- **Social Proof**: Testimonial placement, student success stories
- **Accreditation Display**: Badge placement, credibility signals
- **Contact Information**: Accessibility, prominence of support options

## Test Planning & Setup

### Pre-Test Planning Checklist

- [ ] **Clear Hypothesis**: "We believe that [change] will [improve metric] because [reasoning]"
- [ ] **Success Metrics Defined**: Primary and secondary KPIs identified
- [ ] **Audience Defined**: Who will see this test and why
- [ ] **Test Duration Calculated**: Based on traffic volume and expected effect size
- [ ] **Technical Requirements**: DataLayer events, tracking setup confirmed
- [ ] **QA Plan**: How variations will be tested before launch

### Optimizely Implementation Process

#### **1. Experiment Setup**

```javascript
// Basic Optimizely experiment structure
// Set up in Optimizely dashboard

// Audience targeting example:
URL contains "uagc.edu/programs"
AND Device type = "Desktop"
AND First-time visitor = "True"
```

#### **2. Variation Creation**

**Control (Variation A)**:
- Current experience
- Baseline for comparison
- No changes from existing design

**Treatment (Variation B)**:  
- Test hypothesis implementation
- Single change when possible (for clear attribution)
- Documented rationale for changes

#### **3. Goal Configuration**

```javascript
// Primary Goal: RFI Form Submission
Event: "rfi_form_submit" 
Tracking: GA4 + Optimizely conversion tracking

// Secondary Goals: Engagement metrics
- Time on page > 30 seconds
- Scroll depth > 50%
- Click on program information links
```

### Technical Implementation

#### **DataLayer Integration**

```javascript
// Track Optimizely experiment exposure
window.dataLayer.push({
  'event': 'optimizely_experiment_viewed',
  'experiment_id': 'homepage_hero_test',
  'variation_id': 'variation_b',
  'experiment_name': 'Hero CTA Button Test'
});

// Track conversions
window.dataLayer.push({
  'event': 'optimizely_conversion',
  'experiment_id': 'homepage_hero_test', 
  'variation_id': 'variation_b',
  'goal_name': 'rfi_form_submit',
  'conversion_value': 1
});
```

#### **QA Testing Protocol**

1. **Preview Mode Testing**:
   - Test all variations in Optimizely preview
   - Verify tracking implementation
   - Check mobile/desktop rendering
   - Validate form functionality

2. **Cross-Browser Testing**:
   - Chrome, Firefox, Safari, Edge
   - Mobile browsers (iOS Safari, Android Chrome)
   - Test on various screen sizes

3. **Analytics Validation**:
   - Verify GA4 events firing correctly
   - Check Optimizely results dashboard
   - Confirm attribution accuracy

## Test Management & Analysis

### During Test Execution

#### **Monitoring Checklist (Daily)**
- [ ] Test is running without technical errors
- [ ] Traffic split is working as expected (50/50, etc.)
- [ ] No unusual patterns in data (bot traffic, etc.)  
- [ ] Conversion events are tracking properly
- [ ] No user complaints about broken functionality

#### **Weekly Review Process**
1. **Performance Check**: Are we on track for statistical significance?
2. **Qualitative Feedback**: Any user complaints or positive feedback?
3. **Technical Issues**: Any bugs or tracking problems?
4. **External Factors**: Marketing campaigns, seasonal changes affecting results?

### Results Analysis Framework

#### **Statistical Significance Requirements**
- **Minimum Sample Size**: 1,000 visitors per variation
- **Significance Level**: 95% confidence (p < 0.05)
- **Test Duration**: Minimum 2 weeks to account for weekly patterns
- **Practical Significance**: Minimum 5% improvement for major changes

#### **Analysis Template**

```markdown
# [Test Name] - Results Analysis

## Test Overview
- **Hypothesis**: [Original hypothesis]
- **Test Period**: [Start date] to [End date]
- **Total Visitors**: [Control: X, Treatment: Y]
- **Test Duration**: [X weeks]

## Primary Results
| Metric | Control | Treatment | Change | Confidence |
|--------|---------|-----------|---------|------------|
| Conversion Rate | X.X% | Y.Y% | +Z.Z% | 95% |

## Secondary Metrics
| Metric | Control | Treatment | Change | Notes |
|--------|---------|-----------|---------|-------|
| Time on Page | X:XX | Y:YY | +/-Z% | [Impact assessment] |
| Bounce Rate | X.X% | Y.Y% | +/-Z.Z% | [Impact assessment] |

## Key Insights
1. **Winner**: [Control/Treatment] with [X%] improvement
2. **Statistical Significance**: [Yes/No] at 95% confidence level
3. **Business Impact**: [Revenue/conversion impact estimate]

## Recommendations
- [ ] **Deploy Winner**: Implement winning variation site-wide
- [ ] **Further Testing**: Areas for follow-up experiments
- [ ] **Documentation**: Update style guides/templates with learnings
```

### Common Test Types & Templates

#### **1. Hero Section Optimization**

**Elements to Test**:
- Headlines and value propositions
- CTA button copy and colors  
- Background images vs videos
- Trust signals and testimonials

**Success Metrics**: Click-through rate, time on page, conversion rate

#### **2. Form Optimization**

**Elements to Test**:
- Number of form fields
- Field labels and placeholder text
- Progress indicators
- Required vs optional fields
- Privacy/security messaging

**Success Metrics**: Form completion rate, time to complete, abandonment rate

#### **3. Navigation & UX Tests**

**Elements to Test**:
- Menu structure and labels
- Search functionality prominence  
- Filter and sorting options
- Mobile navigation patterns

**Success Metrics**: Page depth, session duration, task completion rate

## Best Practices & Guidelines

### **Testing Do's**
✅ **Test One Element at a Time**: Easier to attribute results  
✅ **Run Tests for Full Weeks**: Account for weekly behavior patterns  
✅ **Document Everything**: Hypothesis, setup, results, decisions  
✅ **Consider External Factors**: Marketing campaigns, seasonality  
✅ **Plan Follow-up Tests**: Build on learnings systematically  

### **Testing Don'ts**
❌ **Don't Stop Tests Early**: Even if results look promising  
❌ **Don't Test Too Many Things**: Spreads traffic too thin  
❌ **Don't Ignore Mobile**: 60%+ of UAGC traffic is mobile  
❌ **Don't Test During Major Campaigns**: Can skew results  
❌ **Don't Deploy Without Full Analysis**: Consider all metrics  

### **UAGC-Specific Considerations**

#### **Student Journey Context**
- **Military Students**: Different motivations, benefits-focused messaging
- **Working Adults**: Time constraints, flexible scheduling emphasis  
- **Career Changers**: ROI focus, skill development messaging
- **First-Generation**: Support systems, success story emphasis

#### **Compliance & Accessibility**
- **FERPA Compliance**: Student data handling in forms
- **ADA Compliance**: Screen reader compatibility, color contrast
- **State Regulations**: Disclosure requirements, licensing information

## Resources & Tools

### **Internal Resources**
- [Analytics Standards](analytics-standards.md) - Tracking implementation
- [GTM Configuration](gtm-configuration-datalayer.md) - Event setup
- [Content Templates](content-templates.md) - Test documentation templates
- [QA Smoke Test](guides/qa-smoke-test.md) - Testing validation

### **External Tools**
- **[Optimizely](https://app.optimizely.com/)** - Primary testing platform
- **[GA4](https://analytics.google.com/)** - Analytics and goal tracking
- **[Hotjar](https://www.hotjar.com/)** - User behavior analysis
- **[Sample Size Calculator](https://www.optimizely.com/sample-size-calculator/)** - Test planning

### **Team Responsibilities**

| Role | Responsibility |
|------|----------------|
| **Anthony** | Test implementation, technical setup, QA validation |
| **Omar** | Analytics setup, performance monitoring, SEO impact |
| **Brian** | Design variations, accessibility compliance, UX review |
| **Thomas** | Test approval, business impact assessment, strategy |
| **Brandy** | Process compliance, documentation, stakeholder communication |

---

**Documentation Status**: ✅ Active  
**Test Program Status**: 🟢 Running  
**Next Program Review**: Quarterly Docs Day

:::info Need Help with Testing?
Contact **Anthony** for technical setup or **Omar** for analytics configuration. For strategic questions, reach out to **Thomas**.
:::
