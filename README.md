# Spring-AI Project Based learning
A spring boot Project using Spring AI

# What is Spring AI?
 Spring AI is a Spring framework that provides abstractions and integrations for building AI-powered applications in Java and Spring Boot.
    **It allows Developers to integrate applications with AI models 
    Multi model & provider support- works with open AI, Ollama etc. and switch providers by just changing configurations.
    Spring friendly apis- provides Spring beans for the AI client
    Chat History and Memory Support
    Easily Inegrated with Spring boot Applications**
 such as OpenAI, Azure OpenAI, Google Gemini, Anthropic, and others without having to handle the low-level API communication ourselves.

Using Spring AI, we can implement features like chat, prompt management, structured outputs, embeddings, RAG, vector databases, and document-based question answering.

For example, in a Spring Boot application, I can use Spring AI's ChatClient to send a user prompt to an AI model and get the response, similar to how we use RestTemplate or WebClient to communicate with external services

We can directly call an AI provider's REST API, but then our application becomes tightly coupled to that provider. Spring AI provides a common abstraction between our Spring Boot application and AI models. This makes integration easier and reduces provider-specific code. It also gives us ready-to-use features like prompts, structured output, embeddings, vector stores and RAG

```text
Spring AI
│
├── ChatClient / Chat Models
│   └── ChatClient is a high-level API used from a Spring Boot application to interact with chat-based AI models.
│
├── Prompt Templates
│   └── Prompt Templates are reusable prompts with dynamic values that can be passed at runtime.
│
├── Structured Output
│   └── Structured Output allows AI responses to be returned in a predictable format such as JSON or a Java object.
│
├── Embeddings (Vector DB+RAG-enabled RAG for better Q&A)
│   └── Embeddings convert text into numerical vectors that represent the semantic meaning of the text.
│
├── Vector Stores
│   └── Vector Stores store embeddings and help find documents or data that are semantically similar to a user's query.
│
├── RAG #Retrieval Augmented Generation
│   └── RAG retrieves relevant information from external documents or databases and provides it to the AI model as context.
│
├── Advisors
│   └── Advisors allow us to intercept and customize AI interactions, such as adding context, memory, logging, or RAG.
│
├── Tool Calling
│   └── Tool Calling allows an AI model to request execution of application-defined functions, APIs, or business operations.
│
├── Memory / Chat History
│   └── Memory stores previous conversation context so the AI can understand follow-up questions.
│
└── Document Readers & Transformers
    └── Document Readers and Transformers load documents and prepare their content for processing, embedding, and RAG.
```

  # Chat Client:
  @RestController
public class AIController {

    private final ChatClient chatClient;

    public AIController(**ChatClient.Builder builder**) {
        this.chatClient = builder.build();
    }

    @GetMapping("/ask")
    public String ask(@RequestParam String question) {

        return chatClient
                .prompt()
                .user(question)
                .call()
                .content();
    }
}

# Prompts management
  -We can store prompts in extenal files(.st,.mustache)

