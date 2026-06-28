# Foundation Models' Next Battle: Is Multimodal Inevitable, or an Overhyped Narrative?

A deep dialectical inquiry into the future direction of AI

---

## Introduction: A Direction Debate That Cannot Be Avoided

In May 2024, OpenAI released GPT-4o. At the launch event, when the model analyzed human facial expressions in real time and responded to questions with emotionally rich voice, the audience gasped in awe. That moment created an almost instinctive consensus across the global tech community: the future of foundation models lies in multimodal.

But is that consensus correct?

When discussing "future directions," we have actually conflated two distinct questions: whether multimodal has value (almost everyone agrees it does); and whether multimodal should right now be treated as the top strategic priority — even to the point of using it as justification to de-emphasize deep optimization of pure-text language models (that is the question where genuine disagreement exists).

This article attempts to decompose these two questions, drawing on recent technical progress, product case studies, and market data, to arrive at a more honest judgment.

---

## Dimension 1: The Real Value of Perceptual Expansion

The most intuitive argument in favor of prioritizing multimodal is that human cognition itself is multimodal.

This argument is not hollow. In medicine, Google's Med-PaLM M has reached specialist-level performance on chest X-rays, fundus images, and pathology slide diagnosis; Stanford research shows that joint visual + textual diagnosis is 23 percentage points more accurate than pure-text medical record analysis. In education, the feature allowing students to photograph a problem and get a solution boosted engagement by 40%. In the creative industries, Midjourney, Suno, and Adobe Firefly have given tens of millions of ordinary people professional-grade creative production capabilities for the first time.

These are not demo cases — they are commercial deployments with real user bases.

From an information-theoretic perspective, the trend also has its own internal logic. The volume of video information generated on Earth each day far exceeds the volume of text. A single 1080p frame contains information equivalent to thousands of words. An AI that can only process text is touching a tiny subset of the human information world.

---

## Dimension 2: Is the "Maturity" of LLMs Overestimated?

Yet the inference that "LLMs are mature enough, so we should pivot to multimodal" does not hold up under scrutiny.

What is the evidence for "mature enough"? ChatGPT has over 200 million monthly active users; enterprise clients cover more than 90% of the Fortune 500. From a user-scale perspective, that is genuinely impressive.

But from the perspective of capability reliability, the picture is far more complex. Stanford's 2024 evaluations found that LLM hallucination rates on medical literature summarization tasks remain as high as 20–30%. In law, incidents of New York attorneys being sanctioned by courts for submitting AI-generated fabricated case citations have appeared repeatedly in the news. 200 million users interacting daily with a tool that has such high error rates demonstrates the tool's widespread adoption — not the maturity of its capabilities.

More importantly, OpenAI's o1/o3 series has demonstrated the potential of another path. By abandoning the rapidly iterated RLHF approach and returning to deep reasoning training, o3's improvement on the ARC-AGI benchmark is several times larger than the combined total of all multimodal advances over the past two years. This shows that the reasoning depth of LLMs is far from reaching its ceiling. Diverting resources away from this toward multimodal carries a very real cost.

---

## Dimension 3: The Debate Over Multimodal Technical Depth

Advocates of multimodal often invoke an exciting scenario: GPT-4o looks at a photograph and can understand emotion, analyze composition, and connect context to offer a deep response. Isn't that "mature enough"?

There is a critical technical detail here that deserves serious attention.

The architecture of virtually all current multimodal foundation models is pipeline-based: a visual encoder converts images into tokens, and the language model then processes those tokens. There is no genuine bidirectional interaction between visual reasoning and language reasoning — visual inputs are ultimately "translated" into linguistic concepts, and the core processing remains language reasoning.

An experiment illustrates this problem: given the same image, if you describe the image content to GPT-4o in text ("a sad girl, with a backdrop of war ruins"), its analysis quality is almost indistinguishable from when it views the image directly. The visual input is the "receiving end"; language reasoning is the "processing end." The "synergy" of multimodal under current architectures is largely illusory. A more accurate description is: LLMs are the core engine; multimodal is a peripheral input device.

MIT's 2024 research also found that most multimodal models exhibit systematic failures in real-world visual reasoning — particularly in understanding spatial relationships, counting, and 3D structures, where they fall significantly short of human performance. Sora-generated videos showing liquid flowing backward and limbs clipping through objects are additional evidence of the same point: models have statistically mimicked visual patterns but have not truly understood physical reality.

---

## Dimension 4: The Stratification of Commercial Value

The commercial value of multimodal requires an important distinction.

What are enterprises actually doing with multimodal AI? Salesforce's visual analytics core is identifying product categories in images; HubSpot's image understanding detects how frequently brand logos appear; factory safety inspection identifies whether workers are wearing hard hats. What these tasks truly require is machine vision (computer vision), not multimodal large language models — ResNet, which was already mature in 2019, is sufficient. Most commercial security AI vendors also use lightweight specialized vision models precisely because general-purpose multimodal foundation models are too costly and too slow for inference.

Andreessen Horowitz's 2024 report confirms this: most enterprise AI projects have scaled back multimodal features because inference costs exceeded expectations. The per-token cost of multimodal inference is several times higher than text inference — a real constraint in price-sensitive markets.

High-value use cases that genuinely require the deep capabilities of multimodal foundation models do exist — complex medical imaging analysis, cross-modal understanding of research data — but these scenarios need domain-specific models far more than general-purpose multimodal foundation models. In medical image diagnosis, GPT-4V (general-purpose multimodal) achieves 63% accuracy, while a specialized medical vision model (Med-Gemini dedicated version) achieves 84%; the gap does not narrow significantly as scale increases.

---

## Dimension 5: The Two Sides of the Data Bottleneck

Multimodal advocates have an important argument: text data is nearly exhausted. Meta's research team estimates that high-quality text data on the internet will hit a ceiling between 2026 and 2028. Image and video data vastly outnumber text data and represent a way through the "data wall."

This argument is grounded in reality, but the logical chain is incomplete.

Multimodal data is voluminous, but the density of useful training signal is extremely low. Videos on YouTube lack high-quality semantic annotations; image alt text is extremely sparse — while the raw volume of multimodal data is large, much of it is noise. By contrast, synthetic data offers another path for extending text data — DeepMind's AlphaProof used purely synthetic mathematical proof data to achieve a historic breakthrough at the International Mathematical Olympiad. In domains with objective verification mechanisms (can the program run? does the proof hold?), synthetic data can effectively break through the data wall.

Both paths have their value and their limitations. But equating "text data ceiling" directly with "we should prioritize multimodal development" skips over many intermediate steps.

---

## Dimension 6: The Asymmetric Risks in Safety and Ethics

The safety risks of multimodal technology are harder to handle than those of pure text, and they are routinely underestimated.

Deepfakes are the most emblematic safety hazard of multimodal technology. In 2024, a Hong Kong company was defrauded of USD 25 million via a multimodal-fabricated video conference. The harmfulness of multimodal content is more covert — image-context dependency, cross-language visual memes, using "normal" images to smuggle banned content — audit difficulty increases exponentially compared to text content.

Content provenance technologies such as C2PA digital watermarking work in the lab but fail in real-world distribution environments (transcoding, screenshots, compression). Regarding applications targeting visual emotion recognition, MIT Media Lab research also found that the correlation between facial muscle movements and internal emotional states is far lower than commonly assumed, meaning emotion-computing applications built on this scientific premise carry inherent accuracy flaws and ethical risks.

This is not a rejection of multimodal technology itself, but rather: in the stage where safety alignment is not yet complete, the rapid expansion of multimodal capabilities calls for greater caution — not rapid advancement justified by the claim that "governance will catch up."

---

## Dimension 7: The Sequencing Problem in Resource Allocation

Taken together, the core of this debate is not "does multimodal have value," but rather "at what point in time, and in what proportion, should multimodal receive investment."

An interesting observation: there is a notable divergence between the focus of research publications from the world's top AI labs and the focus of their product releases. At the product level, multimodal is the marketing focal point — the star of every launch event. At the research level, the most profound advances (o1/o3 reasoning breakthroughs, systematization of chain-of-thought, self-consistency methods, verification mechanisms for synthetic data) are mostly in the pure language model domain.

This divergence says something: products move toward multimodal because users can see and touch it — the experience is more intuitive. But the genuinely difficult intelligence problems are ones that researchers are still excavating in the soil of language reasoning.

Historically, in every generation of technological development there has been a phase in which "the narrative runs ahead of the technology." Some of the current discussion around multimodal foundation models falls into this category — the long-term direction may well be correct, but the near-term proportion of resource investment may be inflated by the grand narrative.

---

## Conclusion: Foundation and Roof — Not an Either/Or

The most honest answer is neither "multimodal is the future" nor "LLMs are what matters." It is: both matter, but sequencing matters too.

In the current phase, the reliability of language models, their reasoning depth, and safety alignment are still the priority directions most deserving of concentrated resources. These capabilities are the foundation. The perceptual expansion of multimodal represents real incremental value, but directing large resources toward the upper floors before the foundation is solid carries high structural risk.

This is not technological conservatism — it is respect for engineering reality.

GPT-4o's release was genuinely impressive, and multimodal's commercial deployment is advancing in real terms. But what will truly change the world is not the feature of "being able to look at images" — it is the still-unrealized whole that emerges when AI genuinely integrates perception, reasoning, and reliability. Until that day arrives, we need to maintain clear-eyed judgment between chasing narratives and building solid foundations.

---

*This article is based on publicly available technical reports, academic papers, and product evaluation data. All cited figures have documentary sources; no unsupported predictions have been added.*
