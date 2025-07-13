# AI for New Development Research

This document outlines a comparison of various AI-powered development tools to inform our decision-making process.

## Comparison Table

| Tool                       | Individual Plan (per user/month)                                                        | Organization Plan (2-5 members, per user/month)                                           | Key Features                                                                                                    |
| -------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Cursor AI**              | [$20 (Pro)](https://cursor.sh/pricing)                                                  | [$40 (Teams)](https://cursor.sh/pricing)                                                  | AI-powered code editor, unlimited agent requests, background agents, [bug bot](https://docs.cursor.com/bugbot). |
| **Windsurf AI**            | [$15 (Pro)](https://windsurf.ai/pricing)                                                | [$30 (Teams)](https://windsurf.ai/pricing)                                                | AI-powered IDE, 500 prompt credits/month (Pro), centralized billing (Teams).                                    |
| **GitHub Copilot**         | [$10 (Individual)](https://github.com/features/copilot#pricing)                         | [$19 (Business)](https://github.com/features/copilot#pricing)                             | Unlimited code completions, chat support, debugging, security remediation.                                      |
| **JetBrains AI Assistant** | [$10 (AI Pro)](https://www.jetbrains.com/ai-ides/buy/?section=personal&billing=monthly) | [$20 (AI Pro)](https://www.jetbrains.com/ai-ides/buy/?section=commercial&billing=monthly) | Integrated into JetBrains IDEs, local AI support, cloud credits for extensive AI usage.                         |
| **JetBrains Junie**        | [$20 (AI Ultimate)](https://www.jetbrains.com/junie/)                                   | [$40 (AI Ultimate)](https://www.jetbrains.com/junie/)                                     | AI agent for multi-step tasks, integrated into JetBrains IDEs. (Part of AI Assistant)                           |
| **Claude CLI**             | [$20 (Pro)](https://www.anthropic.com/pricing)                                          | [$25 (Team)](https://www.anthropic.com/pricing#team-&-enterprise)                         | Access to Claude models via CLI, higher usage limits than free tier.                                            |
| **Gemini CLI**             | [Free Tier / Pay-as-you-go](https://ai.google.dev/pricing)                              | [Pay-as-you-go / Subscription](https://ai.google.dev/pricing)                             | Access Gemini models via CLI, generous free tier, enterprise-grade features on Vertex AI.                       |
| **OpenAI Codex**           | [$20 (Plus)](https://openai.com/pricing)                                                | [$25 (Team)](https://openai.com/pricing)                                                  | Advanced AI coding assistant, supports GPT models, unlimited reasoning tasks.                                   |
| **TabNine**                | [$9 (Dev)](https://www.tabnine.com/pricing)                                             | [$39 (Enterprise)](https://www.tabnine.com/pricing)                                       | AI-powered code completion, personalized models, enterprise-grade security.                                     |
| **Lovable AI**             | [$20-$25 (Starter/Pro)](https://lovable.dev/pricing)                                    | [$30 (Teams)](https://lovable.dev/pricing)                                                | AI-powered UI/UX design, credit-based system, unlimited private projects.                                       |
| **Figma Dev Mode**         | [$15 (Dev Seat)](https://www.figma.com/pricing/)                                        | [$25 (Dev Seat)](https://www.figma.com/pricing/)                                          | Improved design-to-dev handoff, integrated into Figma's paid plans.                                             |
| **Google Stitch**          | [Free (in Google Labs)](https://labs.google/stitch)                                     | [Free (in Google Labs)](https://labs.google/stitch)                                       | AI design tool for generating UI from text prompts, sketches, or screenshots.                                   |
| **Google Firebase Studio** | [Free (up to 10 workspaces)](https://firebase.google.com/studio)                        | [Free (up to 10 workspaces)](https://firebase.google.com/studio)                          | AI-powered app development platform, integrates with Firebase and Google Cloud services.                        |

## Detailed Breakdown

### Cursor AI

- **Individual (Pro):** [$20/month](https://docs.cursor.com/account/plans-and-usage#individual-plans). This plan provides a monthly quota of "fast" requests for powerful AI models. Once the quota is exhausted, users can continue with unlimited "slow" requests on standard models or opt into usage-based pricing for additional "fast" requests.
- **Organization (Teams):** [$40/user/month](https://docs.cursor.com/account/plans-and-usage#team-plans). Includes all Pro features, with centralized billing and an administrative dashboard to monitor usage.
- **Hobby (Free):** A free tier with limited features and requests.
- **Enterprise:** Custom-priced plans for larger organizations, offering more usage, advanced security, and priority support.

### Windsurf AI

- **Individual (Pro):** [$15/month](https://windsurf.ai/pricing)
    - 500 prompt credits/month across all models
    - **IMPORTANT:** Currently limited Sonnet model support compared to competitors
    - Unlimited Fast Tab completion
    - [SWE-1](https://docs.windsurf.com/windsurf/models) model access (promotional 0 credits)
    - **NEW:** O3 model at 1x credit per prompt
- **Teams:** [$30/month](https://windsurf.ai/pricing)
    - 500 credits per user
    - Windsurf Reviews
    - Admin dashboard with analytics
    - SSO available (+$10/user/month)
- **Enterprise:** Starting at [$60/month](https://windsurf.com/pricing) (1,000 credits/user)

### GitHub Copilot

- **Free:** New tier with 50 agent mode requests, 2,000 completions/month
- **Pro:** [$10/month](https://github.com/features/copilot/plans#compare)
  - **NEW:** 6x(300) more premium requests than Free tier
  - **IMPORTANT:** Additional premium requests available at $0.04/request
  - **NEW:** Coding agent (preview) for autonomous code changes
  - **NEW:** Code review functionality
  - Access to Claude 3.7/4 Sonnet, Gemini 2.5 Pro, o3 models
- **Pro+:** [$39/month](https://github.com/features/copilot/plans#compare)
  - **NEW:** 30x more premium requests than Free
  - Access to Claude Opus 4, o3, GPT-4.5
- **Organization (Business):** [$19/month](https://github.com/features/copilot#pricing)
  - IP indemnity and enterprise controls

### JetBrains AI Assistant

- **Note:** The JetBrains AI Assistant is an add-on for JetBrains IDEs. The pricing below is for the AI Assistant only.
- **Individual (AI Pro):** [$10/user/month](https://www.jetbrains.com/ai-ides/buy/?section=personal&billing=monthly).
- **Organization (AI Pro):** [$20/user/month](https://www.jetbrains.com/ai-ides/buy/?section=commercial&billing=monthly).

#### IDE Pricing:

- **IntelliJ IDEA Ultimate:**
  - **Individual:** [$16.90/month or $169/year](https://www.jetbrains.com/idea/buy/#personal)
  - **Organization:** [$59.90/user/month or $599/user/year](https://www.jetbrains.com/idea/buy/#commercial)
- **WebStorm:**
  - **Individual:** [$6.90/month or $69/year](https://www.jetbrains.com/webstorm/buy/#personal)
  - **Organization:** [$15.90/user/month or $159/user/year](https://www.jetbrains.com/webstorm/buy/#commercial)

### JetBrains Junie

- **Note:** JetBrains Junie is an AI agent feature within the **JetBrains AI Assistant**. It is not a separate product and is included in the AI Assistant's pricing plans. But JetBrains is recommending to use AI Ultimate plan.
- **Individual (AI Pro):** [$20/user/month](https://www.jetbrains.com/junie/).
- **Organization (AI Pro):** [$40/user/month](https://www.jetbrains.com/junie/).
- **Functionality:** Junie can perform complex, multi-step tasks like writing code based on a high-level description and then running tests to verify it.

### Claude CLI

- **Individual (Pro):** $20/month for increased usage of the web interface, which includes access to "Claude Code" in the terminal.
- **Organization:** Pricing is based on API usage (pay-per-use). This can be more expensive for heavy usage.

### Gemini CLI

- **Individual:** A generous free tier is available through Google AI Studio. For higher usage, it's pay-as-you-go.
- **Organization:** Vertex AI offers lower costs for high-volume usage. Gemini for Google Cloud is a subscription service for businesses.

### OpenAI Codex

- **Individual (Plus):** [$20/month](https://openai.com/pricing). Includes access to GPT models optimized for coding tasks, extended limits on messaging, file uploads, and data analysis.
- **Organization (Team):** [$25/user/month](https://openai.com/pricing). Offers advanced models, secure workspace, and connectors to internal sources.
- **Enterprise:** Custom pricing for large-scale deployments with enhanced security and compliance.

### TabNine

- **Individual (Dev):** [$9/month](https://www.tabnine.com/pricing). Includes AI-powered code completion, natural language code generation, and basic personalization.
- **Organization (Enterprise):** [$39/user/month](https://www.tabnine.com/pricing). Offers advanced AI agents, private deployment options, and comprehensive IP protection.
- **Enterprise:** Custom pricing for air-gapped environments and fine-tuned models.

### Lovable AI

- **Individual (Starter/Pro):** $20-$25/month. Includes 100-250 credits per month.
- **Organization (Teams):** $30/month. Includes all Pro features, centralized billing, and access management for 20 seats.

### Figma Dev Mode

- **Individual (Dev Seat):** $15/user/month on the Professional plan.
- **Organization (Dev Seat):** $25/user/month on the Organization plan.

### Google Stitch

- **Individual & Organization:** Currently free as part of Google Labs.

### Google Firebase Studio

- **Individual & Organization:** Free to use for up to 10 workspaces by joining the free Google Developer Program. Potential costs are associated with integrated Firebase and Google Cloud services beyond their free quotas.


