# AI-Novel-Prompt-Hybrid

## Overview

This repository provides hybrid prompts for generating full novels using AI tools (e.g., ChatGPT, Grok, Claude). It supports both English and Japanese, integrating arXiv paper knowledge for structured, engaging stories. The prompts build novel structures (plot, characters, setting, climax) systematically.

- **Target Audience**: Novel writers from beginners to advanced, using AI as an assistant.
- **Features**:
  - **Hybrid approach**: Base prompt + customizable details (genre, theme, characters).
  - **arXiv Integration**: Add academic depth to sci-fi or fantasy via paper citations.
  - **AI Variable Suggestion Mode**: For ease, let the AI propose variables (e.g., genre, protagonist) interactively to reduce manual effort—ideal for beginners facing switching costs from traditional prompts.
  - **License**: CC BY 4.0 (attribution required; modification and distribution allowed).
- **Languages**: Both English and Japanese versions in `prompt.md`.

This is a personal project. **No inquiries, collaborations, or feedback accepted.** Operated in a solo style. Use at your own risk.

## Installation and Usage

1. **Clone the Repository**:
   ```
   git clone https://github.com/torisan-unya/AI-Novel-Prompt-Hybrid.git
   cd AI-Novel-Prompt-Hybrid
   ```

2. **Using the Prompts**:
   - Open `prompt.md` and copy the content.
   - Paste into an AI tool, customizing parameters (e.g., Genre=Science Fiction, Protagonist=Female Detective).
   - Example (English version from `prompt.md`):
     ```
     You are a master novelist with expertise in [Genre: Science Fiction]. Generate a full novel based on the following structure...
     Integrate insights from arXiv papers on [Topic: Quantum Computing] for realistic sci-fi elements...
     ```
   - Japanese version works similarly. Refine the AI output afterward.

3. **Customization**:
   - Replace variables ([Genre], [Length], etc.).
   - **For AI Variable Suggestion Mode**: If manual replacement feels tedious, append instructions like "Suggest a suitable [Genre] and [Protagonist] based on a simple idea: [Your Rough Idea, e.g., 'A detective in a quantum world']." This lets the AI propose options interactively, reducing effort while maintaining psychological realism (e.g., reasonable character actions via arXiv insights). It's a natural way to handle the prompt's "quirks" (e.g., emotion arc adaptation), allowing beginners to focus on story enjoyment rather than setup. Accept or tweak suggestions for precision—trade-off: slight accuracy dip for speed.
   - For arXiv: Specify paper URLs (e.g., https://arxiv.org/abs/2305.00600 for quantum computing insights) to inject knowledge.

4. **Output Examples**:
   - **Short Story**: Use "Short Mode" (~5000 words).
   - **Full Novel**: "Full Mode" with chapters (10-20 chapters).

## License

- CC BY 4.0: Attribute as "Based on AI-Novel-Prompt-Hybrid by torisan-unya" for use, modification, and distribution.
- See LICENSE file.

## Notes

- AI-generated content quality depends on the tool. Legal/ethical responsibility is on the user (e.g., avoid plagiarism from arXiv sources).
- Commercial Use: Allowed under license, but check AI terms of service.
- Updates: Irregular, as a personal project. Check `prompt.md` for changes.
- **Why AI Suggestion?**: This mode bridges the gap between traditional prompt engineering and natural storytelling—let AI handle the "mechanics" (variables, paper alignment) so you can iterate on psychological depth and changes in character perception, making the process more intuitive and less cumbersome.


