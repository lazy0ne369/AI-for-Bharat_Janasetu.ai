# Requirements Document: JanaSetu AI

## Introduction

JanaSetu AI is a government welfare scheme discovery platform designed to help Indian citizens find and understand relevant government schemes through AI-driven personalization. The platform addresses the critical problem of fragmented government welfare information across multiple portals and PDFs with complex legal language, enabling eligible beneficiaries to discover opportunities they would otherwise miss.

The system provides personalized scheme recommendations, simplifies complex government documents, enables regional language access, and provides proactive deadline alerts to reduce dependency on physical Common Service Centers (CSC).

## Glossary

- **User**: An Indian citizen seeking information about government welfare schemes
- **Scheme**: A government welfare program offering benefits to eligible citizens
- **Profile**: User-provided demographic and socioeconomic information
- **Eligibility_Engine**: AI-based component that matches users to relevant schemes
- **Document_Parser**: Component that extracts structured data from government PDFs
- **Conversational_Interface**: Text and voice-based AI chat system
- **Translation_Service**: Component that converts content between languages
- **Notification_Service**: Component that sends deadline alerts to users
- **Dashboard**: Unified interface displaying personalized scheme information
- **CSC**: Common Service Center - physical government service centers
- **LLM**: Large Language Model used for AI processing
- **Semantic_Extraction**: Process of extracting meaning and structure from unstructured text
- **Eligibility_Criteria**: Specific requirements a user must meet to qualify for a scheme
- **Document_Checklist**: List of required documents for scheme application
- **Regional_Language**: Indian languages other than English (Hindi, Tamil, Telugu, etc.)

## User Personas

### Persona 1: Rural Student (Priya)
- Age: 18, from rural Maharashtra
- Education: 12th grade completed
- Income: Family income ₹80,000/year
- Language: Marathi primary, limited English
- Needs: Scholarship information, skill development programs
- Challenges: Limited internet access, unfamiliar with government portals

### Persona 2: Small Farmer (Ravi)
- Age: 45, from Karnataka
- Occupation: 2-acre farmland owner
- Income: ₹1.5 lakh/year
- Language: Kannada primary, no English
- Needs: Agricultural subsidies, crop insurance, equipment loans
- Challenges: Low digital literacy, prefers voice interaction

### Persona 3: MSME Owner (Anjali)
- Age: 35, from Gujarat
- Occupation: Small textile business owner
- Income: ₹5 lakh/year
- Language: Gujarati and English
- Needs: Business loans, grants, skill training for employees
- Challenges: Time constraints, complex application processes

### Persona 4: Urban Low-Income Worker (Suresh)
- Age: 28, from Delhi
- Occupation: Daily wage worker
- Income: ₹2 lakh/year
- Language: Hindi primary, basic English
- Needs: Housing schemes, health insurance, skill programs
- Challenges: Unaware of available schemes, document gathering

## Requirements

### Requirement 1: User Profile Management

**User Story:** As a user, I want to create and maintain my profile with demographic and socioeconomic information, so that the system can recommend relevant schemes.

#### Acceptance Criteria

1. WHEN a new user accesses the platform, THE System SHALL prompt for profile creation
2. THE System SHALL collect age, income, education level, caste category, location, and occupation
3. WHEN a user provides income information, THE System SHALL validate it is a positive number
4. WHEN a user provides age information, THE System SHALL validate it is between 1 and 120
5. THE System SHALL allow users to update their profile information at any time
6. WHEN profile data is saved, THE System SHALL encrypt sensitive information before storage
7. THE System SHALL support profile creation in regional languages

### Requirement 2: AI-Based Eligibility Matching

**User Story:** As a user, I want the system to automatically identify schemes I am eligible for, so that I don't miss relevant opportunities.

#### Acceptance Criteria

1. WHEN a user profile is complete, THE Eligibility_Engine SHALL analyze all available schemes
2. THE Eligibility_Engine SHALL match user attributes against scheme eligibility criteria
3. WHEN multiple schemes match, THE Eligibility_Engine SHALL rank them by relevance score
4. THE Eligibility_Engine SHALL calculate relevance based on profile completeness, deadline proximity, and benefit amount
5. WHEN eligibility criteria include income thresholds, THE Eligibility_Engine SHALL apply exact numerical comparisons
6. WHEN eligibility criteria include categorical requirements, THE Eligibility_Engine SHALL perform exact string matching
7. THE Eligibility_Engine SHALL return results within 3 seconds for any user profile
8. WHEN a user profile is updated, THE Eligibility_Engine SHALL recalculate matching schemes

### Requirement 3: Government Document Ingestion

**User Story:** As a system administrator, I want to ingest government scheme PDFs and extract structured information, so that the platform has up-to-date scheme data.

#### Acceptance Criteria

1. WHEN a PDF document is uploaded, THE Document_Parser SHALL extract text content
2. THE Document_Parser SHALL identify scheme name, eligibility criteria, benefits, deadlines, and required documents
3. WHEN parsing fails for a document, THE Document_Parser SHALL log the error and continue processing other documents
4. THE Document_Parser SHALL use semantic extraction to identify eligibility criteria patterns
5. THE Document_Parser SHALL store extracted data in structured format in the database
6. WHEN a document contains tables, THE Document_Parser SHALL preserve table structure in extraction
7. THE Document_Parser SHALL handle documents in English and Hindi
8. WHEN duplicate schemes are detected, THE System SHALL update existing records rather than create duplicates

### Requirement 4: Personalized Scheme Recommendations

**User Story:** As a user, I want to see a personalized list of schemes ranked by relevance, so that I can focus on the most beneficial opportunities.

#### Acceptance Criteria

1. WHEN a user views the dashboard, THE Dashboard SHALL display schemes ranked by relevance score
2. THE Dashboard SHALL show scheme name, brief description, deadline, and estimated benefit amount
3. WHEN a scheme deadline is within 30 days, THE Dashboard SHALL highlight it with urgent status
4. THE Dashboard SHALL display only schemes where the user meets all eligibility criteria
5. WHEN no schemes match the user profile, THE Dashboard SHALL display suggestions to update profile
6. THE Dashboard SHALL support pagination when more than 20 schemes are available
7. WHEN a user clicks on a scheme, THE System SHALL display full details including eligibility, benefits, and application process

### Requirement 5: Conversational AI Interface

**User Story:** As a user, I want to interact with the system through natural language conversation, so that I can ask questions and get answers without navigating complex menus.

#### Acceptance Criteria

1. THE Conversational_Interface SHALL accept text input from users
2. THE Conversational_Interface SHALL accept voice input and convert it to text
3. WHEN a user asks about eligibility, THE Conversational_Interface SHALL provide personalized answers based on their profile
4. WHEN a user asks about application process, THE Conversational_Interface SHALL provide step-by-step instructions
5. WHEN a user asks about required documents, THE Conversational_Interface SHALL generate a checklist
6. THE Conversational_Interface SHALL respond within 3 seconds for any query
7. WHEN the LLM service is unavailable, THE Conversational_Interface SHALL provide fallback responses from cached templates
8. THE Conversational_Interface SHALL maintain conversation context for up to 10 exchanges
9. WHEN a user query is ambiguous, THE Conversational_Interface SHALL ask clarifying questions

### Requirement 6: Regional Language Support

**User Story:** As a non-English speaking user, I want to use the platform in my regional language, so that I can understand scheme information clearly.

#### Acceptance Criteria

1. THE System SHALL support Hindi, Tamil, Telugu, Kannada, Marathi, Gujarati, and Bengali
2. WHEN a user selects a language, THE Translation_Service SHALL translate all interface text
3. WHEN a user selects a language, THE Translation_Service SHALL translate scheme descriptions
4. THE Translation_Service SHALL preserve technical terms and scheme names in original language
5. WHEN translation fails for specific content, THE System SHALL display content in English with a notification
6. THE Conversational_Interface SHALL accept queries in the selected regional language
7. THE Conversational_Interface SHALL respond in the selected regional language

### Requirement 7: Deadline Monitoring and Notifications

**User Story:** As a user, I want to receive timely alerts about scheme deadlines, so that I don't miss application opportunities.

#### Acceptance Criteria

1. WHEN a scheme deadline is 30 days away, THE Notification_Service SHALL send an alert to eligible users
2. WHEN a scheme deadline is 7 days away, THE Notification_Service SHALL send a reminder to eligible users
3. WHEN a scheme deadline is 1 day away, THE Notification_Service SHALL send a final reminder to eligible users
4. THE Notification_Service SHALL support SMS and email notification channels
5. THE System SHALL allow users to configure notification preferences
6. WHEN a user has opted out of notifications, THE Notification_Service SHALL not send alerts
7. WHEN a scheme deadline is extended, THE Notification_Service SHALL notify affected users

### Requirement 8: Document Checklist Generation

**User Story:** As a user, I want to see a checklist of required documents for each scheme, so that I can prepare my application efficiently.

#### Acceptance Criteria

1. WHEN a user views scheme details, THE System SHALL display a document checklist
2. THE System SHALL extract document requirements from scheme data
3. THE System SHALL categorize documents as identity proof, income proof, address proof, or category-specific
4. THE System SHALL allow users to mark documents as collected
5. WHEN all documents are marked collected, THE System SHALL display application readiness confirmation
6. THE System SHALL provide guidance on how to obtain each document type

### Requirement 9: User Data Security and Privacy

**User Story:** As a user, I want my personal information to be secure and private, so that I can trust the platform with sensitive data.

#### Acceptance Criteria

1. WHEN user data is stored, THE System SHALL encrypt personally identifiable information
2. THE System SHALL use HTTPS for all data transmission
3. THE System SHALL implement authentication before allowing profile access
4. WHEN a user requests data deletion, THE System SHALL remove all personal information within 30 days
5. THE System SHALL not share user data with third parties without explicit consent
6. THE System SHALL log all access to user profiles for audit purposes
7. WHEN suspicious access patterns are detected, THE System SHALL lock the account and notify the user

### Requirement 10: Performance and Scalability

**User Story:** As a platform operator, I want the system to handle high user load efficiently, so that all users have a responsive experience.

#### Acceptance Criteria

1. THE System SHALL respond to user queries within 3 seconds under normal load
2. THE System SHALL support 1000 concurrent users without performance degradation
3. THE System SHALL scale to support 1 million registered users
4. WHEN database queries exceed 2 seconds, THE System SHALL use caching to improve response time
5. THE System SHALL implement rate limiting to prevent abuse
6. WHEN system load exceeds 80% capacity, THE System SHALL trigger auto-scaling

### Requirement 11: Low Bandwidth Mode

**User Story:** As a user with limited internet connectivity, I want to access essential features with minimal data usage, so that I can use the platform despite network constraints.

#### Acceptance Criteria

1. THE System SHALL provide a low bandwidth mode option
2. WHEN low bandwidth mode is enabled, THE System SHALL reduce image quality and disable non-essential animations
3. WHEN low bandwidth mode is enabled, THE System SHALL compress text responses
4. THE System SHALL cache frequently accessed scheme data locally
5. WHEN network connectivity is lost, THE System SHALL allow users to view cached content
6. THE System SHALL display data usage estimates for each operation

### Requirement 12: Fault Tolerance and Availability

**User Story:** As a platform operator, I want the system to remain available even when components fail, so that users can access critical information reliably.

#### Acceptance Criteria

1. THE System SHALL maintain 99% uptime over any 30-day period
2. WHEN the LLM service is unavailable, THE Conversational_Interface SHALL use rule-based fallback responses
3. WHEN the Translation_Service is unavailable, THE System SHALL display content in English
4. WHEN the Notification_Service is unavailable, THE System SHALL queue notifications for retry
5. THE System SHALL implement health checks for all critical components
6. WHEN a component fails health checks, THE System SHALL alert administrators
7. THE System SHALL implement automatic retry logic for transient failures

### Requirement 13: Scheme Search and Filtering

**User Story:** As a user, I want to search and filter schemes by category, deadline, or benefit type, so that I can find specific opportunities quickly.

#### Acceptance Criteria

1. THE System SHALL provide a search interface accepting keywords
2. WHEN a user enters search terms, THE System SHALL return schemes matching name or description
3. THE System SHALL support filtering by scheme category (education, agriculture, business, housing, health)
4. THE System SHALL support filtering by deadline range
5. THE System SHALL support filtering by benefit amount range
6. WHEN multiple filters are applied, THE System SHALL return schemes matching all criteria
7. THE System SHALL display search results within 2 seconds

### Requirement 14: Application Tracking

**User Story:** As a user, I want to track the status of my scheme applications, so that I know where I stand in the process.

#### Acceptance Criteria

1. THE System SHALL allow users to record scheme applications
2. THE System SHALL track application status (not started, in progress, submitted, approved, rejected)
3. WHEN a user updates application status, THE System SHALL record the timestamp
4. THE Dashboard SHALL display all tracked applications with current status
5. THE System SHALL allow users to add notes to each application
6. THE System SHALL send reminders for applications marked as in progress for more than 30 days

### Requirement 15: Analytics and Reporting

**User Story:** As a platform operator, I want to track usage metrics and user behavior, so that I can improve the platform and measure success.

#### Acceptance Criteria

1. THE System SHALL track number of registered users
2. THE System SHALL track number of scheme views per scheme
3. THE System SHALL track number of searches performed
4. THE System SHALL track conversation interactions with the Conversational_Interface
5. THE System SHALL track notification delivery success rates
6. THE System SHALL generate weekly reports on platform usage
7. THE System SHALL calculate scheme discovery success rate (schemes viewed vs schemes applied)
8. THE System SHALL not include personally identifiable information in analytics data

## Assumptions and Constraints

### Assumptions

1. Government scheme data is available in PDF format from public sources
2. Users have access to mobile devices or computers with internet connectivity
3. Users are willing to provide accurate profile information
4. AWS Bedrock LLM service will remain available and cost-effective
5. Regional language translation quality is sufficient for user comprehension
6. Users have valid mobile numbers or email addresses for notifications

### Constraints

1. Development must be completed within hackathon timeframe (limited time)
2. No direct API access to government databases
3. Must rely on publicly available government documents
4. LLM usage must be cost-efficient to maintain platform sustainability
5. System must work with limited infrastructure budget
6. Cannot guarantee 100% accuracy of eligibility matching due to document parsing limitations
7. Regional language support limited to 7 major Indian languages initially

## Risk Analysis

### Technical Risks

1. **PDF Parsing Accuracy**: Government PDFs may have inconsistent formats
   - Mitigation: Implement robust error handling and manual review process

2. **LLM Service Availability**: AWS Bedrock may experience outages
   - Mitigation: Implement fallback rule-based responses

3. **Translation Quality**: Automated translation may produce incorrect meanings
   - Mitigation: Use human review for critical content, provide English fallback

4. **Scalability**: Sudden user growth may overwhelm infrastructure
   - Mitigation: Implement auto-scaling and load testing

### Data Risks

1. **Outdated Scheme Information**: Government schemes may change without notice
   - Mitigation: Implement regular data refresh process and display last-updated timestamps

2. **Incomplete Eligibility Data**: Some schemes may have unclear eligibility criteria
   - Mitigation: Flag schemes with incomplete data and encourage user verification

### User Adoption Risks

1. **Digital Literacy**: Target users may struggle with technology
   - Mitigation: Provide voice interface and simple UI design

2. **Trust**: Users may not trust AI recommendations
   - Mitigation: Provide transparency about matching logic and encourage verification

## Success Metrics

### Primary Metrics

1. **Eligibility Matching Accuracy**: >80% precision in scheme recommendations
   - Measured by user feedback on relevance of recommended schemes

2. **User Satisfaction Score**: >4.0 out of 5.0
   - Measured through in-app surveys

3. **Time to Discover Schemes**: <5 minutes from profile creation to viewing recommendations
   - Measured through analytics tracking

4. **Scheme Awareness Increase**: 50% of users discover schemes they were previously unaware of
   - Measured through user surveys

### Secondary Metrics

1. **User Retention**: 60% of users return within 30 days
2. **Notification Engagement**: 40% of users act on deadline notifications
3. **Conversation Success Rate**: 70% of conversational queries resolved without escalation
4. **Regional Language Adoption**: 50% of users prefer non-English interface
5. **Application Completion Rate**: 30% of viewed schemes result in tracked applications

### Technical Metrics

1. **System Uptime**: 99% availability
2. **Response Time**: <3 seconds for 95th percentile
3. **Error Rate**: <1% of requests result in errors
4. **LLM Cost per User**: <₹10 per month per active user

## Out of Scope

The following items are explicitly out of scope for the initial release:

1. Direct scheme application submission through the platform
2. Integration with government application tracking systems
3. Document upload and verification
4. Payment processing for scheme fees
5. Video content or tutorials
6. Offline mobile application
7. Integration with Aadhaar or other government identity systems
8. Support for languages beyond the initial 7 regional languages
9. Scheme comparison tools
10. Community forums or user-to-user communication

## Future Enhancements

Potential features for future releases:

1. Direct application submission integration
2. Document scanning and OCR for automatic profile completion
3. AI-powered application form filling assistance
4. Scheme impact tracking (benefits received)
5. Expanded language support
6. Integration with government identity verification systems
7. Offline mode with full functionality
8. Scheme comparison and recommendation explanations
9. Success stories and testimonials from beneficiaries
10. Integration with CSC centers for assisted applications
