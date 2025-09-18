# Canonical Links & URL Taxonomy

Comprehensive guide to implementing SEO-friendly URLs and canonical link management in Drupal for UAGC digital properties, ensuring optimal search engine visibility and user experience.

## Overview

Effective URL structure and canonical link implementation are critical for UAGC's digital marketing success. This guide provides technical implementation details for the latest Drupal version, focusing on clean URLs, duplicate content management, and SEO optimization for educational content.

**Why This Matters for UAGC:**
- **Student Experience**: Clean, descriptive URLs improve navigation and trust
- **SEO Performance**: Proper canonical implementation prevents duplicate content penalties
- **Brand Consistency**: Structured URLs reflect UAGC's organized approach to education
- **Analytics Clarity**: Meaningful URLs provide better tracking and reporting insights

## 1. Implementing Clean and Descriptive URLs

### Pathauto Module Configuration

Transform Drupal's default URLs from `/node/123` to meaningful, SEO-friendly paths like `/programs/bachelor-of-science-business-administration`.

#### **Module Installation and Setup**

```bash
# Install Pathauto via Composer (recommended for latest Drupal)
composer require drupal/pathauto

# Enable the module
drush en pathauto -y
```

**Alternative Installation:**
1. Navigate to **Extend** page in Drupal admin
2. Download Pathauto from [drupal.org/project/pathauto](https://www.drupal.org/project/pathauto)
3. Enable Pathauto and its dependencies (Token, CTools)

#### **UAGC-Specific URL Patterns**

**Navigate to:** Configuration > Search and metadata > URL aliases > Patterns

**Recommended Patterns for UAGC Content:**

| Content Type | Pattern | Example Output |
|--------------|---------|----------------|
| Academic Programs | `/online-degrees/[node:field_level]/[node:title]` | `/online-degrees/bachelors/business-information-systems` |
| Faculty Profiles | `/about/faculty/[node:title]` | `/about/faculty/dr-john-smith` |
| Blog Articles | `/blog/[node:created:custom:Y]/[node:created:custom:m]/[node:title]` | `/blog/2024/03/online-learning-best-practices` |
| Student Resources | `/student-experience/[node:field_category]/[node:title]` | `/student-experience/student-resources/scholarship-opportunities` |
| News & Events | `/google-news/[node:created:custom:Y-m-d]/[node:title]` | `/google-news/2024-03-15/spring-graduation-ceremony` |

#### **Advanced Configuration**

**Punctuation Settings:**
- Remove periods, commas, and special characters
- Replace spaces with hyphens
- Convert to lowercase for consistency

**Token Replacement:**
```php
// Custom token for UAGC degree level
[node:field_degree_level:entity:name]

// Program level integration with UAGC structure
/online-degrees/[node:field_degree_level:entity:name]/[node:title]
// Output: /online-degrees/bachelors/business-administration
```

#### **Bulk URL Generation**

After configuring patterns:
1. Navigate to **Configuration** > **Search and metadata** > **URL aliases**
2. Click **Bulk generate** tab
3. Select content types to update
4. Run bulk generation for existing content

:::tip UAGC Implementation Note
For large content migrations, run bulk generation during off-peak hours to minimize site performance impact. Consider running in batches for sites with 1000+ pages.
:::

#### **Advanced URL Pattern Examples**

**Taxonomy Term URL Optimization:**
```
# Configure Pathauto for taxonomy terms
/blog/[term:name]
# Output: /blog/student-success, /blog/online-learning

# Hierarchical taxonomy support for degree programs
/online-degrees/[term:parents:join-path]/[term:name]
# Output: /online-degrees/bachelors/business/management
```

**Content Hierarchy Reflection:**
```
# For student experience content categorization
/student-experience/[node:field_category:entity:name]/[node:title]
# Output: /student-experience/career-services/job-search-strategies

# For program-specific content
/online-degrees/[node:field_degree_level:entity:name]/[node:field_academic_interest:entity:name]/[node:title]
# Output: /online-degrees/bachelors/business/bachelor-business-administration
```

## 2. Managing Canonical URLs for Duplicate Content Prevention

### Metatag Module Implementation

Canonical tags inform search engines about the preferred version of content, crucial for UAGC's multi-platform presence.

#### **Module Installation and Configuration**

```bash
# Install Metatag module
composer require drupal/metatag

# Enable core Metatag modules
drush en metatag metatag_open_graph metatag_twitter_cards -y
```

#### **Global Canonical Configuration**

**Navigate to:** Configuration > Search and metadata > Metatag

**Global Settings:**
```html
<!-- Canonical URL token -->
<link rel="canonical" href="[node:url:absolute]" />

<!-- For UAGC multi-domain setup -->
<link rel="canonical" href="https://www.uagc.edu[node:url]" />
```

#### **Content-Type Specific Canonicals**

**Academic Programs:**
```html
<!-- Consolidate program variations to main degree page -->
<link rel="canonical" href="[node:field_canonical_program:entity:url:absolute]" />
<!-- Example: Point certificate programs to main degree when applicable -->
```

**Faculty Profiles:**
```html
<!-- Handle faculty appearing in multiple colleges -->
<link rel="canonical" href="https://www.uagc.edu/about/faculty/[node:title]" />
```

#### **Handling UAGC-Specific Duplicate Content Scenarios**

**1. Program Variations:**
```php
// Custom canonical logic for degree variants
if ($node->getType() == 'academic_program') {
  $canonical_program = $node->field_canonical_program->entity;
  if ($canonical_program) {
    $canonical_url = $canonical_program->toUrl('canonical', ['absolute' => TRUE])->toString();
  }
}
```

**2. Multi-Campus Content:**
```html
<!-- For content appearing on multiple UAGC platforms -->
<link rel="canonical" href="https://www.uagc.edu[current-page:url:path]" />
```

**3. Landing Page Variants:**
```php
// A/B testing landing pages - point to primary version
$canonical_mapping = [
  '/apply-now-variant-a' => '/apply-now',
  '/programs-landing-test' => '/programs',
  '/financial-aid-promo' => '/financial-aid'
];
```

## 3. URL Taxonomy Structure for Educational Content

### UAGC Information Architecture

Structure URLs to reflect UAGC's educational hierarchy and student journey.

#### **UAGC Website Architecture Overview**

The UAGC website follows a hierarchical structure organized into nine main content categories as defined in the [sitemap index](https://www.uagc.edu/sitemap.xml):

!!! info "Live Structure Reference"
    This structure reflects the actual UAGC website architecture as of 2024. For the most current sitemap, visit [uagc.edu/sitemap.xml](https://www.uagc.edu/sitemap.xml).

```
uagc.edu/
├── online-degrees/          # Academic program catalog
├── admissions/             # Enrollment processes and requirements
├── tuition-financial-aid/  # Financial information and aid
├── student-experience/     # Student support and services
├── partnerships/           # Corporate and academic partnerships
├── about/                  # Institutional information
├── blog/                   # Content marketing and news
├── google-news/           # Press releases and media
└── generic/               # Supporting pages and utilities
```

#### **Academic Program Pages**

**Main Academic Navigation Structure:**
- `/online-degrees/` - Main program catalog
  - `/online-degrees/bachelors/` - Bachelor's degree hub
  - `/online-degrees/masters/` - Master's degree hub
  - `/online-degrees/doctoral/` - Doctoral degree hub
  - `/online-degrees/associate/` - Associate degree hub
  - `/online-degrees/certificates/` - Certificate programs

**Programs by Academic Interest:**
- `/online-degrees/business/` - Business programs
- `/online-degrees/criminal-justice/` - Criminal justice programs
- `/online-degrees/education/` - Education programs
- `/online-degrees/health-care/` - Healthcare programs
- `/online-degrees/information-technology/` - IT programs
- `/online-degrees/liberal-arts/` - Liberal arts programs
- `/online-degrees/social-behavioral-science/` - Social & behavioral science

**Programs by College:**
- `/college-of-professional-advancement/` - Professional programs
- `/college-of-integrative-learning/` - Integrative studies

**Individual Program Pages Pattern:** `/online-degrees/[level]/[program-name]/`

**Examples:**
- `/online-degrees/bachelors/business-information-systems/`
- `/online-degrees/masters/health-care-administration/`
- `/online-degrees/doctoral/psychology/`

**Program Tools & Resources:**
- `/online-degrees/find-your-degree/` - Degree finder tool
- `/online-degrees/comparison/` - Degree comparison tool
- `/online-degrees/emphases/` - Area of emphasis options

#### **Information & Service Pages**

**Admissions Structure:**
- `/admissions/` - Main admissions hub
  - `/admissions/new-students/` - New student resources
  - `/admissions/returning-students/` - Returning student process
  - `/admissions/traditional/` - Traditional credit transfer
  - `/admissions/non-traditional/` - Non-traditional credit transfer
  - `/admissions/bachelors/` - Bachelor's admission requirements
  - `/admissions/masters/` - Master's admission requirements
  - `/admissions/doctorate/` - Doctoral admission requirements
  - `/admissions/associates/` - Associate admission requirements
  - `/admissions/international/` - International student requirements
  - `/admissions/registrar/` - Registrar services
  - `/admissions/week-in-the-life/` - Student experience preview

**Financial Aid Structure:**
- `/tuition-financial-aid/` - Main financial hub
  - `/tuition-financial-aid/scholarships/` - Scholarship information
  - `/tuition-financial-aid/grants/` - Grant programs
  - `/tuition-financial-aid/our-promise/` - 3-week trial promise
  - `/tuition-financial-aid/payment-options/` - Payment plans
  - `/tuition-financial-aid/faq/` - Financial aid FAQ

**Student Experience Structure:**
- `/student-experience/` - Main student support hub
  - `/student-experience/office-student-affairs/` - Student affairs
  - `/student-experience/student-support-services/` - Support services
  - `/student-experience/alumni/` - Alumni services
  - `/student-experience/peer-mentoring/` - Peer mentoring program
  - `/student-experience/career-services/` - Career support
  - `/student-experience/honor-societies/` - Honor societies
  - `/student-experience/student-resources/` - General resources
  - `/student-experience/graduation/` - Graduation information
  - `/student-experience/deans-list/` - Academic recognition
  - `/student-experience/transcript-request/` - Transcript services
  - `/student-experience/student-organizations/` - Student organizations
  - `/student-experience/writing-center/` - Writing support

**About UAGC Structure:**
- `/about/` - Institutional information hub
  - `/about/accreditation/` - Accreditation details
  - `/about/why-uagc/` - Value proposition
  - `/about/university-awards/` - Awards and recognition
  - `/about/professional-affiliations-memberships/` - Professional affiliations
  - `/about/leadership/` - Executive team
  - `/about/faculty/` - Faculty information
  - `/about/media-room/` - Press and media
  - `/about/contact-us/` - Contact information

#### **Military-Focused Pages**

**Military Structure:**
- `/military/` - Main military hub
  - `/military/active-duty/` - Active duty services
  - `/military/veterans/` - Veteran services
  - `/military/spouses-dependents/` - Military family services
  - `/military/tuition-financial-aid/` - Military financial benefits
  - `/military/air-force/` - Air Force specific
  - `/military/army/` - Army specific
  - `/military/coast-guard/` - Coast Guard specific
  - `/military/marines/` - Marines specific
  - `/military/navy/` - Navy specific
  - `/military/space-force/` - Space Force specific
  - `/military/admissions/transfer/` - Military credit transfer

**Military Alliance:**
- `/military-alliance/` - Military partnership programs

#### **Partnership Pages**

**Partnership Structure:**
- `/partnerships/` - Main partnership hub
  - `/partnerships/organizations/` - Corporate partnerships
  - `/partnerships/academic/` - Academic partnerships

#### **Content & News**

**Blog Structure:**
- `/blog/` - Main blog hub with educational content and thought leadership

**News & Media:**
- `/google-news/` - Press releases and news articles
- `/events/` - University events

#### **Specialized Domains & Platforms**

**Student Portals:**
- `login.uagc.edu/` - Student login portal
- `connect.uagc.edu/` - UAGC Connect community platform

**Application Platform:**
- `cloud.mail.uagc.edu/apply/` - Online application system

**International:**
- `china.uagc.edu/` - China-specific site

#### **Paid Campaign Pages**

- **Generic Campaign Pages**: `/success/[page-name]` or `/success/[page-name]-v[version]`
  - Examples: `/success/back-to-school-v5`, `/success/attend-v5`, `/success/get-ahead-v5`

- **Degree Type Landing Pages**: `/success/degree-types/[degree-level]`
  - Examples: 
    - `/success/degree-types/bachelors-degrees-v5`
    - `/success/degree-types/masters-degrees-v5` 
    - `/success/degree-types/doctoral-degrees-v5`

- **Program-Specific Pages**: `/success/degree/[program-name]`
  - Examples: 
    - `/success/degree/ba-business-economics-v5`
    - `/success/degree/ma-education-v5`
    - `/success/degree/doctorate-psychology-v5`

- **Field of Study Pages**: `/success/programs/[field-name]`
  - Examples: `/success/programs/business-v5`, `/success/programs/health-care-v5`

- **Military-Focused Pages**: `/success/military/[audience]`
  - Examples: `/success/military/active-duty-v5`, `/success/military/veteran-v5`

- **College-Specific Pages**: `/success/college/[college-name]`
  - Examples: `/success/college/forbes-business-school-v5`

#### **Paid Campaign URL Parameters**

Tracking parameters commonly added to paid URLs:
- `sourceid` - Campaign source identifier
- `affiliateID` - Affiliate tracking  
- `utm_vendor` - UTM vendor parameter
- `alr` - Audience/lead routing
- `dsaccountid` - Data source account ID
- `dsaccounttype` - Platform type (e.g., GOOGLE)
- `device` - Device targeting (m=mobile, etc.)
- Campaign-specific parameters: `adgroup`, `ad`, `match`, `clickid`

**Example Full Paid URL:**
```
https://www.uagc.edu/success/degree-types/bachelors-degrees-v5?sourceid=18SGB&affiliateID=&clickid=&utm_vendor=&alr=21995198608&adgroup=&ad=&match=&device=m&c3api=2591,,&sourceid=18SGB&dsaccountid=700000002770196&dsaccounttype=GOOGLE
```

#### **URL Conventions & Best Practices**

**Format Rules:**
- All URLs use **lowercase letters**
- Multi-word phrases separated by **hyphens** (`-`)
- No special characters or spaces
- Descriptive and SEO-friendly naming
- Consistent structure across degree levels

**SEO Considerations:**
- URLs should be descriptive of page content
- Avoid unnecessary parameters in organic URLs
- Maintain consistent hierarchy and structure
- Use keyword-rich paths when appropriate

**Technical Guidelines:**
- Keep URLs under 255 characters when possible
- Avoid deep nesting (typically max 4-5 levels)
- Use 301 redirects when changing URL structure
- Implement canonical URLs to prevent duplicate content

#### **SEO-Optimized URL Best Practices**

**1. Keyword Integration:**
- Include primary keywords naturally in URL structure
- Avoid keyword stuffing in path segments
- Use UAGC program terminology consistently

**2. Length Optimization:**
```
✅ Good: /online-degrees/bachelors/business-administration
❌ Too Long: /online-degrees/bachelors/college-of-business/department-of-business-administration/bachelor-of-science-business-administration-with-concentration-in-management
```

**3. Consistency Standards:**
- Use hyphens (not underscores) for word separation
- Maintain lowercase throughout
- Avoid special characters and numbers when possible

#### **Hierarchical Navigation Support**

**Breadcrumb Integration:**
```php
// Custom breadcrumb based on UAGC URL structure
$breadcrumbs = [
  'Home' => '/',
  'Online Degrees' => '/online-degrees',
  'Bachelor\'s Degrees' => '/online-degrees/bachelors',
  'Business' => '/online-degrees/business',
  $node->getTitle() => $node->toUrl()->toString()
];
```

## 4. Redirect Management and Link Integrity

### Drupal Redirect Module Implementation

Maintain SEO value and user experience during content restructuring.

#### **Module Installation**

```bash
# Install Redirect module
composer require drupal/redirect

# Enable redirect tracking
drush en redirect redirect_404 -y
```

#### **UAGC-Specific Redirect Scenarios**

**1. Program Name Changes:**
```php
// Redirect old program URLs to new UAGC naming convention
/programs/business-management → /online-degrees/bachelors/business-administration
/programs/mba-general → /online-degrees/masters/business-administration
```

**2. Department Restructuring:**
```
/faculty/business-department → /about/faculty
/resources/student-services → /student-experience/student-support-services
```

**3. Marketing Campaign URLs:**
```
/apply-now-spring-2024 → /admissions/apply (301 redirect)
/financial-aid-promotion → /tuition-financial-aid (301 redirect)
```

#### **Automated Redirect Configuration**

**Navigate to:** Configuration > Search and metadata > URL redirects

**Bulk Import Setup:**
```csv
source,redirect,status_code
"/old-programs/business","/online-degrees/bachelors/business",301
"/faculty-profiles","/about/faculty",301
"/student-resources","/student-experience/student-resources",301
```

#### **404 Error Monitoring**

**Enable 404 tracking:**
1. Navigate to **Reports** > **Page not found**
2. Monitor frequently accessed broken URLs
3. Create redirects for high-traffic 404s

**Custom 404 Handling:**
```php
// Suggest similar UAGC content for 404 errors
function uagc_custom_404_suggestions($path) {
  $suggestions = [];
  
  if (strpos($path, 'program') !== false || strpos($path, 'degree') !== false) {
    $suggestions[] = '/online-degrees';
  }
  
  if (strpos($path, 'apply') !== false) {
    $suggestions[] = '/admissions/apply';
  }
  
  if (strpos($path, 'financial') !== false || strpos($path, 'tuition') !== false) {
    $suggestions[] = '/tuition-financial-aid';
  }
  
  return $suggestions;
}
```

#### **Advanced Redirect Management**

**Automated Redirect Detection:**
```php
// Automatically create redirects when URL patterns change
function uagc_auto_redirect_creation($old_alias, $new_alias) {
  $redirect = Redirect::create([
    'redirect_source' => $old_alias,
    'redirect_redirect' => $new_alias,
    'status_code' => 301,
    'language' => 'en',
  ]);
  $redirect->save();
}
```

**Bulk Redirect Management:**
```bash
# Use Drush for bulk redirect operations
drush redirect:import /path/to/redirects.csv

# Check for redirect loops
drush redirect:fix-redirects

# Generate redirect report
drush redirect:list --format=csv > redirect_audit.csv
```

## 5. Technical Implementation Best Practices

### Performance Optimization

#### **URL Alias Caching**
```php
// Enable URL alias caching for performance
$settings['cache']['bins']['path_alias'] = 'cache.backend.database';

// Advanced caching for high-traffic sites
$settings['cache']['bins']['path_alias'] = 'cache.backend.redis';
$settings['redis.connection']['host'] = 'localhost';
$settings['redis.connection']['port'] = 6379;
```

#### **Canonical URL Caching**
```php
// Cache canonical URLs to reduce database queries
$config['metatag.settings']['cache_output'] = TRUE;

// Cache TTL optimization for educational content
$config['metatag.settings']['cache_maximum_age'] = 86400; // 24 hours
```

### Advanced Drupal SEO Configuration

#### **Clean URL Parameter Handling**
```php
// Remove unnecessary URL parameters for cleaner URLs
function uagc_url_cleanup() {
  $url_options = [
    'query' => [],
    'fragment' => '',
    'absolute' => FALSE,
  ];
  return $url_options;
}
```

#### **XML Sitemap Integration & Management**

UAGC implements an enterprise-level XML sitemap architecture that efficiently organizes content discovery for search engines while supporting the complex hierarchical structure of educational content.

##### **UAGC Sitemap Architecture Overview**

The UAGC website utilizes a **sitemap index structure** at [uagc.edu/sitemap.xml](https://www.uagc.edu/sitemap.xml) that references multiple specialized sitemaps, each optimized for specific content categories:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <!-- Core Academic Content -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-online-degrees.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Admissions & Enrollment -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-admissions.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Student Experience & Support -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-student-experience.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Financial Aid & Tuition -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-tuition-financial-aid.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Military & Veterans -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-military.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- About & Faculty -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-about.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Partnerships & Alliances -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-partnerships.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- Content Marketing -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-blog.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
  
  <!-- News & Media -->
  <sitemap>
    <loc>https://www.uagc.edu/sitemap-google-news.xml</loc>
    <lastmod>2024-01-15T10:30:00+00:00</lastmod>
  </sitemap>
</sitemapindex>
```

##### **Drupal Simple XML Sitemap Configuration**

**Initial Setup:**
```bash
# Install and enable sitemap generation
composer require drupal/simple_sitemap
drush en simple_sitemap -y

# Configure sitemap generation settings
drush config-set simple_sitemap.settings max_links_per_sitemap 50000
drush config-set simple_sitemap.settings remove_duplicates true
drush config-set simple_sitemap.settings skip_untranslated true
```

**UAGC Content Priority Configuration:**
```php
// Configure content type priorities in settings.php or custom module
$config['simple_sitemap.settings']['content_types'] = [
  // Highest Priority: Core Academic Content
  'academic_program' => [
    'priority' => '1.0',
    'changefreq' => 'monthly',
    'include_images' => true,
  ],
  
  // High Priority: Conversion-Focused Pages
  'admissions_page' => [
    'priority' => '0.9',
    'changefreq' => 'weekly', 
    'include_images' => true,
  ],
  
  // Important: Student Journey Support
  'student_resource' => [
    'priority' => '0.8',
    'changefreq' => 'monthly',
    'include_images' => false,
  ],
  
  // Standard: Informational Content
  'basic_page' => [
    'priority' => '0.7',
    'changefreq' => 'monthly',
    'include_images' => false,
  ],
  
  // Lower Priority: Blog and News
  'article' => [
    'priority' => '0.6',
    'changefreq' => 'never', // After initial publication
    'include_images' => false,
  ],
];
```

##### **Content Category Sitemap Segmentation**

**Academic Programs Sitemap** (`sitemap-online-degrees.xml`):
- All degree program pages with highest SEO priority
- Include program comparison pages and degree finder tools
- Priority: 1.0, Changefreq: monthly
- Include program images and multimedia content

**Admissions & Enrollment Sitemap** (`sitemap-admissions.xml`):
- Application pages, requirement information, and transfer credit
- High-conversion funnel pages with strong SEO value
- Priority: 0.9, Changefreq: weekly
- Exclude test/variant pages, include only canonical admission paths

**Student Experience Sitemap** (`sitemap-student-experience.xml`):
- Support services, career resources, alumni information
- Priority: 0.8, Changefreq: monthly
- Include student success stories and testimonials

**Military-Specific Sitemap** (`sitemap-military.xml`):
- Service branch pages, military benefits, spouse/dependent resources
- Priority: 0.9 (high value for military SEO)
- Changefreq: monthly, Include military partnership content

##### **Advanced Sitemap Configuration**

**Custom URL Inclusion Rules:**
```php
// Include only canonical URLs in sitemaps
function uagc_sitemap_url_filter($url, $url_variant, $entity, $entity_type) {
  // Exclude non-canonical program variants
  if ($entity_type === 'node' && $entity->bundle() === 'academic_program') {
    if ($entity->hasField('field_canonical_program') && 
        !$entity->field_canonical_program->isEmpty()) {
      return false; // Exclude non-canonical program variants
    }
  }
  
  // Exclude paid campaign landing pages from organic sitemap
  if (strpos($url, '/success/') === 0) {
    return false; 
  }
  
  // Include only published, indexable content
  return $entity->isPublished() && 
         !$entity->hasField('field_noindex') || 
         $entity->field_noindex->value == false;
}
```

**Automated Sitemap Generation:**
```bash
# Set up automated sitemap regeneration
drush cron-set simple_sitemap 'simple_sitemap:generate'

# Generate sitemaps programmatically after content updates
drush simple-sitemap:generate-batch

# Verify sitemap integrity
drush simple-sitemap:rebuild-queue
```

##### **SEO Optimization & Best Practices**

**URL Filtering & Clean Structure:**
- **Include Only Canonical URLs**: Prevent duplicate content indexing
- **Exclude Parameter-Heavy URLs**: Remove tracking parameters from sitemap URLs
- **Filter Paid Campaign Pages**: Keep `/success/` paths out of organic sitemaps
- **Include Only Published Content**: Automatic filtering of draft/unpublished pages

**Image Sitemap Integration:**
```php
// Include relevant images for degree programs and key pages
$config['simple_sitemap.settings']['include_images'] = [
  'academic_program' => true,    // Include program images
  'faculty_profile' => true,     // Include faculty photos  
  'student_resource' => false,   // Skip generic resource images
  'basic_page' => false,         // Exclude basic page images
];
```

**Mobile-First Sitemap Considerations:**
- Ensure all sitemap URLs are mobile-responsive
- Include AMP versions where applicable for blog content
- Validate mobile usability for all included URLs

##### **Monitoring & Maintenance Procedures**

**Google Search Console Integration:**
```bash
# Submit sitemaps to Google Search Console
# Primary sitemap index:
https://www.uagc.edu/sitemap.xml

# Individual category sitemaps for detailed monitoring:
https://www.uagc.edu/sitemap-online-degrees.xml
https://www.uagc.edu/sitemap-admissions.xml
https://www.uagc.edu/sitemap-military.xml
```

**Performance Monitoring:**
- **Weekly**: Monitor sitemap submission status in Search Console
- **Monthly**: Review sitemap indexing rates and coverage reports
- **Quarterly**: Audit sitemap structure for new content categories

**Error Detection & Resolution:**
```bash
# Check for sitemap errors
drush simple-sitemap:error-check

# Validate sitemap XML structure
xmllint --noout --schema sitemap.xsd sitemap.xml

# Monitor for 404s in submitted URLs
drush redirect:check-sitemap-urls
```

##### **Enterprise Sitemap Optimization**

**Large Site Considerations:**
- **Split by Content Category**: Maintain separate sitemaps for different content types
- **Limit URLs per Sitemap**: Keep under 50,000 URLs per individual sitemap
- **Compression Support**: Enable gzip compression for large sitemap files
- **CDN Integration**: Serve sitemaps through CDN for faster global access

**Content Freshness Management:**
```php
// Automatically update lastmod dates based on content changes
function uagc_update_sitemap_lastmod($entity) {
  if ($entity->getEntityTypeId() === 'node') {
    $sitemap_service = \Drupal::service('simple_sitemap.generator');
    $sitemap_service->rebuildQueue();
  }
}
```

**Multi-Domain Coordination:**
- **Cross-Domain Reference**: Include appropriate cross-references for `login.uagc.edu`, `connect.uagc.edu`
- **Subdomain Sitemaps**: Maintain separate sitemaps for specialized platforms
- **Canonical Coordination**: Ensure sitemaps reflect proper canonical relationships

##### **Quality Assurance Checklist**

**Pre-Deployment Validation:**
- [ ] All sitemap URLs return HTTP 200 status codes
- [ ] No redirect chains in submitted URLs (max 1 redirect per URL)
- [ ] All URLs use HTTPS protocol consistently
- [ ] Lastmod dates reflect actual content modification times
- [ ] No duplicate URLs across different category sitemaps
- [ ] Mobile-responsive validation for all submitted URLs

**Post-Deployment Monitoring:**
- [ ] Google Search Console shows successful sitemap submission
- [ ] No validation errors reported in Search Console
- [ ] Indexing rate improvements after sitemap optimization
- [ ] Coverage reports show expected URL inclusion/exclusion patterns

##### **Integration with Analytics & SEO Strategy**

**Search Console Integration:**
```javascript
// Track sitemap performance in GA4
gtag('event', 'sitemap_coverage', {
  'sitemap_category': 'online-degrees',
  'submitted_urls': 1245,
  'indexed_urls': 1198,
  'coverage_rate': 0.962
});
```

**Performance Impact Measurement:**
- Monitor organic discovery rates for new content
- Track indexing speed improvements
- Measure click-through rates from search results
- Analyze crawl budget efficiency improvements

This comprehensive sitemap strategy aligns with UAGC's complex content architecture while maintaining optimal SEO performance and search engine discoverability.

### Quality Assurance

#### **URL Testing Checklist**
- [ ] All URLs follow UAGC naming conventions (online-degrees, admissions, student-experience, etc.)
- [ ] Academic program URLs use `/online-degrees/[level]/[program-name]/` pattern
- [ ] Canonical tags point to correct preferred URLs (prefer www.uagc.edu)
- [ ] Redirects use appropriate status codes (301 vs 302)
- [ ] No redirect chains longer than 3 hops
- [ ] URLs are consistent across all UAGC properties (main site, login, connect subdomains)
- [ ] Military-specific URLs use `/military/[service-branch]/` structure
- [ ] Paid campaign URLs follow `/success/` patterns with proper tracking parameters

#### **SEO Validation Tools**
```bash
# Drupal console commands for URL auditing
drupal site:status
drupal database:table:debug path_alias
drupal config:export:view metatag.settings

# Additional Drush commands for SEO auditing
drush pathauto:update-all --all
drush simple-sitemap:rebuild-queue
drush redirect:list --status=301
```

#### **Regular URL Pattern Audits**

**Monthly Review Checklist:**
- [ ] **URL Consistency**: Ensure all new content follows established patterns
- [ ] **Broken Link Detection**: Use Link Checker module to identify issues
- [ ] **Canonical Tag Validation**: Verify proper canonical implementation
- [ ] **Redirect Chain Analysis**: Identify and resolve redirect loops
- [ ] **Performance Impact**: Monitor URL generation impact on site speed

**Automated Monitoring Setup:**
```php
// Custom hook to validate URL patterns
function uagc_entity_presave(Drupal\Core\Entity\EntityInterface $entity) {
  if ($entity->getEntityTypeId() === 'node') {
    $pattern_service = \Drupal::service('pathauto.generator');
    $alias = $pattern_service->createEntityAlias($entity, 'insert');
    
    // Validate URL meets UAGC standards
    if (!uagc_validate_url_pattern($alias)) {
      \Drupal::messenger()->addWarning('URL pattern may not meet UAGC standards.');
    }
  }
}
```

## 6. Monitoring and Maintenance

### Analytics Integration

#### **Google Analytics 4 Setup**
```javascript
// Track clean URLs in GA4 for UAGC content
gtag('config', 'GA_MEASUREMENT_ID', {
  page_title: document.title,
  page_location: window.location.href,
  custom_map: {
    'custom_parameter_1': 'degree_level',    // bachelors, masters, doctoral, associate
    'custom_parameter_2': 'academic_interest', // business, healthcare, technology, etc.
    'custom_parameter_3': 'student_type',    // traditional, military, working_adult
    'custom_parameter_4': 'funnel_stage'     // awareness, consideration, application, enrollment
  }
});

// Track UAGC-specific events
gtag('event', 'page_view', {
  'page_title': document.title,
  'page_location': window.location.href,
  'degree_level': getDegreeLevel(window.location.pathname),
  'military_affiliation': getMilitaryAffiliation(window.location.pathname)
});
```

#### **Search Console Monitoring**
- Monitor crawl errors and coverage issues
- Track canonical URL recognition
- Identify duplicate content warnings

### Regular Maintenance Tasks

#### **Monthly Audits**
1. **URL Structure Review**: Ensure new content follows established patterns
2. **Canonical Validation**: Check for self-referencing canonicals
3. **Redirect Chain Analysis**: Identify and fix redirect chains
4. **404 Error Resolution**: Create redirects for high-traffic broken URLs

#### **Quarterly Reviews**
1. **Pattern Updates**: Adjust Pathauto patterns based on content evolution
2. **Performance Analysis**: Review URL-related site speed metrics
3. **SEO Impact Assessment**: Analyze organic traffic changes by URL structure
4. **Competitor Benchmarking**: Compare URL strategies with other universities

## Implementation Checklist

### Phase 1: Foundation Setup
- [ ] Install and configure Pathauto module
- [ ] Install and configure Metatag module
- [ ] Install and configure Redirect module
- [ ] Set up UAGC-specific URL patterns

### Phase 2: Content Migration
- [ ] Run bulk URL generation for existing content
- [ ] Implement canonical tags for all content types
- [ ] Create redirects for changed URLs
- [ ] Update internal links to use new URL structure

### Phase 3: Quality Assurance
- [ ] Test URL patterns across all content types
- [ ] Validate canonical tag implementation
- [ ] Check redirect functionality
- [ ] Monitor 404 errors and site performance

### Phase 4: Optimization
- [ ] Set up analytics tracking for new URLs
- [ ] Configure Search Console monitoring
- [ ] Implement automated redirect suggestions
- [ ] Establish maintenance procedures
- [ ] Deploy XML sitemap automation
- [ ] Configure URL parameter cleanup
- [ ] Implement advanced caching strategies
- [ ] Set up automated URL pattern validation

---

## Best Practices Summary

### **Essential Drupal SEO Modules**
- **Pathauto**: Automated clean URL generation with custom patterns
- **Metatag**: Comprehensive meta tag and canonical URL management
- **Redirect**: 301 redirect handling and broken link prevention
- **Simple XML Sitemap**: Automated sitemap generation and submission
- **Link Checker**: Automated broken link detection and reporting

### **UAGC-Specific Implementation Standards**
- **URL Length**: Keep under 60 characters when possible for optimal sharing
- **Keyword Placement**: Primary keywords in first 3-5 words of URL
- **Consistency**: Uniform patterns across all content types and taxonomies
- **Accessibility**: URLs that work with screen readers and assistive technology
- **Analytics Integration**: UTM parameter handling without affecting clean URLs

### **Maintenance Schedule**
- **Weekly**: Monitor 404 errors and create necessary redirects, especially for high-traffic program pages
- **Monthly**: Review new content URL patterns, run SEO audits, and validate military-specific URL structure
- **Quarterly**: Update Pathauto patterns based on new program launches and content evolution
- **Bi-annually**: Review paid campaign URL effectiveness and tracking parameter optimization
- **Annually**: Comprehensive URL taxonomy review, competitive analysis, and UAGC brand alignment check

---

**Technical Support:** For Drupal-specific implementation questions, contact the Backend Development team.

**SEO Strategy:** For URL taxonomy and canonical link strategy, refer to the [SEO Guide](/guides/seo-hygiene).

**Performance Monitoring:** Track URL-related metrics in Google Analytics and Search Console for continuous optimization.

**This guide is based on latest Drupal best practices and is updated quarterly to reflect current SEO standards and UAGC content strategy evolution.**
