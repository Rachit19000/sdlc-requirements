Lecture 1

Lecture 2

Lecture 3

 

Other frameworks other than Langchain are Haystack, LlamaIndex

Lecture 4

In models the main problem was that different LLM providers wrote their code in different ways. That means if I am an application developer and I want to coomuicate with llm apis then I need tp nwrite two different types of codes.

Langchain creates this uniformity

Models component creates this uniformity

Through the chains in langchain, we can build pipelines. 
Chains automatically make the output of from the previous output as the input of next

Parallel chains vs Conditional chains ( AI feedback loop )

 

LLM APIs are stateless means that the LLM APIs doesn’t remember what you you to them ( ie- they don’t store your information )
They don’t have any clue regarding the previous requests that you give to them. This is solved with the help of concept of memory

AI agent is chatbot with superpowers. Chatbot can only do conversations, whereas AI agents can do the work too , because AI agents have reasoning capability ( which is done using chain of thought prompting )  and they also have access to tools

The setup to start creating the models in Langchain

   these are the commands to verify the installation of Langchain

Libraries required in requirement.txt

Normal LLMs

Chat Models- In the chat model along with the content rest all information is also shown. We need to extract the content from this

Temperature sets the randomness of output upon changing the input

This is the same uniform code for importing the Claude model from the Anthropic

Open Source models can be downloaded and run onto our own machines

Accesing the huggingface models through the api’s we use HuggingFaceEndpoint, whereas for downloading the model locally we use the HuggingFacePipeline 

Running the model locally

Done till 1:18:00, after that embedded models were there

Lecture 6

Static vs dynamic prompts

Watched till 30:00

Lecture 7

Structured outputs are in JSON format

AI agents tools , databses cannot work on textual outputs. They need structured responses to work properly

For calling the tools, we use the function calling or tool calling inside the place of the method

Lecture 8

Output parsers can work with LLMs that can provide structured outputs and that cannot provide structured outputs

Without using chains and strOutputParser

Using chains and parsers

Till json output parser : 22:26

summary

Lecture 9
With the help of chains, we can create a pipeline. Three types of chains- sequential, parallel, conditional

Simple chain 

Lecture 18 - Tools
Building AI agents using langchain using various tools

Tools are like functions which can interact with LLMs or LLMs can call the tool

Built in tools are for common usecases and custom tools are for custom usecases

 

Whenever we send the tool to LLM, we do not send the complete tool ( else we send its schema )

2) using StructuredTool & Pydantic

 

3) Using Base Class Tool
Here we can create async versions of our tools to handle concurrency of handling multiple tools

Toolkits

Lecture 19

 

Tools execution 
 

After Tool creation, binding, calling, execution send it to LLM to generate the output
 

Currency conversion tool

   

Basically while calling the first tool, the answer or output of that call did not come to the call, so it processed some wrong values from its buffer and gave the wrong conversion rate ( 73.73 )
Injected tool argument is the method in langchain to solve this problem, and in this we set the value of that argument…..LLM does not do it on its own

Lecture 20

First we create a set of tools, then we decide a LLM. And then from those tools and LLM we create an Agent which could be based on different design patterns such as React, Self ask with search 

The right side diagram is a singleton interaction. But, React is different from this which is a multistep process is implemented to solve a given problem in a structured manner.
In React the loop of thought, action and observation is executed

Langchain hub is the github for providing prompts to the agents

This is one of the examples of the prompt

Agent scratchpad is the thought trace of the agent