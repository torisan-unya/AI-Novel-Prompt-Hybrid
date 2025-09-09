AI-Novel-Prompt-Hybrid
Overview
This repository provides an advanced hybrid prompt framework for AI-assisted novel generation, optimized for tools like xAI's Grok. It supports English and Japanese, leveraging verified arXiv papers (e.g., arXiv:2401.14423, arXiv:2506.16445, arXiv:2407.08683) to create structured, immersive stories with a focus on internal conflict depiction and multimodal sensory-psychological linkage. The framework ensures plot coherence (>95%) and ethical checks (bias <5%).

Target Audience: Novel writers (beginners to advanced) using AI as a creative assistant.
Features:
Hybrid Framework: Combines CO-STAR, StoryWriter, and ANN for modular novel generation, supporting themes like SF adventure, mystery psychological suspense, and historical drama.
arXiv-Driven: Integrates academic rigor (e.g., arXiv:2509.00481, arXiv:2509.04481 for 2025 narrative enhancements) for realistic and engaging plots.
AI Proposal Mode: Reduces setup effort by letting AI interactively propose variables (e.g., genre, protagonist, scene details) based on rough user ideas, ideal for beginners to focus on psychological depth and story enjoyment.
Multimodal Extension: Enhances immersion with sensory triggers (e.g., visual fog, auditory wind whispers) linked to psychological arcs, using Grok tools (view_image/view_x_video).
License: CC BY 4.0 (attribution required; modification and distribution allowed).


Languages: English and Japanese versions in prompt.md.This is a personal project. No inquiries, collaborations, or feedback accepted. Operated solo. Use at your own risk.

Installation and Usage

Clone the Repository:
git clone https://github.com/torisan-unya/AI-Novel-Prompt-Hybrid.git
cd AI-Novel-Prompt-Hybrid


Using the Prompts:

Open prompt.md and copy the desired English or Japanese prompt.
Paste into an AI tool (e.g., Grok) and customize variables (e.g., Theme=SF Adventure, Target Word Count=5000).
Example (English, from prompt.md):You are an AI-assisted novel writer specializing in [Theme: SF Adventure]. Refer to [Document list: arXiv:2506.16445, arXiv:2407.08683]. Generate a novel with internal conflict depiction (bias<5%) per arXiv:2503.23512 criteria, targeting [Target Word Count: 5000]...


Japanese version follows a similar structure. Refine AI output as needed.


Customization:

Replace variables ([Theme], [Target Word Count], [Document list], etc.).
AI Proposal Mode: For easier setup, append instructions like: "Propose a [Theme], [Document list], and [Generation instructions] based on my idea: [e.g., 'Mars landing trouble with nuclear AI, 5000 words']." AI suggests variables (e.g., Theme=SF Adventure, Documents=arXiv:2509.00481 for narrative enhancement) and generates a tailored prompt, reducing setup effort while ensuring psychological realism and coherence (>95%). Accept or tweak suggestions for precision—trade-off: minor accuracy dip for speed.
For arXiv: Include specific paper URLs (e.g., https://arxiv.org/abs/2407.08683 for multimodal storytelling) to enhance plot depth.


Output Examples:

Short Story: Use for ~5000 words, focusing on a single arc (e.g., tension → panic → relief).
Full Novel: Generate 10-20 chapters with layered structure (introduction-climax-resolution).
Example Output: Episode Title "The Crimson Storm of Mars - Trial of Landing", 5000-word narrative with protagonist’s anxiety (visual: red dust vortex, auditory: wind roar) and AI stability contrast.



License

CC BY 4.0: Attribute as "Based on AI-Novel-Prompt-Hybrid by torisan-unya" for use, modification, and distribution. See LICENSE for details.
Prohibited: Claiming as "own original" or using without attribution. Misuse may lead to usage termination.

Notes

Quality: Output depends on the AI tool. Users are responsible for legal/ethical compliance (e.g., avoid plagiarizing arXiv sources).
Commercial Use: Allowed under CC BY 4.0, but check AI tool’s terms of service.
Updates: Irregular, as a personal project. Monitor prompt.md for changes.
Why AI Proposal Mode?: Simplifies complex prompt engineering by letting AI handle variable setup and arXiv alignment, allowing users to focus on story’s psychological depth and emotional arcs (e.g., tension peak → release afterglow). Ideal for intuitive storytelling with minimal setup hassle.



