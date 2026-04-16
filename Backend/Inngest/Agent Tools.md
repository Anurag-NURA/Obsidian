# 🧠 Inngest + Tools (Agent Kit) — Quick Notes

## 🔹 What is a Tool?

Tools are functions that extend the capabilities of an [Agent](https://agentkit.inngest.com/concepts/agents). Tools have two core uses:
- Calling code, enabling models to interact with systems like your own database or external APIs.
- Turning unstructured inputs into structured responses.

> A **tool** is a function the AI agent can call to perform real actions.
- Without tools → AI only generates text
- With tools → AI can **act, execute, and interact with systems**

## 🔹 Why Tools Matter

They turn your agent from:
❌ “just answering”  ➡️ into  ✅ “doing things” (run commands, fetch data, write files)


## Creating a Tool

Each Tool’s `name`, `description`, and `parameters` are part of the function definition that is used by model to learn about the tool’s capabilities and decide when it should be called. The `handler` is the function that is executed by the Agent if the model decides that a particular Tool should be called. 

Here is a simple tool that lists charges for a given user’s account between a date range:
```ts
import { createTool } from '@inngest/agent-kit';

const listChargesTool = createTool({
	name: 'list_charges',
	description: "Returns all of a user's charges. Call this whenever you need to find one or more charges between a date range.",
	parameters: z.object({
    userId: z.string(),
    created: z.object({
			gte: z.string().date(),
			lte: z.string().date(),
	    }),
	}),
	handler: async ({ userId, created }, { network, agent, step }) => {
	    // input is strongly typed to match the parameter type.
	    return [{...}]
	},
});
```

**NOTE**: Writing quality `name` and `description` parameters help the model determine when the particular Tool should be called.


### Project Example:
Integrating Terminal with E2B Sandbox

```ts
const codeAgent = createAgent({
	name: "summarizer",
	system:
	"You are an expert next.js developer. You write readable, maintainable code. You write simple Next.js & React snippets",
	model: openai({ model: "gpt-4o", apiKey: process.env.OPENAI_API_KEY }),
	tools: [
		createTool({
			name: "terminal",
			description:
			"Use the terminal to run commands in the sandbox environment",
			parameters: z.object({
			command: z.string().describe("The command to run in the terminal"),
			}),
			handler: async ({ command }, { step }) => {
				return await step?.run("run-terminal", async () => {
					/*
					The output can come in chunks, so we need to buffer it until the command is complete
					"Installing..."
					"Downloading packages..."
					"Done"
					*/
					const buffers = { stdout: "", stderr: "" };
					try {
					const sandbox = await getSandbox(sandboxId);
					const result = await sandbox.commands.run(command, {
						onStdout: (data: string) => {
							buffers.stdout += data;
						},
						onStderr: (data: string) => {
							buffers.stderr += data;
						},
					});
				
					return result.stdout;
				  } catch (error) {
						console.error(
						  `Command failed: ${error} \nstdout: ${buffers.stdout} \nstderr: ${buffers.stderr}`,
						);
						return `Command failed: ${error} \nstdout: ${buffers.stdout} \nstderr: ${buffers.stderr}`;
				  }
				});
			},
		}),
	],
});

```