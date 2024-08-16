---
parser: v2
auto_validation: true
time: 45
primary_tag: software-product>sap-business-technology-platform
tags: [ tutorial>beginner, topic>artificial-intelligence, topic>machine-learning, software-product>sap-business-technology-platform ]
author_name: Dhrubajyoti Paul
author_profile: https://github.com/dhrubpaul
---

# Using Multimodal inputs with GPT4o for Image Recognition on SAP AI Core
<!-- description --> In this tutorial we are going to learn on how to consume GPT4o LLM on AI core deployed on SAP AI core.

## You will learn
- How to inference GPT4o with multimodal inputs on AI core

## Prerequisites
Ai core setup and basic knowledge: [Link to documentation](https://developers.sap.com/tutorials/ai-core-setup.html)
Ai core Instance with Standard Plan or Extended Plan

Multimodality refers to the ability of a model to process and interpret different types of inputs, such as text, images, audio, or video. In the context of GPT-4o on SAP AI Core, multimodal input allows the model to understand and generate responses that incorporate both text and visual data. This enhances the model's ability to perform complex tasks, such as scene detection, object recognition, and image analysis, by combining the strengths of both language processing and image recognition.
In this tutorial, we'll demonstrate these capabilities with the help of GPT-4o, with a sample input and output, which can be replicated in future for various use cases.

### Scene Detection

In this step, we demonstrate how to use GPT-4o to describe a scene depicted in an image. By providing both text and an image URL as input, the model is able to generate a descriptive response that captures the key elements of the scene. This capability is particularly useful for applications like automated content tagging, visual storytelling, or enhancing user experience in multimedia platforms and more.

Follow the further steps to replicate scene detection using GPT-4o.

[OPTION BEGIN [curl]]

The following example shows how you can consume this generative AI model using curl. For more information about prompts, see the tutorial [Prompt LLMs in the Generative AI Hub in SAP AI Core & Launchpad Information published on SAP site](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fdevelopers.sap.com%2Ftutorials%2Fai-core-generative-ai.html).

Before you use this model, please ensure that the deployment has already been created. You can create the deployment either through [generative-ai-hub-sdk or AI Launchpad](https://developers.sap.com/tutorials/ai-core-generative-ai.html#ad7ffc1e-e94e-4de4-b70f-116b038aff04).

For inferencing the model through curl,

- open Windows PowerShell (for Windows based devices)

NOTE: **do not use DOS Prompt instead of PowerShell**

- open Terminal (for macOS based devices)

Enter the following command after replacing `<deployment_url>`, `<resource-group>`, `<token>` with the values for the corresponding model.

NOTE:
 
 - for macOS based devices use  use the **bash** command

 - for windows devices, use the **PowerShell** command

 - Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```bash
curl -L '<deployment_url>/chat/completions?api-version=2023-05-15' \
--header 'AI-Resource-Group: <resource-group>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "describe the scene"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/sceneDetection.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}'
```

```PowerShell
curl.exe -L "<deployment_url>/chat/completions?api-version=2023-05-15" --header "AI-Resource-Group: <resource-group>" --header "Content-Type: application/json" --header "Authorization: Bearer <token>" --data '{\"messages\": [{\"role\": \"user\", \"content\": [{\"type\": \"text\",\"text\": \"describe the scene\"},{\"type\":\"image_url\",\"image_url\": {\"url\": \"https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/sceneDetection.jpg\"}}]}],\"max_tokens\": 4096 }'
```

After executing the above curl command, we'll get the output as follows - 

![output](img/sceneCurlOP.png)

[OPTION END]

[OPTION BEGIN [Postman]]

To begin using the APIs in AI Core, we start with setting up the authentication methods.

![image](img/consumption1.png)
![image](img/consumption2.png)
For ease of access, we set up the region, baseUrl and deploymentUrl variables as a pre-requisite. This avoids the need of passing these values repeatedly for different scenarios. 
NOTE: the deployment URL is specific to the model we intend to use.

![image](img/consumption34.png)
Add the name of your respective resource group. 

![image](img/consumption5.png)
Next, to begin making API calls, we’ll create a new access token. Now we’re ready to use the API for various models.

![image](img/consumption6.png)

Now that we’re done with the pre-requisites, we’ll proceed to using the API for GPT4o for Scene Detection.

**NOTE:** Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```Body
{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "describe the scene."
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/sceneDetection.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}
```

Add the above data in the body of the POST call, then hit ‘Send’ as follows - 

![image](img/scene%20detection.png)

We get the following output accurately describing the scene in the image:

![image](img/scene%20detection%20output.png)
[OPTION END]

For more information on the models refer to [Hello GPT-4o](https://openai.com/index/hello-gpt-4o/)

### Object Detection

This step focuses on identifying and labeling objects within an image. The multimodal input allows GPT-4o to analyze the visual data and generate a list of objects detected in the scene. Object detection is crucial for tasks such as inventory management, autonomous driving, and augmented reality applications and such.

Follow the further steps to replicate object detection using GPT-4o.

[OPTION BEGIN [curl]]

The following example shows how you can consume this generative AI model using curl. For more information about prompts, see the tutorial [Prompt LLMs in the Generative AI Hub in SAP AI Core & Launchpad Information published on SAP site](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fdevelopers.sap.com%2Ftutorials%2Fai-core-generative-ai.html).

Before you use this model, please ensure that the deployment has already been created. You can create the deployment either through [generative-ai-hub-sdk or AI Launchpad](https://developers.sap.com/tutorials/ai-core-generative-ai.html#ad7ffc1e-e94e-4de4-b70f-116b038aff04).

For inferencing the model through curl,

- open Windows PowerShell (for Windows based devices)

NOTE: **do not use DOS Prompt instead of PowerShell**

- open Terminal (for macOS based devices)

Enter the following command after replacing `<deployment_url>`, `<resource-group>`, `<token>` with the values for the corresponding model.

NOTE:
 
 - for macOS based devices use  use the **bash** command

 - for windows devices, use the **PowerShell** command

 - Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```bash
curl -L '<deployment-url>/chat/completions?api-version=2023-05-15' \
--header 'AI-Resource-Group: <resource-group>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "give me the bottle color and its count"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/objectDetection.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}'
```

```PowerShell
curl.exe -L "<deployment_url>/chat/completions?api-version=2023-05-15" --header "AI-Resource-Group: <resource-group>" --header "Content-Type: application/json" --header "Authorization: Bearer <token>" --data '{\"messages\": [{\"role\": \"user\", \"content\": [{\"type\": \"text\",\"text\": \"give me the bottle color and its count\"},{\"type\":\"image_url\",\"image_url\": {\"url\": \"https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/objectDetection.jpg\"}}]}],\"max_tokens\": 4096 }'
```

After executing the above curl command, we'll get the output as follows - 

![output](img/objectCurlOP.png)

[OPTION END]

[OPTION BEGIN [Postman]]

To begin using the APIs in AI Core, we start with setting up the authentication methods.

![image](img/consumption1.png)
![image](img/consumption2.png)
For ease of access, we set up the region, baseUrl and deploymentUrl variables as a pre-requisite. This avoids the need of passing these values repeatedly for different scenarios. 
NOTE: the deployment URL is specific to the model we intend to use.

![image](img/consumption34.png)
Add the name of your respective resource group. 

![image](img/consumption5.png)
Next, to begin making API calls, we’ll create a new access token. Now we’re ready to use the API for various models.

![image](img/consumption6.png)

Now that we’re done with the pre-requisites, we’ll proceed to using the API for GPT4o for Object Detection.

**NOTE:** Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```Body
{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "give me the bottle color and its count"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/objectDetection.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}
```

Add the above data in the body of the POST call, then hit ‘Send’ as follows - 

![image](img/object%20detection.png)

We get the following output accurately describing the scene in the image:

![image](img/object%20detection%20output.png)
[OPTION END]

For more information on the models refer to [Hello GPT-4o](https://openai.com/index/hello-gpt-4o/)

### Graph Analysis

Here, the tutorial demonstrates how GPT-4o can be used to interpret and analyze data presented in graphical form. By combining text and image input, the model can extract meaningful insights from charts, graphs, and other visual data representations. This step is valuable for data analysis, reporting, and decision-making processes.

Follow the further steps to replicate graph analysis using GPT-4o.

[OPTION BEGIN [curl]]

The following example shows how you can consume this generative AI model using curl. For more information about prompts, see the tutorial [Prompt LLMs in the Generative AI Hub in SAP AI Core & Launchpad Information published on SAP site](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fdevelopers.sap.com%2Ftutorials%2Fai-core-generative-ai.html).

Before you use this model, please ensure that the deployment has already been created. You can create the deployment either through [generative-ai-hub-sdk or AI Launchpad](https://developers.sap.com/tutorials/ai-core-generative-ai.html#ad7ffc1e-e94e-4de4-b70f-116b038aff04).

For inferencing the model through curl,

- open Windows PowerShell (for Windows based devices)

NOTE: **do not use DOS Prompt instead of PowerShell**

- open Terminal (for macOS based devices)

Enter the following command after replacing `<deployment_url>`, `<resource-group>`, `<token>` with the values for the corresponding model.

NOTE:
 
 - for macOS based devices use  use the **bash** command

 - for windows devices, use the **PowerShell** command

 - Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```bash
curl -L '<deployment-url>/chat/completions?api-version=2023-05-15' \
--header 'AI-Resource-Group: <resource-group>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "what is this graph about"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/graph.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}'
```

```PowerShell
curl.exe -L "<deployment_url>/chat/completions?api-version=2023-05-15" --header "AI-Resource-Group: <resource-group>" --header "Content-Type: application/json" --header "Authorization: Bearer <token>" --data '{\"messages\": [{\"role\": \"user\", \"content\": [{\"type\": \"text\",\"text\": \"what is this graph about\"},{\"type\":\"image_url\",\"image_url\": {\"url\": \"https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/graph.jpg\"}}]}],\"max_tokens\": 4096 }'
```

After executing the above curl command, we'll get the output as follows - 

![output](img/graphCurlOP.png)

[OPTION END]

[OPTION BEGIN [Postman]]

To begin using the APIs in AI Core, we start with setting up the authentication methods.

![image](img/consumption1.png)
![image](img/consumption2.png)
For ease of access, we set up the region, baseUrl and deploymentUrl variables as a pre-requisite. This avoids the need of passing these values repeatedly for different scenarios. 
NOTE: the deployment URL is specific to the model we intend to use.

![image](img/consumption34.png)
Add the name of your respective resource group. 

![image](img/consumption5.png)
Next, to begin making API calls, we’ll create a new access token. Now we’re ready to use the API for various models.

![image](img/consumption6.png)

Now that we’re done with the pre-requisites, we’ll proceed to using the API for GPT4o for Graph Analysis.

**NOTE:** Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```Body
{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "what is this graph about"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/graph.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}
```

Add the above data in the body of the POST call, then hit ‘Send’ as follows - 

![image](img/graph.png)

We get the following output accurately describing the scene in the image:

![image](img/graph%20analysis%20output.png)
[OPTION END]

For more information on the models refer to [Hello GPT-4o](https://openai.com/index/hello-gpt-4o/)

### Math

In this step, we explore how GPT-4o handles mathematical problems that involve both textual descriptions and visual data. The model can solve equations, interpret mathematical expressions in images, and provide detailed explanations of its reasoning. This capability is useful in educational tools, scientific research, and engineering applications.

Follow the further steps to replicate mathematical operations using GPT-4o.

[OPTION BEGIN [curl]]

The following example shows how you can consume this generative AI model using curl. For more information about prompts, see the tutorial [Prompt LLMs in the Generative AI Hub in SAP AI Core & Launchpad Information published on SAP site](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fdevelopers.sap.com%2Ftutorials%2Fai-core-generative-ai.html).

Before you use this model, please ensure that the deployment has already been created. You can create the deployment either through [generative-ai-hub-sdk or AI Launchpad](https://developers.sap.com/tutorials/ai-core-generative-ai.html#ad7ffc1e-e94e-4de4-b70f-116b038aff04).

For inferencing the model through curl,

- open Windows PowerShell (for Windows based devices)

NOTE: **do not use DOS Prompt instead of PowerShell**

- open Terminal (for macOS based devices)

Enter the following command after replacing `<deployment_url>`, `<resource-group>`, `<token>` with the values for the corresponding model.

NOTE:
 
 - for macOS based devices use  use the **bash** command

 - for windows devices, use the **PowerShell** command

 - Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```bash
curl -L '<deployment-url>/chat/completions?api-version=2023-05-15' \
--header 'AI-Resource-Group: <resource-group>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "find x"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/math.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}'
```

```PowerShell
curl.exe -L "<deployment_url>/chat/completions?api-version=2023-05-15" --header "AI-Resource-Group: <resource-group>" --header "Content-Type: application/json" --header "Authorization: Bearer <token>" --data '{\"messages\": [{\"role\": \"user\", \"content\": [{\"type\": \"text\",\"text\": \"find x\"},{\"type\":\"image_url\",\"image_url\": {\"url\": \"https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/math.jpg\"}}]}],\"max_tokens\": 4096 }'
```

After executing the above curl command, we'll get the output as follows - 

![output](img/mathCurlOP.png)

[OPTION END]

[OPTION BEGIN [Postman]]

To begin using the APIs in AI Core, we start with setting up the authentication methods.

![image](img/consumption1.png)
![image](img/consumption2.png)
For ease of access, we set up the region, baseUrl and deploymentUrl variables as a pre-requisite. This avoids the need of passing these values repeatedly for different scenarios. 
NOTE: the deployment URL is specific to the model we intend to use.

![image](img/consumption34.png)
Add the name of your respective resource group. 

![image](img/consumption5.png)
Next, to begin making API calls, we’ll create a new access token. Now we’re ready to use the API for various models.

![image](img/consumption6.png)

Now that we’re done with the pre-requisites, we’ll proceed to using the API for GPT4o for Math.

**NOTE:** Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```Body
{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "find x"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/math.jpg"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}
```

Add the above data in the body of the POST call, then hit ‘Send’ as follows - 

![image](img/math.png)

We get the following output accurately describing the scene in the image:

![image](img/math%20output.png)
[OPTION END]

For more information on the models refer to [Hello GPT-4o](https://openai.com/index/hello-gpt-4o/)

### Image to Text

The final step focuses on converting visual information into text. By providing an image as input, GPT-4o generates a textual description or transcription of the content. This step is particularly beneficial for accessibility tools, content creation, and archiving visual data.

Follow the further steps to replicate Optical Character Recognition (OCR) using GPT-4o.

[OPTION BEGIN [curl]]

The following example shows how you can consume this generative AI model using curl. For more information about prompts, see the tutorial [Prompt LLMs in the Generative AI Hub in SAP AI Core & Launchpad Information published on SAP site](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fdevelopers.sap.com%2Ftutorials%2Fai-core-generative-ai.html).

Before you use this model, please ensure that the deployment has already been created. You can create the deployment either through [generative-ai-hub-sdk or AI Launchpad](https://developers.sap.com/tutorials/ai-core-generative-ai.html#ad7ffc1e-e94e-4de4-b70f-116b038aff04).

For inferencing the model through curl,

- open Windows PowerShell (for Windows based devices)

NOTE: **do not use DOS Prompt instead of PowerShell**

- open Terminal (for macOS based devices)

Enter the following command after replacing `<deployment_url>`, `<resource-group>`, `<token>` with the values for the corresponding model.

NOTE:
 
 - for macOS based devices use  use the **bash** command

 - for windows devices, use the **PowerShell** command

 - Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```bash
curl -L '<deployment-url>/chat/completions?api-version=2023-05-15' \
--header 'AI-Resource-Group: <resource-group>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <token>' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "extract text"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/handwrittenText.png"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}'
```

```PowerShell
curl.exe -L "<deployment_url>/chat/completions?api-version=2023-05-15" --header "AI-Resource-Group: <resource-group>" --header "Content-Type: application/json" --header "Authorization: Bearer <token>" --data '{\"messages\": [{\"role\": \"user\", \"content\": [{\"type\": \"text\",\"text\": \"extract text\"},{\"type\":\"image_url\",\"image_url\": {\"url\": \"https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/handwrittenText.png\"}}]}],\"max_tokens\": 4096 }'
```

After executing the above curl command, we'll get the output as follows - 

![output](img/handwrittenCurlOP.png)

[OPTION END]

[OPTION BEGIN [Postman]]

To begin using the APIs in AI Core, we start with setting up the authentication methods.

![image](img/consumption1.png)
![image](img/consumption2.png)
For ease of access, we set up the region, baseUrl and deploymentUrl variables as a pre-requisite. This avoids the need of passing these values repeatedly for different scenarios. 
NOTE: the deployment URL is specific to the model we intend to use.

![image](img/consumption34.png)
Add the name of your respective resource group. 

![image](img/consumption5.png)
Next, to begin making API calls, we’ll create a new access token. Now we’re ready to use the API for various models.

![image](img/consumption6.png)

Now that we’re done with the pre-requisites, we’ll proceed to using the API for GPT4o for text extraction.

**NOTE:** Update the “url” to the link of the image resource you want to query the model upon and give the corresponding query in the “text” parameter.

```Body
{
    "messages": [
      {
        "role": "user",
        "content": [
           {
              "type": "text",
              "text": "extract text"
           },
           {
              "type": "image_url",
              "image_url": {
                 "url": "https://raw.githubusercontent.com/SAP-samples/ai-core-samples/main/09_BusinessAIWeek/images/handwrittenText.png"
              }
          }
        ]
      }
    ],
    "max_tokens": 4096
}
```

Add the above data in the body of the POST call, then hit ‘Send’ as follows - 

![image](img/handwrittenText.png)

We get the following output accurately describing the scene in the image:

![image](img/imagetotext%20output.png)
[OPTION END]

For more information on the models refer to [Hello GPT-4o](https://openai.com/index/hello-gpt-4o/)