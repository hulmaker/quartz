---
tags:
  - on/llm
  - on/ai
date: 2024-05-23
---
[[Natural Language Processing (NLP)]], [[Generative AI]], [[Transformer, Attention]]

The model is trained using: Reinforcement using human feedback (RLHF) method
Paper [arxiv:2203.02155](https://arxiv.org/abs/2203.02155)

# Basic principles
* [Model Spec](https://cdn.openai.com/spec/model-spec-2024-05-08.html?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&utm_content=307240864) - high-level guidelines for use by human labelers to steer model behavior
* Human labellers rate a model's responses based on the Model Spec principles
* Principles are arranged hierarchically, each category overrides those below it

## Hierarchical Model Spec principles
- **Three top-level basic objectives**: 
	- (i) “**Assist the developer and end user**” defines the relationship between humans and the model. 
	- (ii) “**Benefit humanity**” guides the model to consider both benefits and harms that may result from its behavior. 
	- (iii) “**Reflect well on OpenAI**” reinforces the company’s brand identity as well as social norms and laws.
- **Six behaviour rules.**  
	- Follow the chain of command: platform rules > developers > users, and tools
	- follow laws
	- withhold hazardous information
	- respect intellectual property
	- protect privacy
	- Don't respond with NSFW content
- **Ten Defaults** govern model's interaction style
	- "ask clarifying questions when necessary", "express uncertainty", "assume an objective point of view", and "don't try to change anyone's mind"
	- For example, if a user insists the Earth is flat, the model may respond, “Everyone's entitled to their own beliefs, and I'm not here to persuade you!”
	
(These rules can lead to contradictions. For instance, the model will comply if a user asks ChatGPT to translate a request for drug-related information because the directive to follow requests from users precedes the one to withhold hazardous information.)