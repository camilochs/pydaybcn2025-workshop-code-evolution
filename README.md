# Code Evolution: Self-Improving Software with LLMs and Python

**Workshop for PyDay Barcelona 2025**


Level: Beginner/Intermediate

Requirements: Basic Python knowledge, familiarity with APIs

## Abstract

What if your code could fix its own bugs, evolve better solutions, and create new capabilities on demand? This workshop explores the intersection of Large Language Models and evolutionary computation to build software that improves itself.

Through four hands-on demos, participants will implement increasingly sophisticated self-improvement patterns: from simple error correction to Darwinian evolution of code, agents that write their own tools, and finally a multi-agent team that evolves its own system prompts through competition.

## Workshop Structure

| Section | Duration | Description |
|---------|----------|-------------|
| Introduction | 10 min | Theory: Why combine Evolution + LLMs? |
| Environment Setup | 5 min | API keys, Google Colab configuration |
| Demo 1: Self-Reparation | 15 min | Basic error correction loop |
| Demo 2: Code Evolution | 25 min | Genetic algorithms with LLM operators |
| Demo 3: Toolmaker | 20 min | Runtime self-modification |
| Demo 4: Evolving Team | 25 min | Multi-agent prompt evolution |
| Q&A / Discussion | 10 min | Security, ethics, and limitations |

## The Four Demos

### Demo 1: The Self-Reparation (Basic)

**Concept:** Self-Correction / Reflexion

A script that automatically fixes its own bugs by:
1. Executing code and capturing errors (stderr)
2. Sending the code + traceback to an LLM
3. Receiving and applying the corrected code
4. Re-executing successfully

This demonstrates the fundamental feedback loop: using execution output as a "learning signal" for improvement.

**Related Research:**
- [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651)
- [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366)

### Demo 2: Code Evolution (Intermediate)

**Concept:** Genetic Algorithm with LLM as Mutation Operator

Instead of fixing errors, we optimize solutions through evolution:
1. **Population**: LLM generates initial candidates
2. **Evaluation**: A fitness function scores each candidate
3. **Selection**: Keep the best performers
4. **Mutation/Crossover**: LLM combines winning traits to create offspring
5. **Repeat** for multiple generations

The problem: Generate passwords meeting complex, interacting constraints (length, emoji requirements, digit sum equals exactly 15, etc.)

**Related Research:**
- [FunSearch: Making new discoveries in mathematical sciences using LLMs](https://www.nature.com/articles/s41586-023-06924-6) (Nature, 2023)
- [Eureka: Human-Level Reward Design via Coding LLMs](https://arxiv.org/abs/2310.12931)

### Demo 3: The Agent Toolmaker

**Concept:** Self-Modification / Hot-swapping

An agent that creates capabilities it doesn't have:
1. Agent receives a request (sentiment analysis)
2. Detects missing tool (`ToolNotFoundError`)
3. Uses LLM to write a new Python function
4. Adds it to `tools.py` and hot-reloads via `importlib.reload()`
5. Completes the original request with its new capability

The system gains complexity with use - each tool persists for future interactions.

**Related Research:**
- [Voyager: An Open-Ended Embodied Agent with LLMs](https://arxiv.org/abs/2305.16291)
- [MetaGPT: Meta Programming for Multi-Agent Collaboration](https://arxiv.org/abs/2308.00352)

### Demo 4: The Evolving Dev Team 

**Concept:** Self-Evolving Agent Prompts / Multi-Agent Competition

Two AI developer agents with different philosophies compete to solve coding problems:
1. **Round 1**: Both solve a problem with their initial system prompts
2. **Evaluation**: A Tech Lead runs actual tests and scores solutions
3. **Evolution**: Each agent rewrites their own system prompt based on feedback
4. **Round 2**: Agents use their evolved prompts on a new problem
5. **Analysis**: Compare performance before and after evolution

The key insight: agents that reflect on their mistakes can improve their own instructions. We observe emergent strategies that weren't explicitly programmed.

**Related Research:**
- [Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651)
- [OPRO: Large Language Models as Optimizers](https://arxiv.org/abs/2309.03409)
- [Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073)

## Technical Requirements

### For Participants

- Google account (for Colab)
- One of the following API keys:
  - OpenAI API key with credits (~1 euro should be sufficient) - Recommended
  - Google Gemini API key (FREE) - [Get it here](https://aistudio.google.com/apikey)
  - Groq API key (FREE, very fast) - [Get it here](https://console.groq.com)
- Modern web browser

### Technologies Used

- Python 3.10+
- LLM API (OpenAI gpt-4o-mini, Google Gemini, or Groq Llama 3.1)
- Google Colab
- TextBlob (for sentiment analysis demo)

## Setup Instructions

1. Open the notebooks in Google Colab
2. Configure your API key in Colab Secrets:
   - Click the key icon in the left sidebar
   - Add your API key as a secret (choose one):
     - `OPENAI_API_KEY` for OpenAI (recommended)
     - `GEMINI_API_KEY` for Google Gemini (free)
     - `GROQ_API_KEY` for Groq (free, very fast)
   - Enable notebook access
3. In each notebook's setup cell, uncomment the section for your chosen provider
4. Run cells sequentially

### Using Free Alternatives

**Google Gemini (FREE):**
1. Get a free API key from [Google AI Studio](https://aistudio.google.com/apikey)
2. Add secret `GEMINI_API_KEY` in Colab Secrets
3. In each notebook's setup cell, comment out OpenAI and uncomment the Gemini section

**Groq (FREE - Very Fast):**
1. Get a free API key from [console.groq.com](https://console.groq.com)
2. Add secret `GROQ_API_KEY` in Colab Secrets
3. In each notebook's setup cell, comment out OpenAI and uncomment the Groq section
4. Note: Groq uses Llama 3.1 model, which is very capable for these demos

## Files

```
pydaybcn2025-code-evolution/
    README.md                    # This file
    demo_01_self_reparation.ipynb    # Bug fixing feedback loop
    demo_02_evolution.ipynb      # Genetic algorithm with LLM
    demo_03_toolmaker.ipynb      # Self-modifying agent
    demo_04_evolving_team.ipynb  # Multi-agent prompt evolution
```

## Key Concepts

### The Feedback Loop

All three demos share a common pattern:

```
Action -> Outcome -> Evaluation -> LLM Improvement -> Better Action
```

The key insight is treating program output (errors, scores, missing capabilities) as training signal for the LLM.

### LLM as Intelligent Operator

Unlike traditional genetic algorithms with random mutations, LLMs provide:
- Semantic understanding of what makes solutions good
- Directed improvement rather than random exploration
- Ability to combine abstract concepts across candidates

### Open-Ended Systems

Demo 3 illustrates open-endedness: systems that grow in complexity without predefined limits. The agent's capability space expands with each new tool it creates.

### Self-Evolving Prompts

Demo 4 shows meta-learning: agents that improve their own instructions. Through competition and reflection, they discover strategies we never explicitly taught them.

## Safety Considerations

These demos use `exec()` and dynamic code generation. In production:

- Sandbox all LLM-generated code (containers, VMs)
- Validate code before execution
- Implement human review for critical changes
- Maintain audit trails of self-modifications
- Set resource limits to prevent runaway processes

## Further Reading

### Papers

1. Madaan et al. (2023). "Self-Refine: Iterative Refinement with Self-Feedback"
2. Shinn et al. (2023). "Reflexion: Language Agents with Verbal Reinforcement Learning"
3. Romera-Paredes et al. (2023). "Mathematical discoveries from program search with LLMs" (FunSearch)
4. Ma et al. (2023). "Eureka: Human-Level Reward Design via Coding LLMs"
5. Wang et al. (2023). "Voyager: An Open-Ended Embodied Agent with LLMs"
6. Hong et al. (2023). "MetaGPT: Meta Programming for Multi-Agent Collaboration"
7. Yang et al. (2023). "Large Language Models as Optimizers" (OPRO)
8. Bai et al. (2022). "Constitutional AI: Harmlessness from AI Feedback"

### Code Improving (Author's Research)

1. Chacon Sartori & Blum (2025). "[irace-evo: Automatic Algorithm Configuration Extended With LLM-Based Code Evolution](https://arxiv.org/abs/2511.14794)"
2. Chacon Sartori et al. (2025). "[Metaheuristics and Large Language Models Join Forces: Toward an Integrated Optimization Approach](https://ieeexplore.ieee.org/document/10818476)" (IEEE Access)
3. Chacon Sartori & Blum (2025). "[Optimizing the Optimizer: An Example Showing the Power of LLM Code Generation](https://annals-csis.org/Volume_43/drp/1481.html)" (FedCSIS '25)
4. Chacon Sartori & Blum (2025). "[Combinatorial Optimization for All: Using LLMs to Aid Non-Experts in Improving Optimization Algorithms](https://camilochs.github.io/comb-opt-for-all/)"

### Related Concepts

- Evolutionary Computation
- Genetic Programming
- Neural Architecture Search
- Program Synthesis
- Automated Machine Learning (AutoML)

## License

MIT License - Feel free to use and adapt for your own workshops.

## Author

[Camilo Chacón Sartori](www.camilochacon.com).

Workshop developed for PyDay Barcelona 2025.
