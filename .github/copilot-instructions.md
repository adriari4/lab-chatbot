# AI Agent Instructions for Chatbot Lab Project

This document provides essential knowledge for AI agents working with this codebase.

## Project Overview

This is a Jupyter notebook-based project that implements an OrderBot for a pizza restaurant using OpenAI's GPT models. The project demonstrates chat-based interactions and order processing.

## Key Components

1. **OpenAI Integration (`lab-chatbot.ipynb`)**
   - Uses OpenAI API with GPT-3.5-turbo model
   - Requires `OPENAI_API_KEY` in `.env` file
   - Key functions: `get_completion()` and `get_completion_from_messages()`

2. **GUI Components**
   - Uses Panel library (`pn`) for interactive interface
   - Main components: TextInput, Button, and conversation display panel
   - Interactive dashboard implementation in notebook

3. **OrderBot Implementation**
   - System messages define restaurant menu and bot behavior
   - Maintains context list for conversation history
   - JSON summary capability for order processing

## Development Workflow

### Environment Setup
1. Install required packages:
   ```python
   pip install openai "panel>=1.2.0" python-dotenv
   ```
2. Create `.env` file with your OpenAI API key:
   ```
   OPENAI_API_KEY=your-key-here
   ```

3. Known Issues and Best Practices:

   a) Panel Import and Initialization:
      - Import and initialize Panel ONCE at the start of the notebook:
      ```python
      import warnings
      warnings.filterwarnings("ignore")
      
      from openai import OpenAI
      import panel as pn
      import os
      from dotenv import load_dotenv, find_dotenv
      
      # Initialize Panel once
      pn.extension()
      ```
      
   b) Common Panel Warnings:
      - "Duplicate qualified model declaration": Caused by importing/initializing Panel multiple times
        - Solution: Remove duplicate imports and `pn.extension()` calls
        - Keep only one set of imports at the notebook start
        - Restart kernel after fixing imports
      
   c) Panel Dashboard Tips:
      - Use `dashboard.servable()` instead of just `dashboard` for better display
      - Put all widget definitions after Panel initialization
      - Use consistent variable names (`inp`, `panels`, `context`) throughout the notebook
      - Clean up old widget instances before recreating them

### Key Patterns

1. **Message Handling**
   ```python
   messages = [
       {'role': 'system', 'content': 'system_prompt_here'},
       {'role': 'user', 'content': 'user_message_here'}
   ]
   ```

2. **Conversation Context**
   - Context is maintained in the `context` list
   - Each interaction appends user input and assistant response
   - Format: `{'role': type, 'content': message}`

3. **Order Processing Flow**
   - Greet customer
   - Collect order details
   - Confirm pickup/delivery
   - Get delivery address if needed
   - Process payment
   - Generate order summary

## Testing & Debugging

- Test different conversation flows in notebook cells
- Use temperature=0 for deterministic responses
- Check order summary JSON format for correct itemization
- When using Panel:
  - Put all imports and Panel initialization at the start of the notebook
  - Run `warnings.filterwarnings("ignore")` before any imports
  - Call `pn.extension()` only once in your notebook
  - Test UI components after each modification
  - Use `dashboard.servable()` for improved display
  - Restart kernel if you encounter widget rendering issues

## Common Modifications

1. **Menu Updates**: Modify the `context` list's system message
2. **Bot Behavior**: Adjust system prompt in `context` initialization
3. **UI Customization**: Modify Panel widget properties in dashboard setup

Remember to run cells in sequence to maintain proper state and context.