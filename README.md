# HyperSense-VLM-RL-Agent
A multimodal embodied agent that uses Vision-Language Models and Deep Reinforcement Learning to understand natural-language instructions and act intelligently inside 3D environments. Combines semantic grounding, visual perception, and RL-based control for instruction-following tasks.
                 ┌─────────────────────────────┐
Instruction --> │        VLM / LLM           │
 (text prompt)  │ (LLaVA / BLIP2 / CLIP+LLM) │
                └───────────┬─────────────────┘
                            │ semantic embedding + grounding
                            ▼
  ┌──────────────┐    ┌──────────────────┐    ┌────────────┐
  │  Simulator   │    │ Perception (CNN) │    │ Agent Sate │
  │ (AI2-THOR)   │--->│  visual features  │<---│  + proprio │
  │ RGB / Depth  │    └──────────────────┘    └────────────┘
  └──────────────┘             │                      │
           │                   └──────┬───────────────┘
           │                          │ fused state
           ▼                          ▼
     Observation Buffer        Fusion Module (attention)
                                (visual + language + goal)
                                         │
                                         ▼
                                Policy Network (PPO)
                                ┌────────────┬──────────┐
                                │   Actor    │  Critic  │
                                └────────────┴──────────┘
                                         │
                              Discrete / Continuous actions
                                         │
                                         ▼
                                  Simulator (exec actions)
                                         │
                                         ▼
                         Reward signal (env + VLM verifier)
                                         │
                                         ▼
                                  Training loop & logs
