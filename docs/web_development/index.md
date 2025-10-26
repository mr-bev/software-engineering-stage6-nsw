Secure Software Architecture and Programming for the Web have been blended as they have significant conceptual overlaps that makes integration more effective:

- Authentication, authorisation, and encryption appear in both
- Security concepts are more meaningful when applied to real web projects
- Students can immediately see the "why" behind security practices
- Web development without security feels incomplete and outdated

## Course Overview

**Duration**: 16 weeks (5-6 hours per week)  
**Approach**: Blended integration of Secure Software Architecture and Programming for the Web  

!!! note
    This is work in progress. The contents on this page may change as the course details are created.

## Phase 1: Web Fundamentals & Security Awareness

**Duration**: Weeks 1-3

### Week 1: How the Web Works

**Learning Objectives**:

- Explain how data is transferred across the internet
- Identify different web protocols and their purposes
- Distinguish between secure and insecure connections
- Use browser developer tools to analyse network traffic

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Investigate how data is transferred on the internet (data packets, IP addresses IPv4, DNS)
- ✓ Investigate and describe web protocols and ports (HTTP, HTTPS, TCP/IP, DNS)
- ✓ Explore and explain the influence of a web browser on web development, including dev tools

*Secure Software Architecture:*

- ✓ Describe benefits of developing secure software (data protection, minimising cyber attacks)
- ✓ Explore fundamental security concepts (introduction to confidentiality, integrity, availability)

**Content Overview**:

- Complete journey of a web request from URL to rendered page
- Data packets and how information travels across networks
- IPv4 addressing and DNS resolution
- HTTP vs HTTPS comparison with security implications
- Browser developer tools (Network tab, Console, Elements)
- Introduction to why security matters on the web


### Week 2: Web Protocols & Security Foundations

**Learning Objectives**:

- Describe the function and security features of key web protocols
- Explain encryption fundamentals and SSL/TLS operation
- Analyse SSL certificates to verify secure connections
- Understand hash values and digital signatures

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Investigate and describe web protocols and ports (FTP, SFTP, SSL, TLS, SMTP, POP3, IMAP)
- ✓ Explain processes for securing the web (SSL certificates, encryption algorithms, encryption keys, plain text and cipher text, authentication and authorisation, hash values, digital signatures)

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (confidentiality, integrity, availability)

**Content Overview**:

- Deep dive into protocol functions and port numbers
- File transfer protocols: FTP vs SFTP security comparison
- Email protocols: SMTP, POP3, IMAP
- SSL/TLS handshake process and certificate infrastructure
- Symmetric vs asymmetric encryption
- Introduction to hashing and digital signatures
- Authentication and authorisation concepts
- Plain text vs cipher text demonstrations

### Week 3: Introduction to Web Development & Security Mindset

**Learning Objectives**:

- Create basic web pages using HTML and CSS
- Apply W3C standards for accessibility and security
- Recognise potential security vulnerabilities in web applications
- Explain the role of W3C in web development

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Explore applications of web programming (interactive websites, e-commerce, PWAs)
- ✓ Investigate and explain the role of W3C (WAI, internationalisation, web security, privacy, machine-readable data)

*Secure Software Architecture:*

- ✓ Describe benefits of developing secure software (data protection, minimising attacks and vulnerabilities)
- ✓ Describe how capabilities and experience of end users influence secure design features

**Content Overview**:

- HTML structure and semantic elements
- Basic CSS for styling
- W3C standards and their importance
- Web Accessibility Initiative (WAI) guidelines
- Introduction to web security and privacy standards
- Machine-readable data formats
- Real-world examples of hacked websites
- Security by design mindset introduction
- End user considerations in design

## Phase 2: Front-End Development & Input Security

**Duration**: Weeks 4-6  

### Week 4: JavaScript Fundamentals & Client-Side Security

**Learning Objectives**:

- Develop interactive web pages using JavaScript
- Implement input validation and sanitisation
- Demonstrate and prevent Cross-Site Scripting (XSS) attacks
- Apply defensive programming practices for client-side code

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Model elements that form a web development system (client-side/front-end web programming)

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (authentication, authorisation, accountability)
- ✓ Design, develop and implement code using defensive data input handling practices (input validation, sanitisation, error handling)
- ✓ Design, develop and implement secure code to minimise vulnerabilities in user action controls (cross-site scripting XSS)
- ✓ Apply security features for data protection, security, privacy and regulatory compliance

**Content Overview**:

- JavaScript basics: variables, data types, functions, events
- DOM manipulation and event handling
- Interactive form creation
- XSS vulnerability demonstration (controlled environment)
- Input validation techniques
- HTML escaping and sanitisation
- Regular expressions for input patterns
- Client-side error handling
- Security vs usability balance

### Week 5: CSS Frameworks, Version Control & Secure Development Lifecycle

**Learning Objectives**:

- Apply CSS frameworks to create responsive, accessible designs
- Use Git for version control and collaboration
- Explain the software development lifecycle with security integration
- Understand how end-user capabilities influence design decisions

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Investigate CSS and its impact (consistency, flexibility, maintenance tools)
- ✓ Investigate reasons for version control and apply it when developing web applications
- ✓ Explore types and significance of code libraries for front-end development (frameworks, predesigned CSS classes)
- ✓ Investigate methods to support and manage load times of web pages/applications
- ✓ Design and apply UI/UX principles (font, colour, navigation)
- ✓ Design UI that considers accessibility and inclusivity

*Secure Software Architecture:*

- ✓ Interpret and apply fundamental software development steps (requirements definition, specifications, design, development, integration, testing and debugging)
- ✓ Describe how capabilities and experience of end users influence secure design features
- ✓ Use and explain 'privacy by design' approach (proactive not reactive, embed privacy into design)

**Content Overview**:

- CSS frameworks (Bootstrap/Tailwind)
- Responsive design principles
- Predesigned CSS classes for consistency
- Load time optimisation (CDN vs local hosting)
- Git fundamentals: init, add, commit, push, pull
- Branching strategies and merge workflows
- Version control for secure development
- Software Development Lifecycle (SDLC): requirements → design → develop → test → deploy → maintain
- Security by design approach
- Privacy by design principles
- Accessibility considerations (WCAG guidelines)
- End user technical literacy and design implications

### Week 6: Advanced Client-Side Security & User Experience

**Learning Objectives**:

- Prevent Cross-Site Request Forgery (CSRF) attacks
- Implement secure session management concepts on client-side
- Create accessible and secure user authentication interfaces
- Apply privacy by design principles in user interfaces

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Design and apply UI/UX principles (font, colour, audio, video, navigation)
- ✓ Design UI that considers accessibility and inclusivity

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (authentication, authorisation, accountability)
- ✓ Design, develop and implement secure code to minimise vulnerabilities (cross-site request forgery CSRF)
- ✓ Design, develop and implement code considering efficient execution (session management)
- ✓ Use and explain 'privacy by design' approach (respect for user privacy)
- ✓ Apply security features for data protection, privacy and regulatory compliance

**Content Overview**:

- CSRF attacks explained and demonstrated
- CSRF token implementation (client-side)
- Introduction to session management
- Authentication vs authorisation (front-end perspective)
- Secure login form design
- Password strength indicators
- Accessible error messages (security without revealing system details)
- ARIA attributes for screen readers
- Keyboard navigation
- Color contrast and visual accessibility
- Privacy by design: data minimisation in forms
- User privacy controls and preferences
- Multi-factor authentication user flows

## Phase 3: Back-End Development & Core Security

**Duration**: Weeks 7-10  

### Week 7: Server-Side Programming, Authentication & Template Engines

**Learning Objectives**:
- Set up and configure a web server
- Implement secure password hashing and authentication
- Use template engines to render dynamic content
- Apply cryptography in authentication systems

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Model elements that form a web development system (server-side/back-end web programming)
- ✓ Observe and describe back-end process used to manage web request (webserver software, web framework, objects, libraries)
- ✓ Develop web application using appropriate scripting language
- ✓ Explore types and significance of code libraries (template engines)

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (authentication, authorisation, accountability)
- ✓ Use and explain the contribution of cryptography to 'security by design' approach
- ✓ Design, develop and implement code using defensive data input handling practices (input validation, sanitisation, error handling)
- ✓ Design, develop and implement secure code to minimise vulnerabilities (broken authentication and session management)

**Content Overview**:

- Webserver software (Apache, Nginx, Node.js, Python servers)
- Web frameworks (Express, Flask, Django)
- Complete request-response cycle
- Server-side routing and endpoints
- Template engines (EJS, Jinja2, Handlebars)
- Rendering dynamic HTML from server
- Password hashing (bcrypt, scrypt, argon2)
- Never store plain text passwords
- Password salting
- Secure authentication logic
- Session creation and management
- Server-side validation and sanitisation
- Error handling and exception management

### Week 8: Database Integration, SQL Injection Prevention & REST Principles

**Learning Objectives**:

- Connect web applications to databases
- Write secure SQL queries using prepared statements
- Prevent SQL injection attacks
- Apply RESTful design principles to API endpoints
- Understand database scaling for large datasets

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Model elements that form a web development system (interfacing with databases based on SQL or non-SQL)
- ✓ Observe and describe back-end process (databases)
- ✓ Develop web application with shell scripts (make files and directories, searching for text)
- ✓ Apply web-based database and construct script that executes SQL (selecting fields, 'group by', common SQL queries, constraints using WHERE, table joins)
- ✓ Compare Object-Relational Mapping (ORM) to SQL
- ✓ Investigate effect of big data on web architecture (data mining, metadata - introduction)

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (confidentiality, integrity, availability)
- ✓ Design, develop and implement code using defensive data input handling practices (input validation, sanitisation)
- ✓ Apply security features for data protection

**Content Overview**:

- SQL vs NoSQL database overview
- Database schema design principles
- Connecting server to database
- SQL queries: SELECT, INSERT, UPDATE, DELETE
- WHERE clauses and constraints
- GROUP BY for data aggregation
- Table joins (INNER, LEFT, RIGHT)
- SQL injection vulnerability demonstration
- Parameterised queries / prepared statements
- Object-Relational Mapping (ORM) tools
- ORM vs raw SQL comparison
- Shell scripts for database management
- Bash commands for file operations
- Introduction to RESTful API principles
- REST conventions (GET, POST, PUT, DELETE)
- JSON request/response format
- Database indexing for performance
- Introduction to data mining concepts
- Metadata management in databases

### Week 9: Advanced Authentication, Authorisation & Session Management

**Learning Objectives**:

- Implement comprehensive authentication and authorisation systems
- Apply role-based access control (RBAC)
- Secure session management with best practices
- Prevent broken authentication vulnerabilities
- Handle race conditions in concurrent requests

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Assess contribution of back-end web development to success of web application
- ✓ Investigate effect of big data on web architecture (streaming service management - scalability)

*Secure Software Architecture:*

- ✓ Explore fundamental security concepts (authentication, authorisation, accountability)
- ✓ Use and explain contribution of cryptography to 'security by design' approach
- ✓ Design, develop and implement code considering efficient execution (memory management, session management, exception management)
- ✓ Design, develop and implement secure code to minimise vulnerabilities (broken authentication and session management, invalid forwarding and redirecting, race conditions)
- ✓ Apply security features for data protection, security, privacy and regulatory compliance

**Content Overview**:

- Authentication: "Who are you?" (verification methods)
- Authorisation: "What can you do?" (permissions and roles)
- Accountability: Logging and audit trails
- Role-based access control (RBAC) implementation
- User roles: admin, user, moderator, etc.
- Protected routes and middleware
- Session creation, storage, and destruction
- Secure session cookies (httpOnly, secure, sameSite flags)
- Session hijacking prevention
- Session fixation vulnerabilities
- Session timeout and expiration
- Broken authentication vulnerabilities
- Rate limiting for brute force prevention
- Multi-factor authentication concepts
- Exception management and error handling
- Try-catch blocks for database operations
- Generic error messages to users
- Detailed logging for developers
- Race conditions in authentication
- Time-of-check to time-of-use (TOCTOU) vulnerabilities
- Database locks and atomic operations
- Memory management for session storage
- Session storage at scale (distributed systems)
- Invalid redirects and forwards prevention

### Week 10: File Security, Safe APIs & Cryptography in Practice

**Learning Objectives**:

- Implement secure file upload handling
- Prevent file-based attacks and path traversal
- Design and implement safe RESTful APIs
- Apply cryptography for data protection
- Understand API security in context of big data and streaming

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Observe and describe back-end process (objects, libraries)
- ✓ Investigate effect of big data on web architecture (streaming service management - API rate limiting)
- ✓ Describe how collaborative work practices between front-end and back-end developers improve development (API contracts)

*Secure Software Architecture:*

- ✓ Use and explain contribution of cryptography to 'security by design' approach
- ✓ Design, develop and implement a safe API to minimise software vulnerabilities
- ✓ Design, develop and implement secure code to protect user file and hardware vulnerabilities from file attacks and side channel attacks
- ✓ Apply security features for data protection, security, privacy and regulatory compliance

**Content Overview**:

- File upload vulnerabilities
- Unrestricted file upload attacks
- Path traversal attacks (../../etc/passwd)
- File inclusion vulnerabilities
- Side channel attacks (timing attacks, cache attacks)
- Secure file handling practices
- File type validation (magic numbers, not just extensions)
- File name sanitisation
- Storing files outside web root
- File size limits and scanning
- File permissions and access control
- RESTful API design and implementation
- API endpoint security
- JWT (JSON Web Tokens) for API authentication
- API rate limiting and throttling
- Input validation for API requests
- CORS (Cross-Origin Resource Sharing) policies
- API versioning strategies
- Practical cryptography implementation
- Encrypting sensitive data at rest
- Encrypting data in transit
- Key management strategies
- Environment variables for secrets
- Never hard-code encryption keys
- API security for big data applications
- Streaming service security considerations
- API contracts for front-end/back-end collaboration

## Phase 4: Secure Architecture & Progressive Web Apps

**Duration**: Weeks 11-14

### Week 11: Progressive Web Apps & Privacy by Design

**Learning Objectives**:

- Design and implement Progressive Web Apps (PWAs)
- Apply privacy by design principles throughout development
- Create installable, offline-capable web applications
- Implement comprehensive UI/UX with accessibility

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Explore applications of web programming (progressive web apps)
- ✓ Design, develop and implement a progressive web app (PWA)
- ✓ Application of UI and UX principles (font, colour, audio, video, navigation)
- ✓ UI that considers accessibility and inclusivity

*Secure Software Architecture:*

- ✓ Use and explain 'privacy by design' approach (proactive not reactive, embed privacy into design, respect for user privacy)
- ✓ Use and explain contribution of sandboxing to 'security by design' approach
- ✓ Apply security features for data protection, security, privacy and regulatory compliance
- ✓ Describe how capabilities and experience of end users influence secure design features

**Content Overview**:

- Progressive Web App characteristics
- Service workers for offline functionality
- Web app manifest configuration
- Installable web applications
- Push notifications
- Cache strategies (cache-first, network-first, stale-while-revalidate)
- Privacy by design principles
- Proactive privacy approach (not reactive)
- Privacy as default setting
- Embedding privacy into design from start
- Full lifecycle data protection
- Respect for user privacy and control
- Data minimisation principles
- Privacy-preserving technologies
- GDPR and privacy regulation compliance
- Cookie consent implementation
- Privacy policy and transparency
- User data dashboard (view/download/delete)
- Data retention policies
- Sandboxing concepts
- Browser sandboxing (iframes, same-origin policy)
- Isolating code execution
- Container concepts for deployment
- UI/UX design principles
- Typography and color theory
- Multimedia integration (images, audio, video)
- Accessible navigation
- Responsive design for all devices
- ARIA attributes and screen reader support
- Keyboard navigation
- Alternative text and captions
- Designing for diverse user capabilities

### Week 12: Testing Strategies & Security Hardening

**Learning Objectives**:

- Apply multiple security testing methodologies
- Conduct code reviews with security focus
- Use SAST and DAST tools to find vulnerabilities
- Perform vulnerability assessments and penetration testing
- Harden systems against security threats

**Syllabus Coverage**:

*Secure Software Architecture:*

- ✓ Interpret and apply fundamental software development steps (testing and debugging)
- ✓ Test and evaluate security and resilience of software by determining vulnerabilities, hardening systems
- ✓ Apply and evaluate strategies used by software developers to manage security of programming code (code review, SAST, DAST, vulnerability assessment, penetration testing)
- ✓ Use and explain contribution of sandboxing to 'security by design' approach

**Content Overview**:

- Comprehensive testing strategies
- Code review best practices
- Security-focused code review checklist
- Peer review workflows
- Automated code review tools (linters)
- Static Application Security Testing (SAST)
- Source code analysis without execution
- SAST tools: SonarQube, ESLint security plugins, Bandit
- Identifies: SQL injection, XSS, hard-coded secrets, buffer overflows
- Integration into development workflow
- Dynamic Application Security Testing (DAST)
- Testing running applications (black-box)
- DAST tools: OWASP ZAP, Burp Suite
- Identifies: runtime vulnerabilities, configuration issues, auth problems
- Simulating real attacks
- Vulnerability assessment
- Systematic security weakness examination
- Risk rating and prioritisation
- Automated scanners plus manual testing
- Penetration testing
- Authorised simulated attacks
- Ethical hacking methodology
- Red team vs blue team exercises
- Finding exploitable vulnerabilities
- System hardening techniques
- Remove unnecessary dependencies
- Update libraries to latest secure versions
- Implement security headers (CSP, X-Frame-Options, HSTS)
- Configure secure defaults
- Disable directory listing
- Remove debug code and comments
- Sandboxing for testing
- Container isolation (Docker concepts)
- Virtual machines for testing
- Limiting blast radius of vulnerabilities

### Week 13: Business Continuity, Disaster Recovery & Open Source

**Learning Objectives**:

- Develop incident response and disaster recovery plans
- Implement business continuity strategies
- Handle security breaches appropriately
- Evaluate open-source software and CMS platforms
- Understand big data backup and recovery strategies

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Explain use and development of open-source software in relation to web development
- ✓ Research, experiment with and evaluate prevalence and use of web content management systems (CMS)
- ✓ Investigate effect of big data on web architecture (backup and recovery at scale)

*Secure Software Architecture:*

- ✓ Interpret and apply fundamental software development steps (installation, maintenance)
- ✓ Test and evaluate security and resilience of software (handling breaches, maintaining business continuity, conducting disaster recovery)

**Content Overview**:

- Security breach handling
- Incident response plan development
- Detection and analysis procedures
- Containment strategies
- Eradication and recovery steps
- Post-incident review and lessons learned
- Communication protocols (users, stakeholders, regulators)
- Business continuity planning
- Keeping critical functions operational during incidents
- Redundancy and failover systems
- High availability architecture
- Disaster recovery planning
- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)
- Backup strategies (3-2-1 rule: 3 copies, 2 media types, 1 offsite)
- Regular backup testing
- Database replication
- Cloud-based disaster recovery
- Monitoring and alerting systems
- Installation and deployment considerations
- Maintenance phase of SDLC
- Patch management
- Security updates and vulnerability remediation
- Open-source software in web development
- Benefits: community support, transparency, cost, flexibility
- Security considerations: code vetting, vulnerability disclosure
- Contributing to open source
- Licenses (MIT, GPL, Apache) and compliance
- Content Management Systems (CMS)
- WordPress, Drupal, Joomla comparison
- Headless CMS (Strapi, Contentful, Sanity)
- When to use CMS vs custom development
- CMS security: plugin vulnerabilities, update management
- Industry prevalence evaluation
- Big data backup and recovery
- Backing up large-scale databases
- Streaming service continuity

### Week 14: Collaborative Development & Professional Practices

**Learning Objectives**:

- Apply collaborative development practices in teams
- Delegate tasks based on expertise
- Improve solution quality through collaboration
- Integrate front-end and back-end development
- Demonstrate professional software development workflows

**Syllabus Coverage**:

*Programming for the Web:*

- ✓ Describe how collaborative work practices between front-end and back-end developers improve development of web solution

*Secure Software Architecture:*

- ✓ Interpret and apply fundamental software development steps (complete lifecycle: requirements → maintenance)
- ✓ Apply and describe benefits of collaboration to develop safe and secure software (considering various points of view, delegating tasks based on expertise, quality of solution)

**Content Overview**:

- Benefits of collaborative development
- Diverse perspectives improve security
- Shared knowledge reduces single points of failure
- Code review catches more vulnerabilities
- Delegation based on expertise
- Front-end specialist, back-end specialist, security specialist, UX designer
- Quality improvement through peer accountability
- Front-end and back-end collaboration
- API contract design (agree on endpoints before implementation)
- Documentation and communication
- Shared testing environments
- Version control workflows
- Git branching strategies (feature branches, pull requests)
- Integration testing together
- Agile security practices
- Security in sprint planning
- Definition of "done" includes security checks
- Security champions in development teams
- Regular security retrospectives
- Complete SDLC in practice
- Requirements gathering for secure applications
- Specifications with security requirements
- Secure design patterns
- Development with security in mind
- Integration testing
- Testing and debugging for security
- Deployment and installation
- Ongoing maintenance and updates

## Phase 5: Enterprise Impact & Professional Standards

**Duration**: Weeks 15-16  

### Week 15: Enterprise Benefits & Industry Impact

**Learning Objectives**:

- Analyse benefits of secure development practices to enterprises
- Evaluate impact on products, services, and work practices
- Assess productivity and business interactivity improvements
- Connect security investments to business outcomes

**Syllabus Coverage**:

*Secure Software Architecture:*

- ✓ Investigate and explain benefits to enterprise of implementation of safe and secure development practices (improved products or services, influence on future software development, improved work practices, productivity, business interactivity)

**Content Overview**:

- Enterprise benefits of secure software development
- Improved products and services
- Competitive advantage through security
- Customer trust and retention
- Reduced liability and legal costs
- Brand reputation protection
- Influence on future software development
- Security-first culture establishment
- Technical debt reduction
- Foundation for innovation
- Easier regulatory compliance
- Scalability with security built-in
- Improved work practices
- Automated testing reduces manual effort
- Version control improves workflows
- Code review improves team knowledge
- Documentation reduces onboarding time
- Clear security standards reduce ambiguity
- Productivity improvements
- Fewer security incidents = less downtime
- Automation of security checks
- Better collaboration tools
- Reduced time spent on firefighting
- Business interactivity enhancements
- API-first architecture enables partnerships
- Secure integrations with third-party services
- Data-driven decision making
- Real-world metrics
- Cost of security investment vs cost of breaches
- ROI calculation for security measures
- Financial impact analysis of major breaches
- Case studies of security success and failure

### Week 16: Social, Ethical & Legal Ramifications

**Learning Objectives**:

- Evaluate social, ethical, and legal issues in secure software development
- Analyse ramifications affecting people and enterprises
- Take informed positions on controversial issues
- Demonstrate mastery through capstone project presentations

**Syllabus Coverage**:

*Secure Software Architecture:*

- ✓ Evaluate social, ethical and legal issues and ramifications affecting people and enterprises resulting from development and implementation of safe and secure software (employment, data security, privacy, copyright, intellectual property, digital disruption)

**Content Overview**:

- Employment impact
- Job creation in cybersecurity field
- Automation and job displacement
- Need for continuous learning and upskilling
- Remote work enabled by secure systems
- Gig economy and platform security
- Data security and privacy issues
- GDPR, CCPA, and global privacy regulations
- Right to be forgotten
- Data portability rights
- Consent and transparency requirements
- Children's online privacy (COPPA)
- Biometric data concerns
- Surveillance capitalism
- Copyright and intellectual property
- Software licensing (proprietary vs open source)
- API copyright issues
- Code plagiarism and attribution
- Trade secret protection
- Patent considerations in software
- Fair use in web scraping and data collection
- Digital disruption
- Traditional industries transformed by web technology
- Democratisation of services and information
- Economic inequality and digital divide
- Environmental impact (data centers, energy consumption)
- Social media, misinformation, and platform responsibility
- Ethical dilemmas in web development
- Dark patterns in UX design
- Addictive design practices
- Surveillance and user tracking
- Algorithmic bias and discrimination
- Accessibility as ethical imperative
- Responsible vulnerability disclosure
- Cultural differences in privacy expectations