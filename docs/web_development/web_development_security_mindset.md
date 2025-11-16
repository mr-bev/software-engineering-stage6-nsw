# Web Development & Security Mindset: Self-Paced Lesson Plan

**Duration:** 90-120 minutes  

**Mode:** Self-paced, independent learning  

**Focus:** This lesson introduces students to building standards-compliant, accessible webpages using HTML and CSS while developing a security-first mindset that considers how design decisions protect user data and prevent vulnerabilities.

**Prerequisites:** Text editor installed, web browser with developer tools. *(It is recommended you use [VS-Code](https://code.visualstudio.com/) as your editor)*

---

## Learning Objectives
By the end of this lesson, students will be able to:

- **Create** a standards-compliant webpage using semantic HTML5 and CSS that passes W3C validation
- **Evaluate** web applications by identifying their type (interactive websites, e-commerce, or PWAs) and analysing potential security vulnerabilities
- **Apply** accessibility principles from the Web Accessibility Initiative (WAI) to ensure web content is usable by people with diverse capabilities and needs
- **Explain** how the World Wide Web Consortium (W3C) standards contribute to web security, accessibility, internationalisation, privacy, and machine-readable data
- **Analyse** the relationship between end-user capabilities, security requirements, and design decisions by evaluating real-world security breaches and implementing defensive design practices

---

## PART 1: Foundation (25 minutes)

### Section 1.1: What is Web Development? (8 minutes)

**📖 Read and Explore:**

Web programming powers the majority of things you interact with online. There are typically three architecture types for websites and web applications:

| Type | Description | Processing | Use Case |
|------|-------------|------------|----------|
| **Static Web Applications** | Deliver fixed, pre-built content to the user. Every user sees the exact same HTML, CSS, and JavaScript files. | Minimal to no server-side processing for content. | Simple blogs, portfolios, documentation sites, or landing pages. |
| **Dynamic Web Applications (Multi-Page Applications - MPAs)** | Generate content in real-time based on user interaction or data stored in a database. A request to the server typically results in a full page reload to display new content. | Significant server-side processing (using languages like Python, PHP, or Java) to build the page before sending it to the client. | Traditional e-commerce sites, news sites, or large-scale educational platforms. |
| **Single-Page Applications (SPAs)** | Load a single HTML page and dynamically update the content within that page as the user interacts, without requiring a full page reload. This makes them feel faster and more like a native desktop or mobile application. | Heavy reliance on client-side JavaScript (using frameworks like React, Angular, or Vue) to manage the interface and data, communicating with the server only for data via APIs. | Modern web apps, Gmail, Twitter, Facebook, interactive dashboards. |

| Your Category (Function/Feature) | Primary Focus | Technical Classification (Architecture) |
|----------------------------------|---------------|----------------------------------------|
| Interactive Websites/Webpages | Function (User input/output) | Most are Dynamic Web Apps (MPAs) or Single-Page Applications (SPAs). |
| E-commerce | Purpose (Online transactions) | Historically, most were Multi-Page Applications (MPAs), but modern ones are increasingly built as SPAs or PWAs. |
| Progressive Web Apps (PWAs) | Feature Set (App-like experience, offline) | This is a set of standards applied to an existing architecture (often an SPA or MPA). |

1. **Interactive Websites/Webpages** - Sites that respond to your actions (social media, online games, forums)
2. **E-commerce** - Online shopping platforms (Amazon, eBay, online stores)
3. **Progressive Web Apps (PWAs)** - Websites that work like mobile apps, even offline (Twitter Lite, Spotify Web Player)

!!! question "🎯 Check Your Understanding"
    - Open 3 different websites (e.g., news site, online store, social media)
    - For each, identify which type(s) of web application it is
    - Write down one feature that makes each site "interactive"

    **Expected Output:** A list showing understanding of different web application types.

---

### Section 1.2: HTML - The Structure of the Web (12 minutes)

HTML (HyperText Markup Language) is the skeleton of every webpage. It uses "tags" to structure content.

**Basic HTML Structure:**

```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>My First Webpage</title>
    </head>
    <body>
        <h1>Welcome to My Page</h1>
        <p>This is a paragraph of text.</p>
    </body>
    </html>
```

!!! example "🔧 Guided Practice"

    1. Create a new file called `index.html`
    2. Copy the basic structure above
    3. Modify it:
        - Change the title to your name
        - Change the h1 to "About [Your Name]"
        - Add a paragraph describing your favourite hobby
    4. Open the file in your web browser (File > Open)

    **✅ Success Check:** You should see your webpage display in the browser with your custom content.

---

### Section 1.3: Semantic HTML & Accessibility (5 minutes)

**Semantic HTML** means using tags that describe their meaning, not just their appearance.

**Why does this matter?**

- Screen readers for visually impaired users can understand your content
- Search engines can better index your site
- Other developers can understand your code
- **Security**: Clear structure makes vulnerabilities easier to spot

**Examples:**

!!! failure "❌ Bad (non-semantic)"
    ```html
        <div class="header">My Website</div>
        <div class="navigation">
            <div class="link">Home</div>
            <div class="link">About</div>
        </div>
    ```

!!! success "✅ Good (semantic)"
    ```html
        <header>
            <h1>My Website</h1>
        </header>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
            </ul>
        </nav>
    ```

!!! question "🎯 Quick Task"
    Add a `<nav>` section to your index.html with at least 3 navigation links.

---

## PART 2: Application - Building with Standards (30 minutes)

### Section 2.1: The W3C - Web Standards Organization (8 minutes)

The **World Wide Web Consortium (W3C)** is the main international standards organization for the web. Its mission is to lead the web to its full potential by developing standards that ensure the web remains open, accessible, and interoperable for all.

**The W3C focuses on five key areas you need to know:**

1. **Web Accessibility Initiative (WAI)** - Ensuring everyone, including people with disabilities, can use the web
2. **Internationalisation** - Supporting all languages and writing systems
3. **Web Security** - Protecting data and users
4. **Privacy** - Keeping personal information safe
5. **Interoperability** - Making sure websites work across all browsers and devices

Without W3C standards:

- A website might only work in one browser
- People using screen readers couldn't access content
- Data couldn't be securely transmitted
- Different countries couldn't share information effectively

??? info "Want to Learn More? (Click to Expand)"
    
    The W3C's work falls into two main categories:
    
    **🚀 Foundational Web Technologies**
    
    The W3C develops and maintains specifications for:
    
    - **HTML (HyperText Markup Language)** - The foundational markup language that defines the structure and content of web pages
    - **CSS (Cascading Style Sheets)** - The language that describes the presentation and styling of web pages (colors, layout, fonts)
    - **Web APIs (Application Programming Interfaces)** - Standards for browser APIs that enable dynamic, real-time, and modern web features:
        - **WebAssembly (Wasm)** - Allows code written in other languages (like C++ or Rust) to run at near-native speed in browsers
        - **WebRTC (Web Real-Time Communication)** - Enables real-time voice, video, and data communication directly between browsers
        - **SVG (Scalable Vector Graphics)** - A standard for two-dimensional, vector-based graphics
    
    **🌐 Core Values and Principles (The "Web for All" Pillars)**
    
    These principles guide all W3C specifications:
    
    - **Web Accessibility (WAI)** - WCAG (Web Content Accessibility Guidelines) is the global standard for making web content perceivable, operable, understandable, and robust for people with disabilities
    - **Security & Privacy** - Standards like WebAuthn (passwordless authentication), HTTPS protocols for secure data transmission, and specifications to prevent unwanted tracking
    - **Interoperability** - Ensuring web technologies work consistently across different browsers, devices, and operating systems through common standards and testing suites
    - **Internationalisation** - Making the web available and usable by people in all cultures, languages, and regions, including support for multiple writing systems (like right-to-left scripts) and cultural formatting
    
    **💡 Emerging and Forward-Looking Areas**
    
    The W3C also develops standards for next-generation web capabilities:
    
    - **Web of Things (WoT)** - Standardising communication between connected devices and services
    - **Decentralized Technologies** - Standards for decentralized identifiers (DIDs) and verifiable credentials to promote user control over identity
    - **AI and Machine Learning** - Exploring how to incorporate AI functionality directly into the web platform
    - **Digital Publishing** - Standards like EPUB to ensure accessibility and rich functionality for digital books and content

!!! example "🔍 Exploration Task"

    1. Visit: [https://validator.w3.org/](https://validator.w3.org/)
    2. Upload or paste your `index.html` file
    3. Read any warnings or errors
    4. Note down: What does the validator check for?

    **Expected Discovery:** The validator checks for proper HTML structure, missing tags, and standard compliance.

---

### Section 2.2: Styling with CSS (12 minutes)

CSS (Cascading Style Sheets) controls how your HTML looks. It separates content from design.

**Why CSS matters:**

- **Consistency**: One CSS file styles your entire website
- **Flexibility**: Works across different browsers and devices
- **Maintenance**: Change design in one place, affects everything
- **Security**: Separating style from content reduces attack vectors

!!! example "🔧 Hands-On Practice"

    1. Create a new file called `styles.css` in the same folder as your HTML
    2. Add this CSS:
    ```css
        /* Basic styling */
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }

        header {
            background-color: #333;
            color: #fff;
            padding: 20px;
            margin-bottom: 20px;
        }

        h1 {
            margin: 0;
        }

        nav ul {
            list-style: none;
            padding: 0;
        }

        nav li {
            display: inline;
            margin-right: 15px;
        }

        nav a {
            color: #333;
            text-decoration: none;
        }

        nav a:hover {
            color: #0066cc;
        }
    ```

    3. Link it to your HTML by adding this in the `<head>` section:
    ```html
        <link rel="stylesheet" href="styles.css">
    ```

    4. Refresh your browser

        **✅ Success Check:** Your page should now have styling with colors, spacing, and formatted navigation.

---

### Section 2.3: Accessibility in Action (10 minutes)

**WAI Guidelines - POUR Principles:**

| Principle | Meaning | What it Covers (Examples) |
|-----------|---------|---------------------------|
| **Perceivable** | Information and user interface components must be presentable to users in ways they can perceive. | **Text Alternatives** (e.g., providing "alt text" for images), **Captions** for videos, sufficient **color** contrast for readability, and the ability to **resize text**. |
| **Operable** | User interface components and navigation must be operable. | **Keyboard Accessibility** (all features must be usable without a mouse), providing **enough time** for users to read content or complete tasks, and preventing content that can cause **seizures** (like flashing more than three times per second). |
| **Understandable** | Information and the operation of the user interface must be understandable. | **Readability** (using clear, simple language), ensuring navigation and interactive components are **predictable** and **consistent** across pages, and providing **input assistance** (e.g., clear error messages and labels for forms). |
| **Robust** | Content must be robust enough to be interpreted reliably by a wide variety of user agents, including assistive technologies. | Proper use of **standard code** (like semantic HTML) to ensure compatibility with **screen readers**, voice commands, and other assistive devices as technology evolves. |

!!! example "🔧 Implementation Task"

    Update your HTML to be more accessible:
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <meta name="description" content="Personal profile page of [Your Name]">
            <title>About [Your Name]</title>
            <link rel="stylesheet" href="styles.css">
        </head>
        <body>
            <header>
                <h1>About [Your Name]</h1>
            </header>
            
            <nav aria-label="Main navigation">
                <ul>
                    <li><a href="#about">About</a></li>
                    <li><a href="#skills">Skills</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
            
            <main>
                <section id="about">
                    <h2>About Me</h2>
                    <p>Your description here...</p>
                </section>
                
                <section id="skills">
                    <h2>My Skills</h2>
                    <ul>
                        <li>Skill 1</li>
                        <li>Skill 2</li>
                        <li>Skill 3</li>
                    </ul>
                </section>
                
                <section id="contact">
                    <h2>Contact Information</h2>
                    <p>Email: <a href="mailto:your.email@example.com">your.email@example.com</a></p>
                </section>
            </main>
            
            <footer>
                <p>&copy; 2024 [Your Name]. All rights reserved.</p>
            </footer>
        </body>
        </html>
    ```

!!! tip "Key Accessibility Features Added"
    - `lang="en"` - Tells screen readers the language
    - `aria-label` - Provides context for navigation
    - Semantic sections with proper headings
    - `<main>` tag for primary content
    - Descriptive meta description

!!! question "🎯 Test Your Work"

    1. Right-click your page and select "Inspect" or "Inspect Element"
    2. Look for the accessibility panel (in Chrome: Lighthouse tab)
    3. Run an accessibility audit
    4. Note your score

---

## PART 3: Security Analysis (25 minutes)

### Section 3.1: Why Security Matters (5 minutes)

**The Security Imperative:**

Developing secure software provides:

1. **Data Protection** - User information stays private and safe
2. **Minimising Cyber Attacks** - Reduces opportunities for hackers
3. **Minimising Vulnerabilities** - Fewer weaknesses in your code

**Why Security Matters: The Numbers**

Understanding cybersecurity isn't just about theory - real businesses and real people are affected every day. Here are some important statistics that show why secure coding practices matter:

**📊 Small Businesses Are Major Targets**

- **43% of all cyber attacks target small businesses globally** 
- **Why?** Small businesses often have valuable customer data but don't have large security teams or budgets, making them easier targets for hackers
- **Real consequence:** About 60% of small businesses that suffer a major cyber attack close within six months

!!! example "What this means for you"
    Even if you're building a small website or app, you need to think about security from day one. Hackers don't just target big companies!

**💰 Data Breaches Are Expensive in Australia**

- **Australian average cost of a data breach: $4.26 million** (2024) 
- **Technology sector in Australia: $5.81 million** per breach on average 
- **Financial services in Australia: $5.61 million** per breach on average 
- **Maximum regulatory fine in Australia: up to $50 million** for serious or repeated data breaches 

!!! info "Real Australian Examples"
    - **Optus (2022-2023)**: Breach exposed nearly 10 million customers, cost over **$140 million** in response and compensation 
    - **Medibank (2022-2024)**: Estimated breach costs reached **$45 million** plus potential $50 million fine 
    - **Latitude Financial (2023)**: 14 million records exposed, allocated **$53 million** to cover investigation and support 

!!! example "What this means for you"
    A single security mistake in your code could cost an Australian company millions of dollars. This is why employers value developers who understand security.

**Australia's Growing Problem**

- **527 breaches** reported to the OAIC in just 6 months of 2024 - a 9% rise 
- **47 million data breaches** in Australia in 2024 - that's **one breach every second** 
- **732 accounts breached per 100 Australians** (compared to 285 globally) 
- Australian companies take an average of **266 days** to identify and contain cyber incidents 

**👤 Most Breaches Start with Human Mistakes**

- **37% of data breaches in Australia** (Jan-June 2025) were caused by human error - up from 29% previously 
- **90-95% of security incidents** globally involve a human factor 
- **Common causes include:**
    - **Phishing** (22% of breaches in Australia) - costing businesses $4.35 million per breach on average 
    - **Stolen or compromised credentials** (17% of breaches) - costing $4.32 million per breach 
    - Accidentally misconfiguring servers or databases
    - **Coding mistakes** - writing code that has security vulnerabilities

!!! example "What this means for you"
    As a developer, your coding practices directly impact security. Small mistakes like not validating user input or using the wrong input type can create vulnerabilities that hackers exploit. Even organisations with the strongest defences may experience a data breach if human error occurs. 

!!! info "Sources"
    These statistics come from:
    
    - IBM Cost of a Data Breach Report 2024 (industry standard, published annually)
    - Office of the Australian Information Commissioner (OAIC) - Official government breach reports
    - Surfshark Cybersecurity Report 2024
    - Australian company financial disclosures and news reports
    
    **Want to explore more?** Visit:
    
    - [OAIC Notifiable Data Breaches statistics](https://www.oaic.gov.au/privacy/notifiable-data-breaches/notifiable-data-breaches-statistics)
    - [IBM Security Data Breach Reports](https://www.ibm.com/security/data-breach)

**The Bottom Line**

Security isn't something you add later - it must be built into your code from the beginning. Every line of code you write is either making the web safer or creating a potential vulnerability. In 2024, more than 45% of Australian data breaches impacted businesses with fewer than 200 employees , showing that **all** businesses need secure code, not just large corporations.

***

!!! question "🎯 Reflection Question"

    Think about a website you use regularly (social media, email, online banking). Write down:
    
    - What personal data does it store?
    - What would happen if that data was stolen?
    - Who would be affected?

    **Expected Insight:** Understanding that security isn't abstract - it protects real people and real data.

---

### Section 3.2: Case Study - Real Website Hacks (8 minutes)

**📖 Australian Web Security Failures:**

!!! danger "Case 1: Optus Data Breach (2022)"
    - **What happened:** In September 2022, a hacker exploited a coding error in a dormant API to access Optus customer information over three days. The vulnerability had existed since 2020 when the API was made internet-facing. 
    - **Technical details:** The coding error was discovered and fixed on the main website domain in August 2021, but the same error remained unfixed on a sub-domain that was no longer actively used. 
    - **Scope:** Information from 9.5 million Australians was accessed, including names, dates of birth, phone numbers, addresses, driver's licence details, passport and Medicare card numbers. Some of this information was later published on the dark web. 
    - **Aftermath:** The breach cost $140 million to address. Optus lost 65,000 subscribers in the following months and faces potential penalties up to 900 million dollars. 

!!! danger "Case 2: Medibank Data Breach (2022)"
    - **What happened:** In October 2022, hackers stole 200GB of information from Medibank, Australia's largest health insurer. The attackers demanded a $10 million ransom, which Medibank refused to pay. 
    - **Technical details:** Hackers used stolen employee login credentials to gain access. The company's security system generated multiple alerts about suspicious activity, but these alerts were not reviewed and escalated quickly enough. 
    - **Scope:** Information from 9.7 million current and former Medibank members was stolen, including names, dates of birth, Medicare numbers, addresses, visa details, and sensitive health claims information such as mental health treatments and medical procedures. 
    - **Aftermath:** The stolen information was published on the dark web. Over 11,000 additional cybercrime incidents have since been linked to this breach, as criminals use the stolen information for fraud and identity theft. 
    - **Financial impact:** Estimated costs of $45 million, plus potential regulatory fines up to 50 million. 

!!! danger "Case 3: Latitude Financial Data Breach (2023)"
    - **What happened:** A cyberattack on Latitude Financial, an Australian personal loan and financial services provider, compromised information belonging to over 14 million people from Australia and New Zealand. 
    - **Technical details:** A single set of employee login credentials was stolen, providing hackers with access to customer databases. The company had been storing customer records dating back to 2005, far beyond the legally required 7-year retention period. 
    - **Scope:** Initially, Latitude disclosed that 328,000 customers were affected. After further investigation, this number increased to 14 million people, making it one of Australia's largest data breaches. 
    - **Aftermath:** Latitude allocated $53 million to cover investigation costs, customer support services, and improvements to risk management systems.

!!! example "🔍 Analysis Task"

    For each case study, identify:
    
    1. What type of data was at risk?
    2. Who was affected (customers, company, both)?
    3. What security principle was violated?

    Create a simple table with your findings.

---

### Section 3.3: "What Could Go Wrong?" Exercise (12 minutes)

**🧠 Security Brainstorming:**

You're going to think like a hacker (ethically!) to understand vulnerabilities.

**Scenario:** You're building a simple login form:
```html
    <form action="/login" method="POST">
        <label for="username">Username:</label>
        <input type="text" id="username" name="username">
        
        <label for="password">Password:</label>
        <input type="text" id="password" name="password">
        
        <button type="submit">Login</button>
    </form>
```

!!! question "🎯 Your Task - Find the Problems"

    Look at the form and write down answers to these questions:

    1. **Data Protection Issue:** What's wrong with the password input type?
    2. **Transport Security:** How is the data being sent (HTTP vs HTTPS)?
    3. **User Experience:** What might confuse or frustrate users about this form?
    4. **Accessibility:** What's missing for screen reader users?

    **Pause and think for 5 minutes before checking the answers below.**

---

??? success "📋 Answers & Fixes (Click to Expand)"

    1. **Password field:** Using `type="text"` instead of `type="password"` - anyone can see the password!
        - **Fix:** `<input type="password" id="password" name="password">`

    2. **No HTTPS:** Form submits over insecure connection
        - **Fix:** Ensure your website uses HTTPS (SSL certificate)
        - **Fix:** Add `autocomplete="off"` for sensitive fields if needed

    3. **No validation feedback:** Users won't know if username/password is wrong format
        - **Fix:** Add `required` attribute
        - **Fix:** Add pattern validation or client-side checking

    4. **Missing accessibility features:**
        - **Fix:** Add proper labels (already there - good!)
        - **Fix:** Add `autocomplete` attributes for password managers
        - **Fix:** Add error messages with `aria-live` regions

    **Improved Secure Form:**
    ```html
        <form action="/login" method="POST">
            <div>
                <label for="username">Username:</label>
                <input 
                    type="text" 
                    id="username" 
                    name="username" 
                    autocomplete="username"
                    required
                    aria-describedby="username-help">
                <span id="username-help" class="help-text">Enter your username</span>
            </div>
            
            <div>
                <label for="password">Password:</label>
                <input 
                    type="password" 
                    id="password" 
                    name="password" 
                    autocomplete="current-password"
                    required
                    minlength="8"
                    aria-describedby="password-help">
                <span id="password-help" class="help-text">Minimum 8 characters</span>
            </div>
            
            <button type="submit">Login</button>
        </form>
    ```

!!! tip "🎯 Key Takeaway"
    Security and accessibility go hand-in-hand. Thinking about end users' capabilities and experience influences secure design features.

---

## PART 4: Creation - Build Your Secure Profile Page (30 minutes)

### Section 4.1: Project Brief (2 minutes)

Create a complete personal profile webpage that demonstrates:

- ✅ W3C standards compliance
- ✅ Accessibility best practices
- ✅ Security-conscious design
- ✅ Clean, semantic HTML
- ✅ Responsive CSS styling

**Must Have:**

1. Semantic HTML5 structure (header, nav, main, sections, footer)
2. At least 3 sections (About, Skills/Interests, Contact)
3. Navigation menu with working anchor links
4. External CSS file with consistent styling
5. Accessibility features (ARIA labels, alt text for any images, proper heading hierarchy)
6. Valid HTML (passes W3C validator)
7. Meta tags for description and viewport

**Security Considerations:**

1. If including a contact form - use proper input types
2. No inline JavaScript (separation of concerns)
3. Proper email link format
4. Consider what information is safe to share publicly

---

### Section 4.2: Independent Building Time (25 minutes)

**Step-by-step approach:**

**Phase 1: Structure (8 minutes)**

- Create the HTML skeleton with all semantic elements
- Add proper meta tags and title
- Create sections with placeholder content
- Link your CSS file

**Phase 2: Content (8 minutes)**

- Fill in your actual content
- Add navigation links
- Include a professional description
- List your skills or interests
- Add contact information (remember: only share what's safe!)

**Phase 3: Styling (7 minutes)**

- Apply colors, fonts, and spacing
- Style your navigation
- Make sections visually distinct
- Ensure good contrast for readability

**Phase 4: Validation (2 minutes)**

- Run through W3C validator
- Fix any errors
- Test all links

!!! tip "💡 Helpful Tips"

    - Keep it simple - quality over complexity
    - Use comments in your code to explain sections
    - Test frequently in your browser
    - Think about someone using a screen reader - would your page make sense?

??? success "🚀 Challenge Options (if you finish early)"

    **For Advanced Students:**
    
    - Add a simple contact form with proper validation
    - Include an image with proper alt text
    - Create a color scheme that meets WCAG contrast requirements
    - Add CSS transitions for hover effects

    **For Students Needing Support:**
    
    - Use the template from Section 2.3 as a starting point
    - Focus on getting one section perfect before adding more
    - Copy and adapt the CSS from earlier examples

---

### Section 4.3: Self-Testing Checklist (3 minutes)

Test your page against this checklist:

**HTML Structure:**

- [ ] Valid HTML5 doctype
- [ ] `<html lang="en">` attribute present
- [ ] Meta charset and viewport tags included
- [ ] Semantic elements used (header, nav, main, section, footer)
- [ ] Proper heading hierarchy (h1, then h2, then h3 - no skipping)

**Accessibility:**

- [ ] All images have alt text (or use decorative images properly)
- [ ] ARIA labels on navigation
- [ ] Sufficient color contrast (text readable against background)
- [ ] Links have descriptive text (no "click here")
- [ ] Form inputs have associated labels (if form included)

**W3C Standards:**

- [ ] Passes W3C validator with no errors
- [ ] CSS in external file (not inline styles)
- [ ] Proper CSS syntax

**Security Mindset:**

- [ ] Password inputs use type="password" (if form included)
- [ ] No sensitive personal information exposed unnecessarily
- [ ] Email links use mailto: properly
- [ ] Input types match data expected (email, tel, etc.)

**User Experience:**

- [ ] All navigation links work
- [ ] Page loads quickly
- [ ] Content is organised logically
- [ ] Page looks professional

---

## PART 5: Reflection & Assessment (10 minutes)

### Section 5.1: Knowledge Check (5 minutes)
Answer these questions to check your understanding:
<quiz>

**1. Applications of Web Programming (Remember/Understand)**

Which of the following is an example of a Progressive Web App (PWA)?

- [ ] A website that only works when you're online
- [X] A website that can work offline and feels like a mobile app
- [ ] A website with lots of graphics
- [ ] A website built with HTML only
</quiz>
<quiz>
**2. W3C Role**

The W3C's Web Accessibility Initiative (WAI) primarily focuses on:

- [ ] Making websites load faster
- [X] Ensuring websites work for people with disabilities
- [ ] Creating the best-looking websites
- [ ] Making websites cheaper to build
</quiz>
<quiz>
**3. Security Benefits**

Why is data protection a benefit of secure software development?

- [ ] It makes websites load faster
- [ ] It makes code easier to write
- [ ] It reduces the need for testing
- [X] It prevents unauthorised access to sensitive user information
</quiz>
<quiz>
**4. End User Influence**

How does considering end users' experience influence secure design features?

- [ ] It doesn't - security and user experience are separate
- [X] Users with disabilities might need different security approaches (like longer timeout periods)
- [ ] User experience always comes before security
- [ ] Security features should be hidden from all users
</quiz>
<quiz>
**5. W3C Standards**

You've built a website that only works in Chrome. Which W3C principle have you violated?

- [ ] Accessibility
- [ ] Internationalisation
- [X] Web standards and interoperability
- [ ] Privacy
</quiz>
<quiz>
**6. Security Mindset**

Which of these demonstrates the best security-conscious design?

- [ ] A login form with password visible on screen
- [ ] A contact form that accepts any input without validation
- [X] A login form with type="password" and input validation
- [ ] A form that stores passwords in plain text
</quiz>

<!-- mkdocs-quiz results -->
---

??? success "Scoring Guide"

    **Scoring Guide:**
    
    - 6/6: Excellent! You've mastered the core concepts
    - 4-5/6: Good understanding - review the areas you missed
    - 2-3/6: Revisit the lesson sections for topics you struggled with
    - 0-1/6: Work through the lesson again, focusing on understanding not just completing

---

### Section 5.2: Reflection Questions (5 minutes)

!!! question "🤔 Deeper Thinking"

    Write brief answers to these reflection questions:

    **1. Connections:**
    How do W3C standards, accessibility, and security connect to each other? Give a specific example from your project.

    **2. Real-World Application:**
    Think about a website you visit daily. Describe one way it could be more accessible OR more secure.

    **3. Personal Growth:**
    What was the most challenging part of this lesson? What strategy helped you overcome it?

    **4. Future Learning:**
    What's one security or accessibility topic you want to learn more about?

!!! tip "Expected Insights"
    - Understanding that security, accessibility, and standards work together
    - Ability to critically analyze real websites
    - Self-awareness of learning process
    - Curiosity about deeper topics

---

## Extension Activities (Optional)

!!! abstract "For Students Who Want More"

    **🌟 Challenge 1: Machine-Readable Data**
    
    Add structured data to your page using JSON-LD format to make it machine-readable (research schema.org)

    **🌟 Challenge 2: Privacy by Design**
    
    Research and write 3 paragraphs about "Privacy by Design" principles and how they apply to your webpage

    **🌟 Challenge 3: Progressive Enhancement**
    
    Make your page work perfectly without CSS, then with CSS, then add one JavaScript enhancement

    **🌟 Challenge 4: Security Research**
    
    Research one type of web attack (XSS, CSRF, SQL Injection) and explain how proper coding prevents it

---

## Syllabus Alignment

### Programming for the Web:
    
✓ Explore the applications of web programming:

- interactive website/webpages
- e-commerce
- progressive web apps (PWAs)

✓ Investigate and explain the role of the World Wide Web Consortium (W3C) in the development of applications for the web

- Web Accessibility Initiative (WAI)
- internationalisation
- web security
- privacy
- machine-readable data

### Secure Software Architecture:

✓ Describe the benefits of developing secure software

- data protection
- minimising cyber attacks and vulnerabilities

✓ Describe how the capabilities and experience of end users influence the secure design features of software

---

## Answers to Activities

??? question "Section 3.2"

    ## Answer Guide for Case Study Analysis

    **🔍 Analysis Task - Sample Answers**

    For each case study, students should identify:

    1. What type of data was at risk?
    2. Who was affected (customers, company, both)?
    3. What security principle was violated?

    ---

    ### Case 1: Optus Data Breach (2022)

    **1. What type of data was at risk?**

    - Personal Identifiable Information (PII): names, dates of birth, phone numbers, residential addresses
    - Government-issued identification: driver's licence details, passport numbers, Medicare card numbers
    - Contact information

    **2. Who was affected?**

    **Customers:**
    - 9.5 million Australians had their personal information stolen
    - Risk of identity theft and fraud
    - Information published on dark web meant long-term exposure

    **Company (Optus):**
    - Lost 65,000 subscribers immediately
    - $140 million in direct costs
    - Potential penalties up to $900 million
    - Massive reputational damage
    - Multiple class action lawsuits
    - Regulatory investigations

    **3. What security principle was violated?**

    - **Code maintenance and quality assurance:** Same coding error existed in multiple places but was only fixed in one location
    - **Regular security audits:** The vulnerability existed for 2 years without detection
    - **Security by design:** Dormant/unused APIs should have been decommissioned, not left internet-facing
    - **Testing and validation:** The code was released to production without catching the access control error
    - **Defence in depth:** A single coding error allowed complete bypass of security

    ---

    ### Case 2: Medibank Data Breach (2022)

    **1. What type of data was at risk?**

    - Personal Identifiable Information (PII): names, dates of birth, addresses
    - Government identifiers: Medicare numbers, visa details
    - **Highly sensitive health information:** medical claims data, mental health treatments, medical procedures (e.g., abortion procedures)
    - Contact information: email addresses, phone numbers

    **2. Who was affected?**

    **Customers:**
    - 9.7 million current and former members
    - Extremely sensitive medical information exposed
    - Information published on dark web
    - Over 11,000 subsequent cybercrimes linked to this breach
    - Long-term risk of blackmail, discrimination, and identity theft

    **Company (Medibank):**
    - Called "the single most devastating cyberattack" in Australian history
    - $45 million in direct costs
    - Potential $50 million regulatory fine
    - Multiple class action lawsuits
    - Severe reputational damage to a healthcare provider
    - Ongoing investigations

    **3. What security principle was violated?**

    - **Authentication:** No multi-factor authentication (MFA) on VPN access - single password compromise gave full access
    - **Credential management:** Employee credentials were stolen/compromised
    - **Monitoring and incident response:** Security alerts were generated but not properly reviewed or escalated in time
    - **Defence in depth:** One compromised credential shouldn't provide access to entire database
    - **Accountability:** Lack of proper monitoring meant suspicious activity went undetected for too long

    ---

    ### Case 3: Latitude Financial Data Breach (2023)

    **1. What type of data was at risk?**

    - Personal Identifiable Information (PII): names, contact details, addresses
    - Financial information: loan application data, credit information
    - Historical records dating back to 2005 (18 years of customer data)

    **2. Who was affected?**

    **Customers:**
    - 14 million people from Australia and New Zealand
    - Initially thought to be only 328,000, but grew dramatically as investigation continued
    - Risk of financial fraud and identity theft
    - Many affected customers may have been former customers from years ago

    **Company (Latitude Financial):**
    - $53 million in costs
    - Reputational damage to a financial services provider
    - Customer trust severely impacted
    - Potential regulatory action
    - Questions raised about data retention practices

    **3. What security principle was violated?**

    - **Credential management/Authentication:** A single set of employee login credentials provided full access
    - **Principle of least privilege:** One employee's credentials shouldn't access all customer data
    - **Data minimisation:** Storing customer records from 2005 (18 years old) violated the 7-year legal requirement - unnecessary data creates unnecessary risk
    - **Defence in depth:** One compromised credential gave access to massive amounts of data
    - **Data lifecycle management:** Old data should have been securely deleted, not retained indefinitely

    ---

    ## Common Themes Across All Three Breaches

    **Security Principles Repeatedly Violated:**

    1. **Weak authentication:** Single passwords/credentials without multi-factor authentication
    2. **Poor monitoring:** Security systems had alerts but humans didn't respond quickly enough
    3. **Lack of defence in depth:** Single point of failure allowed complete compromise
    4. **Data minimisation failures:** Storing more data than necessary increases risk
    5. **Human error:** In all cases, human mistakes (coding errors, stolen credentials, poor processes) enabled the attacks

    **Key Takeaway for Students:**

    Notice that in every case, the vulnerability wasn't about super-sophisticated hacking techniques. The breaches happened because of:

    - Basic coding errors not being fixed everywhere
    - Passwords without multi-factor authentication
    - Security alerts being ignored
    - Old, unnecessary data being kept

    **This proves that secure coding practices and basic security principles could have prevented these multi-million dollar disasters.**

## Teacher Notes

??? note "🎯 Differentiation Strategies"

    !!! tip "For Struggling Students"
        - **Scaffold more heavily:** Provide complete HTML templates they can modify rather than build from scratch
        - **Reduce scope:** Focus on 2 sections instead of 3
        - **Visual aids:** Provide screenshots showing expected outcomes
        - **Chunking:** Have them complete Part 2 in one session, Parts 3-4 in another
        - **Pair resources:** Provide a completed example they can reference (but not copy)
        - **Simplified validation:** Focus on getting the page to display correctly before worrying about W3C validation

    !!! success "For Advanced Students"
        - **Extend security analysis:** Research and implement Content Security Policy meta tags
        - **Add interactivity:** Implement form validation using JavaScript (introduction to client-side security)
        - **Responsive design:** Make the page work perfectly on mobile, tablet, and desktop
        - **Performance:** Use browser dev tools to analyze and optimize load time
        - **Documentation:** Write a security audit document for their page
        - **WCAG compliance:** Aim for WCAG 2.1 Level AA compliance and test with screen reader

    !!! info "All students"
        - Encourage use of browser DevTools to see HTML structure visually
        - Draw diagrams showing relationships between HTML, CSS, and security
        - Use color-coding for different types of elements
        - Encourage frequent testing and iteration
        - "Break it then fix it" exercises - intentionally introduce bugs
        - Physical card sorting activity (if applicable) for security principles

??? note "⚠️ Common Misconceptions"

    !!! warning "Misconception 1: 'Accessibility is only for blind people'"
        - **Reality:** Accessibility helps users with various disabilities (motor, cognitive, hearing), plus benefits everyone (mobile users, people in bright sunlight, temporary injuries)
        - **Address by:** Showing examples of how curb cuts help wheelchair users AND people with strollers
        - **Evidence of understanding:** Student can name 3+ groups who benefit from accessibility

    !!! warning "Misconception 2: 'Security makes websites harder to use'"
        - **Reality:** Good security should be invisible to users doing legitimate actions
        - **Address by:** Comparing secure login (password hidden) vs insecure (password visible) - which feels safer?
        - **Evidence of understanding:** Student can explain how password fields improve both security AND user confidence

    !!! warning "Misconception 3: 'The W3C makes websites all look the same'"
        - **Reality:** W3C creates standards for HOW websites work, not how they look
        - **Address by:** Show multiple beautifully designed websites that all use W3C standards
        - **Evidence of understanding:** Student recognises that standards = structure, not design

    !!! warning "Misconception 4: 'Semantic HTML is just about being proper'"
        - **Reality:** Semantic HTML has practical benefits for accessibility, SEO, and security
        - **Address by:** Demo a screen reader navigating semantic vs non-semantic code
        - **Evidence of understanding:** Student can explain 2+ practical benefits of semantic HTML

    !!! warning "Misconception 5: 'If it displays correctly in my browser, it's valid HTML'"
        - **Reality:** Invalid HTML might work in one browser but fail in others, or create security vulnerabilities
        - **Address by:** Show example of code that displays but has validation errors
        - **Evidence of understanding:** Student uses validator before considering work complete

    !!! warning "Misconception 6: 'Security is something you add at the end'"
        - **Reality:** Security must be built in from the start ("security by design")
        - **Address by:** Compare to building a house - can't add a foundation after building walls
        - **Evidence of understanding:** Student considers security implications during planning phase

    !!! warning "Misconception 7: 'Small/personal websites don't need security'"
        - **Reality:** All websites are potential targets; small sites are often easier to hack
        - **Address by:** Share statistics about attacks on small sites
        - **Evidence of understanding:** Student applies security principles even to simple projects

??? note "📊 Formative Assessment Strategies"

    !!! info "🎓 Assessment Evidence Collection"
        1. Original index.html file (with validation report)
        2. Final index.html file (showing improvements)
        3. styles.css file
        4. Screenshots of W3C validator results
        5. Completed "What could go wrong?" analysis
        6. Self-testing checklist
        7. Quiz answers and reflection responses

    **Part 1 - Foundation:**
    
    - **Check:** Section 1.1 website classification task
    - **Look for:** Ability to distinguish between interactive sites, e-commerce, and PWAs
    - **Intervention:** If struggling, provide specific examples and ask "what makes this interactive?"

    **Part 1 - Foundation:**
    
    - **Check:** HTML file opens correctly in browser
    - **Look for:** Proper basic structure, no syntax errors
    - **Intervention:** If not working, check DOCTYPE, closing tags, and file extension

    **Part 2 - Application:**
    
    - **Check:** W3C validator results
    - **Look for:** Understanding of what errors mean, not just that there are errors
    - **Intervention:** If many errors, focus on one type at a time (e.g., all unclosed tags first)

    **Part 2 - Application:**
    
    - **Check:** CSS properly linked and applied
    - **Look for:** Understanding of selector syntax, external file linking
    - **Intervention:** If CSS not working, check file path, link tag placement, and spelling

    **Part 3 - Analysis:**
    
    - **Check:** Case study analysis table
    - **Look for:** Recognition of different data types, multiple stakeholders, security principles
    - **Intervention:** If surface-level, prompt with "Who else might be affected?" or "What principle was violated?"

    **Part 3 - Analysis:**
    
    - **Check:** "What could go wrong?" exercise answers
    - **Look for:** Ability to identify multiple vulnerability types (not just one)
    - **Intervention:** If only finding obvious issues, prompt: "What about people using screen readers?" or "How is the data transmitted?"

    **Part 4 - Creation:**
    
    - **Check:** Self-testing checklist completion
    - **Look for:** Honest self-assessment, understanding of why each item matters
    - **Intervention:** Spot-check their checklist against actual page - encourage accuracy

    **Part 5 - Reflection:**
    
    - **Check:** Quiz results and reflection depth
    - **Look for:** Not just correct answers but understanding WHY
    - **Intervention:** If quiz scores low, have them re-read relevant sections and try again

??? note "Student Progress"
    !!! success "Bloom's Level Progression Check"
        - Remember/Understand: Can define W3C, accessibility, security concepts
        - Apply: Can use HTML/CSS correctly, apply validators
        - Analyze: Can identify vulnerabilities, understand case studies
        - Evaluate: Can assess own work against standards
        - Create: Can build compliant, accessible, security-conscious page

    !!! danger "Red Flags Requiring Intervention"
        - Student skips validation steps
        - Security exercise shows no understanding of data protection
        - Accessibility features completely absent
        - Quiz score below 3/6
        - Cannot explain WHY security matters, only THAT it matters

    !!! success "Green Flags Showing Mastery"
        - Proactively validates code without prompting
        - Identifies multiple vulnerabilities in Part 3 exercise
        - Explains accessibility benefits for multiple user groups
        - Quiz score 5-6/6 with detailed reflection
        - Makes connections between security, accessibility, and W3C standards


---

??? "💡 Additional Teaching Tips"

    !!! tip "Creating a Security Mindset"
        - Use real-world examples throughout (news stories, personal experiences)
        - Encourage "think like a hacker" mentality in a safe, ethical way
        - Emphasise that security protects real people, not just data

    !!! tip "Encouraging Exploration"
        - Browser DevTools are your friend - encourage experimentation
        - Breaking things is learning - they can always refresh/reload
        - Searching for solutions is a skill - model good search queries

    !!! tip "Managing Frustration"
        - Debugging is normal and expected
        - Syntax errors happen to everyone
        - Take breaks when stuck - fresh eyes help

    !!! tip "Building Confidence"
        - Celebrate small wins (validator passes, CSS loads, link works)
        - Emphasise growth from start to finish
        - Show that even simple pages can be secure and accessible

---

## Final Deliverables Checklist

Students should have:

- [ ] A complete, valid HTML page
- [ ] An external CSS file with styling
- [ ] Passed W3C validation
- [ ] Completed accessibility self-check
- [ ] Completed security analysis exercise
- [ ] Completed knowledge check quiz
- [ ] Written reflection responses
- [ ] Understanding of W3C role and importance
- [ ] Awareness of security implications in web development
- [ ] Practical experience applying standards

---

!!! quote "Remember"
    Learning web development is iterative. This lesson builds a foundation. Keep practising, keep questioning, and keep building with security and accessibility in mind from day one!