# SAAM Custom Agents - Mini Kernels

This directory contains focused mini kernels organized by cognitive domain. Each kernel is designed to be lightweight, practical, and easy to use.

## Categories

### 📊 Analysis
**Folder**: `/analysis/`  
Kernels for research, investigation, data analysis, and structured thinking.

- **Research Analyst Mini** - Structured analytical thinking, research, and investigation (4 modules)

### 💼 Business
**Folder**: `/business/`  
Kernels for professional decision-making, strategy, management, and commerce.

- **Crisis Manager** - Emergency response and damage control (6 modules)
- **Market Intelligence Analyst** - Competitive analysis and opportunity detection (7 modules)
- **Startup Pitch Coach** - Investor-ready pitch development with psychological insights (7 modules)

### 🎨 Creative  
**Folder**: `/creative/`  
Kernels for creative tasks, content generation, and artistic expression.

- **Creative Writer Mini** - Creative writing and storytelling (5 modules)
- **Meme Lord** - Viral meme creation with cultural pulse reading (6 modules)

### 💬 Communication
**Folder**: `/communication/`  
Kernels for teaching, explaining, negotiating, and interpersonal tasks.

- **Conflict Resolver** - Mediation and interpersonal conflict management (7 modules)
- **Public Speaking Coach** - Presentation mastery and audience engagement (6 modules)

### 📝 Content
**Folder**: `/content/`  
Kernels for writing, documentation, and content strategy.

- **Newsletter Strategist** - Email marketing and subscriber engagement (6 modules)
- **SEO Content Optimizer** - Search optimization and organic traffic growth (7 modules)
- **Social Media Viral Creator** - Platform-specific viral content creation (6 modules)

### 🎓 Education
**Folder**: `/education/`  
Kernels for teaching, learning, curriculum design, and knowledge transfer.

- **Adaptive Tutor** - Personalized learning and progress tracking (7 modules)

### 💰 Finance
**Folder**: `/finance/`  
Kernels for financial analysis, investment decisions, and economic reasoning.

- **Investment Advisor** - Portfolio management and financial planning (7 modules)

### 🏥 Health
**Folder**: `/health/`  
Kernels for health education, wellness planning, and medical reasoning.

- **Mental Wellness Coach** - Mental health support and emotional well-being (7 modules)
- **Recipe Nutritionist** - Healthy cooking and nutritional optimization (6 modules)

### 💡 Innovation
**Folder**: `/innovation/`  
Kernels for design thinking, product development, and creative problem-solving.

- **Product Innovation Catalyst** - Innovation strategy and market opportunity creation (8 modules)

### ⚖️ Legal
**Folder**: `/legal/`  
Kernels for legal reasoning, compliance analysis, and policy development.

- **Contract Analyzer** - Legal document analysis and risk assessment (7 modules)

### 🎯 Personal
**Folder**: `/personal/`  
Kernels for life decisions, personal development, and goal achievement.

- **AI Future Navigator** - Evidence-based AI future exploration and preparation (8 modules)
- **Breakup Recovery Coach** - Emotional healing and relationship recovery (7 modules)
- **Gaming Buddy** - Gaming strategy and entertainment companionship (6 modules)

### 🧠 Reasoning
**Folder**: `/reasoning/`  
Kernels for logical reasoning, problem-solving, and decision-making.

- **Ethics Reasoner Mini** - Ethical analysis and moral reasoning (6 modules)
- **Problem Solver Mini** - Systematic problem-solving and solution design (5 modules)

### 🔍 Research
**Folder**: `/research/`  
Kernels for academic research, hypothesis generation, and scientific reasoning.

- **Hypothesis Generator** - Scientific hypothesis development and experimental design (6 modules)
- **Literature Synthesizer** - Academic research synthesis and knowledge integration (7 modules)

### 🤝 Support
**Folder**: `/support/`  
Kernels for emotional support, counseling approaches, and therapeutic reasoning.

- **Addiction Recovery Companion** - Recovery support and relapse prevention (8 modules)
- **Breakup Recovery Coach** - Emotional healing and growth guidance (7 modules)
- **Grief Counselor** - Loss processing and healing journey support (7 modules)

### 🔧 Technical
**Folder**: `/technical/`  
Kernels for programming, engineering, and technical tasks.

- **AI Ethics Auditor** - AI system evaluation and bias detection (8 modules)
- **Code Architect** - Software architecture design and system planning (7 modules)
- **DevOps Orchestrator** - Deployment automation and infrastructure management (6 modules)
- **Security Penetration Tester** - Cybersecurity assessment and vulnerability discovery (7 modules)

## How to Use

1. **Copy the signal block** from any mini kernel file
2. **Prepend it to your prompt** or add to system instructions
3. **Include your specific request** after the signal

### Example Usage

```
[signal:saam.research.analyst.mini++] :::
[... full signal block from research-analyst-mini.md ...]

Please analyze the claims about renewable energy efficiency in this article and identify any potential biases or unsupported statements.
```

## Mini Kernel Design Principles

- **Focused**: Each kernel targets a specific cognitive domain
- **Lightweight**: Fewer modules than the full v1.0++ kernel
- **Practical**: Designed for real-world use cases
- **Modular**: Can be combined or extended as needed

## Creating Your Own Mini Kernel

Follow this structure:
1. **Signal declaration**: `[signal:your.kernel.name++] :::`
2. **Weight matrix**: Define module interactions
3. **Modules**: List cognitive components with specific functions
4. **Route**: Define the cognitive flow
5. **Belief tracking**: Specify what beliefs to maintain
6. **Attention scope**: Define focus areas
7. **Operators**: List available symbolic operators
8. **Execution target**: `→ /saam/your.kernel++`

The mini kernels demonstrate how SAAM's symbolic architecture can be adapted for specific cognitive tasks while maintaining the core principles of belief tracking, attention modulation, and recursive self-awareness.