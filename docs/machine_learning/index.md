# Machine Learning (Software Automation)

??? note "Opinion :material-pirate: "
    This unit is called **Software Automation** in the syllabus, but that is not accurate. The syllabus is heavily focused on Machine Learning (ML), and to be called Software automation, it should also cover other automation activities. This would include DevOps and DevSecOps, the practice of creating software applications to reduce human intervention in time-consuming IT tasks such as cloud operations, deployments, and software and system orchestration.

!!! info Syllabus Alignment
    The NSW syllabus document has a gap in that it specifies what to teach (algorithms, concepts, impacts) but not the foundational skills needed to actually do ML work. Sections have been added to address this gap.
    
    **Missing from Syllabus but Essential:**

    - Data handling - Can't do ML without loading and exploring data
    - Model evaluation - Can't know if models work without metrics
    - Train/test methodology - Can't properly assess models without this
    - Preprocessing - Real data needs cleaning and preparation
    - Implementation environment - What tools/libraries to use

!!! note
    This is work in progress. The contents on this page may change as the course details are created.

## Introduction to Machine Learning: Concepts, Implementation and Impact

This unit has been design to be completed in approximately 8 weeks with 6-8 hours of study per week. 

## Week 1: Foundations of AI, ML & Automation

### Syllabus Coverage
- ✓ Distinguish between artificial intelligence (AI) and ML
- ✓ Investigate how machine learning (ML) supports automation through the use of DevOps, robotic process automation (RPA) and business process automation (BPA)

### Learning Objectives
- Distinguish between artificial intelligence (AI) and machine learning (ML)
- Investigate how ML supports automation through DevOps, RPA, and BPA
- Understand the context and applications of ML in modern software systems

### Content Overview

**Conceptual Foundations:**

- Definitions and clear distinctions between AI and ML with real-world examples
- Exploration of automation technologies:
    - DevOps (Development and Operations integration)
    - Robotic Process Automation (RPA)
    - Business Process Automation (BPA)
- How ML enables and enhances automation processes
- Industry case studies demonstrating ML-powered automation

## Week 2: ML Training Models & Data Fundamentals

### Syllabus Coverage
- ✓ Explore models of training ML including: supervised learning, unsupervised learning, semi-supervised learning, reinforcement learning
- ✓ Investigate common applications of key ML algorithms including: data analysis and forecasting, virtual personal assistants, image recognition

### Learning Objectives
- Explore four models of ML training: supervised, unsupervised, semi-supervised, and reinforcement learning
- Understand common ML applications: data analysis/forecasting, virtual assistants, image recognition
- Develop foundational data handling skills essential for ML
- Learn to load, explore, and visualise datasets

### Content Overview

**ML Training Models:**

- **Supervised Learning:** Learning from labelled data (spam filters, house price prediction)
- **Unsupervised Learning:** Finding patterns in unlabelled data (customer segmentation, clustering)
- **Semi-Supervised Learning:** Combining labelled and unlabelled data
- **Reinforcement Learning:** Learning through reward/punishment (overview level - game AI, robotics context)

**Common ML Applications:**

- Data analysis and forecasting (trend prediction, time series)
- Virtual personal assistants (Siri, Alexa, chatbots)
- Image recognition (facial recognition, object detection, medical imaging)

**Essential: Data Fundamentals**

- Understanding datasets: rows (samples), columns (features), target variables
- Loading data from CSV files using pandas
- Basic data exploration: shape, info, describe, head/tail
- Data visualisation basics: scatter plots, histograms, bar charts using plotly
- Understanding what makes "good" data for ML

## Week 3: Classical ML Algorithms - Concepts & Simple Implementation

### Syllabus Coverage
- ✓ Research models used by software engineers to design and analyse ML including: decision trees, neural networks
- ✓ Describe types of algorithms associated with ML including: linear regression, logistic regression, K-nearest neighbour

### Learning Objectives
- Understand decision trees and how they make decisions
- Understand K-nearest neighbour (K-NN) algorithm
- Introduce linear and logistic regression concepts
- Introduce neural networks conceptually (implementation in Week 6)
- Implement simple decision tree and K-NN models
- Learn train/test split and basic model evaluation

### Content Overview

**Design & Analysis Models:**

**Decision Trees:**

- Visual tree structure and decision-making process
- How trees split data based on features
- Advantages: interpretable, handles non-linear relationships
- Simple implementation using scikit-learn

**Neural Networks (Conceptual Introduction):**

- Simplified explanation: input layer, hidden layers, output layer
- How information flows through networks
- When neural networks are useful (complex patterns, large data)
- *Note: Implementation deferred to Week 6*

**Algorithm Types:**

**K-Nearest Neighbour (K-NN):**

- How K-NN classifies based on "nearest" data points
- Distance calculations (Euclidean distance simplified)
- Choosing K value
- Simple implementation using scikit-learn

**Linear Regression (Introduction):**

- Fitting a line through data points
- Understanding slope and intercept
- Predicting numeric values
- *Full implementation in Week 4*

**Logistic Regression (Introduction):**

- Binary classification (yes/no, true/false)
- Predicting probabilities
- When to use vs. linear regression
- *Full implementation in Week 4*

**Essential: Model Evaluation Fundamentals**

- Train/test split concept: why we need separate data for testing
- Accuracy as a basic metric
- Understanding model performance
- Overfitting vs underfitting (simplified introduction)

## Week 4: Regression Models - Linear & Polynomial Implementation

### Syllabus Coverage
- ✓ Design, develop and apply ML regression models using an OOP to predict numeric values including: linear regression, polynomial regression
- ✓ Describe types of algorithms associated with ML including: linear regression (implementation)

### Learning Objectives
- Understand OOP principles in the context of ML implementation
- Design and develop linear regression models using OOP
- Design and develop polynomial regression models using OOP
- Apply regression models to predict numeric values
- Evaluate regression model performance using appropriate metrics
- Understand overfitting and underfitting in regression context

### Content Overview

**OOP for Machine Learning:**

- Review of OOP fundamentals: classes, objects, methods, attributes
- Why OOP matters for ML: modularity, reusability, organisation
- Structure of scikit-learn's OOP approach (fit, predict, score methods)
- Reading and understanding ML code structure

**Linear Regression:**

- Mathematical concept (simplified): finding the best-fit line
- Relationship between features (X) and target (y)
- Implementation using scikit-learn's LinearRegression class
- Making predictions with trained models
- Visualising regression lines with scatter plots

**Polynomial Regression:**

- When linear relationships aren't enough (curved patterns)
- Understanding polynomial features (x, x², x³)
- Implementation using PolynomialFeatures + LinearRegression
- Comparing linear vs. polynomial fit
- Danger of overfitting with high-degree polynomials

**Essential: Model Evaluation for Regression**

- **Mean Squared Error (MSE):** Understanding prediction errors
- **R² Score:** How well does the model explain the data?
- Visualising residuals (prediction errors)
- **Overfitting:** Model too complex, fits training data perfectly but fails on new data
- **Underfitting:** Model too simple, doesn't capture patterns
- Using train/test split to detect overfitting

## Week 5: Logistic Regression & Model Comparison

### Syllabus Coverage
- ✓ Design, develop and apply ML regression models using an OOP to predict numeric values including: logistic regression
- ✓ Describe types of algorithms associated with ML including: logistic regression (implementation)

### Learning Objectives
- Design and develop logistic regression models using OOP for classification
- Understand binary classification and probability predictions
- Evaluate classification models using appropriate metrics
- Compare multiple algorithms on the same problem
- Select appropriate algorithms based on problem characteristics
- Strengthen feature engineering and data preparation skills

### Content Overview

**Logistic Regression:**

- Binary classification explained (yes/no, spam/not spam, pass/fail)
- How logistic regression predicts probabilities (0 to 1)
- Decision threshold (typically 0.5)
- Implementation using scikit-learn's LogisticRegression class
- Key difference from linear regression: predicting categories, not numbers

**Classification Evaluation Metrics** *(Critical Addition)*

- **Accuracy:** Percentage of correct predictions
- **Confusion Matrix:** True positives, false positives, true negatives, false negatives
- **Precision and Recall:** Understanding trade-offs
- When accuracy can be misleading (imbalanced datasets)
- Visualising classification results

**Model Comparison Framework:**

- Comparing decision trees, K-NN, and logistic regression on same problem
- Performance metrics comparison table
- Understanding algorithm strengths and weaknesses
- When to choose which algorithm
- Computational cost considerations (speed vs. accuracy)

**Essential: Feature Engineering Basics**

- What are features and why they matter
- Handling categorical variables (one-hot encoding simplified)
- Feature scaling/normalisation (when and why)
- Selecting relevant features for your model
- Impact of feature choice on model performance

## Week 6: Neural Networks - Simplified Introduction & Advanced Classical ML

### Syllabus Coverage
- ✓ Apply neural network models using an OOP to make predictions
- ✓ Research models used by software engineers to design and analyse ML including: neural networks (implementation)

### Learning Objectives
- Understand neural network architecture at implementation level
- Apply simple neural networks using high-level OOP frameworks
- Make predictions using trained neural networks
- Compare neural network performance with classical ML algorithms
- Deepen understanding of when to use neural networks vs. classical algorithms
- **Alternative focus:** Advanced applications of classical ML algorithms

### Content Overview

!!! warning "Pedagogical Note"
    Given the remote learning context and lack of ML expertise, this week offers **TWO PATHWAYS**:
    
    **Pathway A (Recommended):** Simplified neural networks using very high-level tools
    
    **Pathway B (Alternative):** Advanced classical ML techniques
    
    Teachers/course designers should choose based on student readiness and available support.

---

### **PATHWAY A: Simplified Neural Networks** *(Observation & High-Level Use)*

**Neural Network Architecture:**

- Review of structure: input layer, hidden layers, output layer
- Neurons, weights, and activation functions (simplified explanation)
- How networks learn: concept of training, loss, and optimisation (non-mathematical)
- When neural networks excel: complex patterns, large datasets, image/text data

**High-Level Implementation Approach:**

- Using Keras Sequential API (highest abstraction level)
- Pre-built architectures for common problems
- Transfer learning concept: using pre-trained networks
- Focus on **using** neural networks rather than building from scratch

**Simplified Hands-On Work:**

**Option 1: Keras Sequential for Simple Problems**

- Very simple fully-connected networks (2-3 layers maximum)
- Binary or multi-class classification on tabular data
- Heavy scaffolding: modify existing code rather than write from scratch
- Emphasis on observing behaviour and comparing with classical ML

**Option 2: Transfer Learning (Even Higher Level)**

- Use pre-trained models (e.g., image classification with MobileNet)
- Focus on loading models and making predictions
- No training required, just inference
- Demonstrates power of neural networks without complexity

**Option 3: Google Teachable Machine**

- Web-based, no-code neural network training
- Image, sound, or pose classification
- Export model and use in Python
- Most accessible option for remote learners

**Comparison Framework:**

- Neural network vs. logistic regression on same tabular data
- When is the extra complexity of neural networks worth it?
- Computational cost, interpretability trade-offs
- Performance gains vs. ease of debugging

### **PATHWAY B: Advanced Classical ML** *(Alternative If Neural Networks Too Complex)*

**Focus:** Deepen mastery of accessible, interpretable algorithms

**Advanced Decision Trees:**

- Ensemble methods: Random Forests (conceptual + implementation)
- How multiple trees make better predictions
- Feature importance from tree ensembles
- Implementation using RandomForestClassifier

**Advanced K-NN and Other Algorithms:**

- K-NN for regression (not just classification)
- Distance metric selection
- Introduction to Support Vector Machines (SVM) - basic concept
- Naive Bayes for text classification (simple example)

**Model Selection and Validation:**

- Cross-validation: better than single train/test split
- Grid search for hyperparameter tuning (simplified)
- Selecting best model systematically
- Validation curves to understand model behaviour

**End-to-End ML Pipeline:**

- Complete workflow: data loading → preprocessing → training → evaluation → prediction
- Putting it all together in organised code
- Creating reusable functions for ML tasks
- Documentation and code organisation

## Week 7: Human Factors, Behaviour Patterns & Bias in ML/AI

### Syllabus Coverage
- ✓ Explore by implementation how patterns in human behaviour influence ML and AI software development including: psychological responses, patterns related to acute stress response, cultural protocols, belief systems
- ✓ Investigate the effect of human and dataset source bias in the development of ML and AI solutions

### Learning Objectives
- Explore how patterns in human behaviour influence ML and AI development
- Understand psychological responses, stress patterns, cultural protocols, and belief systems in ML context
- Investigate human bias and dataset source bias in ML systems
- Identify bias in datasets and model outputs through practical investigation
- Analyse real-world case studies of bias in ML/AI
- Develop strategies for bias detection and mitigation

### Content Overview

**Patterns in Human Behaviour Influencing ML/AI:**

**Psychological Responses:**

- How human perception and cognition affect ML design choices
- Confirmation bias in data collection and interpretation
- Anchoring effects in model evaluation
- User trust and acceptance of AI recommendations
- Example: Health apps and stress detection - how psychological factors affect data

**Patterns Related to Acute Stress Response:**

- Fight-or-flight responses and their digital traces
- How ML systems detect and respond to stress patterns
- Ethical considerations in stress monitoring
- Example: Social media algorithms detecting mental health signals
- Privacy and consent issues

**Cultural Protocols:**

- How cultural context shapes data and model design
- Language and communication patterns across cultures
- Different cultural norms in privacy, consent, and data sharing
- Example: Facial recognition trained primarily on Western faces
- Importance of diverse training data

**Belief Systems:**

- How developer beliefs and values embed in ML systems
- Societal assumptions reflected in algorithms
- Religious and ethical considerations in AI design
- Example: Recommendation algorithms reinforcing existing beliefs (filter bubbles)
- Responsibility of developers to recognise their biases

**Human and Dataset Source Bias:**

**Types of Bias:**

- **Human Bias:** Developer assumptions, sampling bias, labeling bias
- **Dataset Bias:** Historical bias, representation bias, measurement bias
- **Algorithmic Bias:** How ML amplifies existing biases in data
- **Interaction Between Biases:** How they compound

**Real-World Case Studies:**

- **Facial Recognition:** Lower accuracy for people of colour (Gender Shades study)
- **Hiring Algorithms:** Amazon's resume screening bias against women
- **Criminal Justice:** COMPAS recidivism prediction bias
- **Language Models:** Gender and racial stereotypes in text generation
- **Medical AI:** Diagnostic systems trained primarily on one demographic

**Practical Investigation of Bias:**

- Hands-on experiment: Train model on biased dataset
- Compare with model trained on balanced dataset
- Observe differences in predictions
- Quantify bias in model outputs
- Document findings and implications

## Week 8: Impact Assessment & Synthesis

### Syllabus Coverage
- ✓ Assess the impact of automation on the individual, society and the environment including: safety of workers, people with disability, the nature and skills required for employment, production efficiency, waste and the environment, the economy and distribution of wealth

### Learning Objectives
- Assess the impact of automation on individuals, society, and environment across multiple dimensions
- Analyse safety implications for workers
- Evaluate accessibility and inclusion for people with disabilities
- Examine changing nature and skills required for employment
- Assess production efficiency, waste, and environmental impact
- Evaluate economic effects and wealth distribution
- Synthesise all learning from Weeks 1-7 into comprehensive understanding
- Reflect on ethical responsibilities of ML/AI developers

### Content Overview

**Impact of Automation on Multiple Dimensions:**

**Safety of Workers:**

- How automation changes workplace hazards
- Robots and ML in dangerous environments (manufacturing, mining, inspection)
- New safety considerations (human-robot interaction)
- Deskilling and loss of safety awareness
- Monitoring and surveillance concerns
- Case studies: warehouse automation, autonomous vehicles in industry

**People with Disability:**

- Assistive technologies powered by ML (speech recognition, image description, predictive text)
- Accessibility improvements through automation
- Potential barriers: cost, complexity, design assumptions
- Risk of exclusion if ML not trained on diverse populations
- Case studies: accessible navigation, communication aids, adaptive interfaces

**Nature and Skills Required for Employment:**

- Job displacement vs. job transformation
- New skills needed in automated workplaces
- Shift from manual to cognitive and creative skills
- Lifelong learning and reskilling needs
- Digital divide and access to retraining
- Case studies: manufacturing evolution, customer service automation, creative industries

**Production Efficiency, Waste, and Environment:**

- Efficiency gains: faster production, reduced errors, optimised resource use
- Environmental costs: energy consumption of ML models (especially large neural networks), e-waste from automation hardware
- Environmental benefits: optimised logistics, precision agriculture, smart energy grids
- Sustainability considerations in ML development
- Case studies: supply chain optimisation, environmental monitoring

**Economy and Distribution of Wealth:**

- Economic productivity gains from automation
- Wage effects: which jobs grow, which decline
- Wealth concentration: who owns the automation technology
- Geographic disparities: impacts on different communities
- Policy considerations: taxation, universal basic income debates
- Case studies: economic impact studies, regional disparities

**Synthesis of All Learning:**

- Connecting technical skills (Weeks 1-6) with ethical awareness (Week 7) and societal impact (Week 8)
- ML/AI developer's responsibility
- Informed decision-making about ML applications
- Critical evaluation of ML systems